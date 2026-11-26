###
odnośnik do uruchomienia actions:
https://github.com/Oleskito/breach-checker/actions/runs/45826754394

błąd:
 > [lint 5/5] RUN htmlhint index.html:
0.277 
0.295    /site/index.html
0.296       L16 |        <h1>Zmieniony tekst naglowka
0.296                    ^ Tag must be paired, missing: [ </h1> ], start tag match failed [ <h1> ] on line 16. (tag-pair)
0.296 
0.298 Scanned 1 files, found 1 errors in 1 files (23 ms)
------
Error: Process completed with exit code 1.

odnośnik do naprawionego actions:
https://github.com/Oleskito/breach-checker/actions/runs/45827285032
Wcześniej pipeline pobierał z rejestru tylko gotowy obraz backendu, a frontend budował na bieżąco z plików na maszynie testowej. Teraz oba obrazy są najpierw publikowane w GHCR i stamtąd pobierane do testów, więc sprawdzamy dokładnie te same gotowe paczki, które trafią na produkcję.
###


###
odnośnik po zmienieniu dockerfile 127.0.0.1:5000:
https://github.com/Oleskito/breach-checker/actions/runs/45827525120
odnośnik po przywróceniu 0.0.0.0:
https://github.com/Oleskito/breach-checker/actions/runs/45827930971
Tag latest wciąż wskazywał na poprzedni, działający obraz, ponieważ po błędzie w testach krok promote w ogóle się nie uruchomił i nie nadpisał tagu. Jest to kluczowe dla użytkownika pobierającego obraz bez podawania wersji (czyli domyślnie latest), bo dzięki temu ma gwarancję, że pobiera ostatnią stabilną wersję, a nie wersję zepsutą.
###

###
wykonanie poleceń w terminalu:
---------------------
Removing login credentials for ghcr.io
latest: Pulling from oleskito/breach-checker-backend
4ad78ab98a70: Pull complete
83a14706aa6d: Pull complete
e3e428093f5e: Pull complete
e8fbaa2d830a: Pull complete
286d8c291daa: Pull complete
25865e85c94f: Pull complete
263f437192fc: Pull complete
647d3f21ad12: Pull complete
30cf67d7101c: Pull complete
Digest: sha256:1a1064a3c49e94065fb0f8415e8b8dfe67364249327c3f185bd2943d616611fd
Status: Downloaded newer image for ghcr.io/oleskito/breach-checker-backend:latest
ghcr.io/oleskito/breach-checker-backend:latest
Error response from daemon: failed to resolve reference "ghcr.io/oleskito/breach-checker-backend:4489f99": ghcr.io/oleskito/breach-checker-backend:4489f99: not found
REPOSITORY                                TAG       DIGEST                                                                    IMAGE ID       CREATED         SIZE
ghcr.io/oleskito/breach-checker-backend   latest    sha256:1a1064a3c49e94065fb0f8415e8b8dfe67364249327c3f185bd2943d616611fd   1a1064a3c49e   7 minutes ago   212MB
The push refers to repository [ghcr.io/oleskito/breach-checker-backend]
286d8c291daa: Layer already exists                                                                                                                                                       
30cf67d7101c: Layer already exists                                                                                                                                                       
e3e428093f5e: Layer already exists                                                                                                                                                       
83a14706aa6d: Layer already exists                                                                                                                                                       
263f437192fc: Layer already exists
e8fbaa2d830a: Layer already exists
25865e85c94f: Layer already exists
647d3f21ad12: Layer already exists
4ad78ab98a70: Layer already exists
latest: digest: sha256:1a1064a3c49e94065fb0f8415e8b8dfe67364249327c3f185bd2943d616611fd size: 2199
---------------------
Identyczne digesty pokazują, że tag latest i tag ze skrótem commita wskazują na dokładnie ten sam obraz. Polecenie docker pull zadziałało bez logowania, ponieważ po zmianie widoczności pakietu na publiczną każdy może go swobodnie pobrać, natomiast docker push wymaga autoryzacji do zapisu – do czego właśnie był potrzebny token z uprawnieniem write:packages.
###