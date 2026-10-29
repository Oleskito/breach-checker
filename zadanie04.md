zadanie do samodzielnego wykonania
1. odpowiedz z przegladarki {"status":"ok"}
wynik docker backend logs:
172.18.0.1 - - [29/Oct/2026 11:45:44] "GET /health HTTP/1.1" 200 -


2. wyniki healthcheck-probe
docker run --rm --network breach-net healthcheck-probe:
backend: OK

docker run --rm healthcheck-probe:
backend: UNREACHABLE

docker stop backend
docker run --rm --network breach-net healthcheck-probe:
backend: UNREACHABLE

Aby kontenery się ze sobą komunikowały muszą być w tej samej sieci. Dodatkowo jeśli jeden z kontenerów jest wyłączony to nie mogą się ze sobą skomunikować


3. Bez wolumena po usunieciu kontenera i odpaleniu go od nowa - pliku już nie ma
cat: /tmp/notatka.txt: No such file or directory

drugie cat
Thu Oct 29 12:01:12 UTC 2026
Thu Oct 29 12:01:30 UTC 2026

Z wolumenem dane są zapisywane poza kontenerem więc przetrwają usunięcie kontenera
