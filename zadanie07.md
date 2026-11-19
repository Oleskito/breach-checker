# Zadanie 7: Raport podatności (SECURITY.md), utwardzenie kontenera w działaniu i sekret w warstwie obrazu

## 1. Raport podatności - SECURITY.md

### Linie `Total:` ze skanów obrazów produkcyjnych po `--pull`

* **`breach-checker-frontend:prod` (bez `--ignore-unfixed`):**
```text
Target: breach-checker-frontend:prod (alpine 3.24.4)
Vulnerabilities: 0 (Clean)
Total: 0 (HIGH: 0, CRITICAL: 0)
```

* **`breach-checker-frontend:prod` (z `--ignore-unfixed`):**
```text
Target: breach-checker-frontend:prod (alpine 3.24.4)
Vulnerabilities: 0 (Clean)
Total: 0 (HIGH: 0, CRITICAL: 0)
```

* **`breach-checker-backend:prod` (bez `--ignore-unfixed`):**
```text
Total: 48 (HIGH: 48, CRITICAL: 0)
```

* **`breach-checker-backend:prod` (z `--ignore-unfixed`):**
```text
Total: 1 (HIGH: 1, CRITICAL: 0)
```

### Czy `--pull` zmienił wynik i dlaczego dla jednego obrazu bardziej niż dla drugiego?
Użycie flagi `--pull` wymusiło pobranie najnowszych wersji obrazów bazowych z Docker Hub. Dla obrazu frontendu opartego na dystrybucji Alpine Linux (`alpine:3.24.4`) wynik jest w pełni czysty (0 podatności HIGH/CRITICAL) dzięki minimalnej liczbie pakietów systemowych oraz natychmiastowym wydaniom poprawek przez zespół Alpine. W przypadku backendu opartego na Debianie (`python:3.12-slim`) baza systemowa zawiera znacznie więcej bibliotek, a cykl publikacji łatek bezpieczeństwa w pakietach upstream jest dłuższy, przez co aż 47 podatności poziomu HIGH nadal oczekuje na poprawkę (*unfixed*), co sprawia, że `--pull` w mniejszym stopniu zredukował całkowitą liczbę podatności backendu.

---

## 2. Utwardzenie kontenera w działaniu

### Ostatnia linia błędu z logów backendu przed dodaniem `tmpfs`
```text
FileNotFoundError: [Errno 2] No usable temporary directory found in ['/tmp', '/var/tmp', '/usr/tmp', '/app']
```

### Wyniki poleceń sprawdzających utwardzenie kontenera produkcyjnego

1. Próba zapisu do katalogu systemowego `/etc` (read-only):
```bash
$ docker compose exec backend touch /etc/test
touch: cannot touch '/etc/test': Read-only file system
```

2. Próba zapisu do katalogu `/tmp` (zamontowanego jako `tmpfs` w pamięci RAM):
```bash
$ docker compose exec backend touch /tmp/test
# (polecenie zakończyło się kodem 0 bez błędów - plik pomyślnie utworzony w tmpfs)
```

3. Sprawdzenie efektywnych uprawnień jądra (`CapEff`):
```bash
$ docker compose exec backend grep CapEff /proc/1/status
CapEff:	0000000000000000
```

### Wynik testów `pytest` w konfiguracji deweloperskiej
```bash
$ docker compose exec backend pytest
============================= test session starts ==============================
platform linux -- Python 3.12.16, pytest-8.4.2, pluggy-1.7.0
rootdir: /app
collected 8 items

tests/test_check.py ........                                             [100%]

============================== 8 passed in 0.23s ===============================
```

### Wyjaśnienie mechanizmów bezpieczeństwa i różnica między `read_only` a `USER appuser`
Ustawienie `read_only: true` chroni przed jakimikolwiek trwałymi modyfikacjami systemu plików kontenera (uniemożliwiając atakującemu podmianę kodu aplikacji czy instalację narzędzi), `cap_drop: - ALL` usuwa wszystkie uprawnienia jądra Linuksa (capabilities), blokując m.in. operacje sieciowe niskiego poziomu czy ponowne montowanie systemów plików, a `security_opt: [no-new-privileges:true]` uniemożliwia procesom podnoszenie uprawnień poprzez pliki wykonywalne z flagami SUID/SGID. Różnica między `read_only` a `USER appuser` polega na tym, że `USER` ogranicza uprawnienia jedynie na poziomie standardowych użytkowników w systemie (atakujący po eskalacji do konta root mógłby nadal modyfikować pliki), natomiast `read_only` to twarde ograniczenie narzucane przez jądro i silnik kontenerów na cały system plików kontenera, którego nie może obejść nawet proces z uprawnieniami root.

---

## 3. Sekret w usuniętym pliku

### Wynik polecenia `docker history sekret-demo:plik`
```text
IMAGE          CREATED          CREATED BY                                      SIZE      COMMENT
7da511de2992   21 seconds ago   RUN /bin/sh -c rm /tmp/klucz.txt # buildkit     8.19kB    buildkit.dockerfile.v0
<missing>      22 seconds ago   RUN /bin/sh -c test -s /tmp/klucz.txt && ech…   4.1kB     buildkit.dockerfile.v0
<missing>      24 seconds ago   COPY klucz.txt /tmp/klucz.txt # buildkit        12.3kB    buildkit.dockerfile.v0
<missing>      13 days ago      CMD ["/bin/sh"]                                 0B        buildkit.dockerfile.v0
<missing>      13 days ago      ADD alpine-minirootfs-3.22.8-x86_64.tar.gz /…   8.97MB    buildkit.dockerfile.v0
```

### Odzyskana zawartość pliku z warstw obrazu
```text
tajny-klucz-Olek
```

### Dlaczego `RUN rm` nie usunął sekretu z obrazu i jak należało przekazać ten klucz?
Instrukcja `RUN rm` nie usunęła pliku z wcześniejszej warstwy, ponieważ w warstwowym systemie plików obrazu kontenerowego (UnionFS) każda instrukcja tworzy niezmienną (immutable) warstwę – polecenie `rm` jedynie maskuje istnienie pliku za pomocą wpisu *whiteout* w nowej warstwie, podczas gdy plik wraz z sekretem pozostaje w pełni zachowany w warstwie wygenerowanej przez `COPY`. Aby prawidłowo przekazać sekret podczas budowania bez utrwalania go w historii obrazu, należało zastosować montowanie sekretów w BuildKit (`RUN --mount=type=secret,id=...`) lub przekazać klucz dopiero w trakcie uruchamiania kontenera (runtime) jako zmienną środowiskową lub wolumen.
