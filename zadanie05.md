1. Wynik docker compose up -d --build:
PS C:\Users\olekp\Documents\Semestr III\Wirtualizacja_lab> docker compose up -d --build 
[+] Building 32.4s (25/25) FINISHED                                                                                                                                                                                  
 => [internal] load local bake definitions                                                                                                                                                                      0.0s
 => => reading from stdin 1.15kB                                                                                                                                                                                0.0s
 => [backend internal] load build definition from Dockerfile                                                                                                                                                    0.1s
 => => transferring dockerfile: 367B                                                                                                                                                                            0.0s
 => [frontend internal] load build definition from Dockerfile                                                                                                                                                   0.1s
 => => transferring dockerfile: 374B                                                                                                                                                                            0.0s
 => [frontend internal] load metadata for docker.io/library/nginx:alpine                                                                                                                                        0.3s
 => [backend internal] load metadata for docker.io/library/python:3.12-slim                                                                                                                                     6.4s
 => [frontend internal] load .dockerignore                                                                                                                                                                      0.1s
 => => transferring context: 66B                                                                                                                                                                                0.0s
 => [frontend 1/6] FROM docker.io/library/nginx:alpine@sha256:785835ea65db4bba6f021acc0f3be91b0fef76a53fe41f8588c6698d2aed0606                                                                                  0.1s
 => => resolve docker.io/library/nginx:alpine@sha256:785835ea65db4bba6f021acc0f3be91b0fef76a53fe41f8588c6698d2aed0606                                                                                           0.1s
 => [frontend internal] load build context                                                                                                                                                                      0.0s
 => => transferring context: 120B                                                                                                                                                                               0.0s
 => CACHED [frontend 2/6] RUN apk add --no-cache nodejs npm && npm install -g htmlhint                                                                                                                          0.0s
 => CACHED [frontend 3/6] COPY index.html style.css script.js /usr/share/nginx/html/                                                                                                                            0.0s
 => CACHED [frontend 4/6] COPY nginx.conf /etc/nginx/conf.d/default.conf                                                                                                                                        0.0s
 => CACHED [frontend 5/6] RUN date > /usr/share/nginx/html/build.txt                                                                                                                                            0.0s
 => CACHED [frontend 6/6] RUN htmlhint /usr/share/nginx/html/index.html                                                                                                                                         0.0s
 => [frontend] exporting to image                                                                                                                                                                               0.4s
 => => exporting layers                                                                                                                                                                                         0.0s
 => => exporting manifest sha256:15ea203b870e212323327a0ac3308cc7e11e5ae00b268d5d864d2d0596e69595                                                                                                               0.0s
 => => exporting config sha256:00ef1c534302618e13c55a20b5202e5050f2ffc140ea979ddaf75d22b0fff395                                                                                                                 0.0s
 => => exporting attestation manifest sha256:473333c5149e99d1d47f9bd456aea9304124faf247496d46b313fe356e3d9095                                                                                                   0.1s
 => => exporting manifest list sha256:72bbaa1e038e17d21c68f8e1d29b530c4d3b2b18d89a9ff460dce327019cfd91                                                                                                          0.1s
 => => naming to docker.io/library/wirtualizacja_lab-frontend:latest                                                                                                                                            0.0s
 => => unpacking to docker.io/library/wirtualizacja_lab-frontend:latest                                                                                                                                         0.0s
 => [frontend] resolving provenance for metadata file                                                                                                                                                           0.0s
 => [auth] library/python:pull token for registry-1.docker.io                                                                                                                                                   0.0s
 => [backend internal] load .dockerignore                                                                                                                                                                       0.0s
 => => transferring context: 2B                                                                                                                                                                                 0.0s
 => [backend 1/5] FROM docker.io/library/python:3.12-slim@sha256:b18b261e1b4974b4f321451ad5251ded85abb22c2b8b262da527dda1d031ab30                                                                               0.2s
 => => resolve docker.io/library/python:3.12-slim@sha256:b18b261e1b4974b4f321451ad5251ded85abb22c2b8b262da527dda1d031ab30                                                                                       0.1s
 => [backend internal] load build context                                                                                                                                                                       0.0s
 => => transferring context: 63B                                                                                                                                                                                0.0s
 => [backend 2/5] WORKDIR /app                                                                                                                                                                                  0.1s
 => [backend 3/5] COPY requirements.txt .                                                                                                                                                                       0.2s
 => [backend 4/5] RUN pip install --no-cache-dir -r requirements.txt                                                                                                                                           18.8s
 => [backend 5/5] COPY app.py .                                                                                                                                                                                 0.2s
 => [backend] exporting to image                                                                                                                                                                                3.2s
 => => exporting layers                                                                                                                                                                                         2.1s
 => => exporting manifest sha256:ef043f36b2128229b1b854aa6c9d8f2a6bbdc8325edba8263ffaf149c1957b4d                                                                                                               0.1s
 => => exporting config sha256:8e62017af2ec82ec16e1cc00d2e8bb05d6c04c2e4a40e2da611ca1ff19c9244a                                                                                                                 0.1s
 => => exporting attestation manifest sha256:4eda21dd12cd8b449fb6f938e5660e2306687f52135da8149695efd694f40452                                                                                                   0.1s
 => => exporting manifest list sha256:f56ef5cf85d2b2b1718b3eecc88a02500c1844824e4b70ae614279a6c4a6822a                                                                                                          0.1s
 => => naming to docker.io/library/wirtualizacja_lab-backend:latest                                                                                                                                             0.0s
 => => unpacking to docker.io/library/wirtualizacja_lab-backend:latest                                                                                                                                          0.7s
 => [backend] resolving provenance for metadata file                                                                                                                                                            0.1s
[+] up 6/6
 ✔ Image wirtualizacja_lab-backend        Built                                                                                                                                                                 33.0s
 ✔ Image wirtualizacja_lab-frontend       Built                                                                                                                                                                 33.0s
 ✔ Network wirtualizacja_lab_default      Created                                                                                                                                                                0.1s
 ✔ Container wirtualizacja_lab-db-1       Healthy                                                                                                                                                                7.2s
 ✔ Container wirtualizacja_lab-backend-1  Healthy                                                                                                                                                               37.6s
 ✔ Container wirtualizacja_lab-frontend-1 Started 


 Wynik polecenia docker compose ps:
 NAME                           IMAGE                        COMMAND                  SERVICE    CREATED              STATUS                        PORTS
wirtualizacja_lab-backend-1    wirtualizacja_lab-backend    "python app.py"          backend    About a minute ago   Up About a minute (healthy)   5000/tcp
wirtualizacja_lab-db-1         postgres:16-alpine           "docker-entrypoint.s…"   db         About a minute ago   Up About a minute (healthy)   5432/tcp
wirtualizacja_lab-frontend-1   wirtualizacja_lab-frontend   "/docker-entrypoint.…"   frontend   About a minute ago   Up About a minute             0.0.0.0:8080->80/tcp, [::]:8080->80/tcp


2. Trwałość bazy:
wynik polecenia insert:
ERROR:  duplicate key value violates unique constraint "leaked_hashes_pkey"
DETAIL:  Key (hash)=(bc45408273d7e1914b741c3407b0b559764f7876) already exists.

###hash został dodany wcześniej dlatego jest error

po wykonaniu compose down + up:
ERROR:  duplicate key value violates unique constraint "leaked_hashes_pkey"
DETAIL:  Key (hash)=(bc45408273d7e1914b741c3407b0b559764f7876) already exists.

po wykonaniu down -v + up
INSERT 0 1

3. SKALOWANIE
docker compose ps po utworzeniu kopii backendu:
NAME                           IMAGE                        COMMAND                  SERVICE    CREATED              STATUS                        PORTS
wirtualizacja_lab-backend-1    wirtualizacja_lab-backend    "python app.py"          backend    2 minutes ago        Up 2 minutes (healthy)        5000/tcp
wirtualizacja_lab-backend-2    wirtualizacja_lab-backend    "python app.py"          backend    About a minute ago   Up About a minute (healthy)   5000/tcp
wirtualizacja_lab-backend-3    wirtualizacja_lab-backend    "python app.py"          backend    About a minute ago   Up About a minute (healthy)   5000/tcp
wirtualizacja_lab-db-1         postgres:16-alpine           "docker-entrypoint.s…"   db         2 minutes ago        Up 2 minutes (healthy)        5432/tcp
wirtualizacja_lab-frontend-1   wirtualizacja_lab-frontend   "/docker-entrypoint.…"   frontend   2 minutes ago        Up 2 minutes                  0.0.0.0:8080->80/tcp, [::]:8080->80/tcp

#kilka linii z logs przed restartem
backend-1  | check: hash=bc454...
backend-1  | 172.19.0.4 - - [05/Nov/2026 11:17:05] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.19.0.4 - - [05/Nov/2026 11:17:05] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.19.0.4 - - [05/Nov/2026 11:17:05] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.19.0.4 - - [05/Nov/2026 11:17:06] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.19.0.4 - - [05/Nov/2026 11:17:06] "POST /check HTTP/1.1" 200 -
#jak widać wszystkie zapytania obsługuje backend-1

#kilka lini logs po restarcie frontend:
backend-1  | check: hash=bc454...
backend-1  | 172.19.0.4 - - [05/Nov/2026 11:17:05] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.19.0.4 - - [05/Nov/2026 11:17:05] "POST /check HTTP/1.1" 200 -
backend-2  | 172.19.0.4 - - [05/Nov/2026 11:19:29] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...
backend-1  | 172.19.0.4 - - [05/Nov/2026 11:17:05] "POST /check HTTP/1.1" 200 -
backend-1  | check: hash=bc454...

#Nginx rozwiązuje nazwy tylko raz - w momencie startowania konteneru dlatego przed restartem był tylko jeden adres backend widoczny
#gdyby backend miał przypisane porty 5000:5000 to skalowanie nie działałoby - każda replika miałaby mieć ten sam port