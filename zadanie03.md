[
    {
        "Id": "sha256:617579cfee0167ba30f207e58c1a4e96a0b417c8c0bb25539aae7c2c4a6149d9",
        "RepoTags": [
            "aleksander-frontend:v1"
        ],
        "RepoDigests": [
            "aleksander-frontend@sha256:617579cfee0167ba30f207e58c1a4e96a0b417c8c0bb25539aae7c2c4a6149d9"
        ],
        "Comment": "buildkit.dockerfile.v0",
        "Created": "2026-10-22T10:15:44.981777446Z",
        "Config": {
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.31.8",
                "PKG_RELEASE=1",
                "DYNPKG_RELEASE=1",
                "NJS_VERSION=1.0.2",
                "NJS_RELEASE=1",
                "ACME_VERSION=0.4.1"
            ],
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "WorkingDir": "/",
            "Labels": {
                "autor": "Aleksander",
                "data": "2026-10-14",
                "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
            },
            "StopSignal": "SIGQUIT"
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 229069645,
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:75c137aedfb2760f88629236cb7b797630aed0c3d91d626d1d1bb694878fc2ba",
                "sha256:347d70688a4f620ee434007bc3b622592c459d0c45cbc275d0c8c3db0d2cb3e5",
                "sha256:0118eeeab20f23cb5712fe7b96dd0a3460b185c3f9fb0bdb59062a3972f5b9af",
                "sha256:a027351c56d0ec60ff555693e0afdd9ac6536425c3a6cd70cfd99438c32cf33b",
                "sha256:54733ab91a37b26f9dbcdebb53c37d88e967e1aca9e52984d231c7418c858dba",
                "sha256:26fc657c345556a2c48a5cdaa66f5e31ea881a18184bc943ad42cc46e93d7139",
                "sha256:6e2ae602f9d69418f36fd9c178e472fb6e6b468f6aadd3dbd759fcee552a7527",
                "sha256:a617e334a194398d200a112e5d4a39c65aa720650fe0fae732bdb1d7d4fb53a0",
                "sha256:dc43a20406c55385d23901c18c45bc0760bfd389a7daf3cf3e6d1d922692ebea",
                "sha256:82be276b5e5a0c040a1636d33dfab880cd4f6857146a0831f5f32669f00535d7",
                "sha256:5f70bf18a086007016e948b04aed3b82103a36bea41755b6cddfaf10ace3c6ef"
            ]
        },
        "Metadata": {
            "LastTagTime": "2026-10-22T10:19:21.702834237Z"
        },
        "Descriptor": {
            "mediaType": "application/vnd.oci.image.index.v1+json",
            "digest": "sha256:617579cfee0167ba30f207e58c1a4e96a0b417c8c0bb25539aae7c2c4a6149d9",
            "size": 856
        },
        "Identity": {
            "Build": [
                {
                    "Ref": "8vr3fqi6c5ojwqcupzxqb6a66",
                    "CreatedAt": "2026-10-22T10:19:24.265052757Z"
                }
            ]
        }
    }
]


--------------------INSPECT latest:

[
    {
        "Id": "sha256:0fa7be9f27c2919e8b1ae619c1e63ceebd189da48faf2a2daa0ad29a688a8456",
        "RepoTags": [
            "aleksander-frontend:latest"
        ],
        "RepoDigests": [
            "aleksander-frontend@sha256:0fa7be9f27c2919e8b1ae619c1e63ceebd189da48faf2a2daa0ad29a688a8456"
        ],
        "Comment": "buildkit.dockerfile.v0",
        "Created": "2026-10-22T10:15:44.981777446Z",
        "Config": {
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.31.8",
                "PKG_RELEASE=1",
                "DYNPKG_RELEASE=1",
                "NJS_VERSION=1.0.2",
                "NJS_RELEASE=1",
                "ACME_VERSION=0.4.1"
            ],
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "WorkingDir": "/",
            "Labels": {
                "autor": "Aleksander",
                "data": "2026-10-14",
                "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
            },
            "StopSignal": "SIGQUIT"
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 229069645,
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:75c137aedfb2760f88629236cb7b797630aed0c3d91d626d1d1bb694878fc2ba",
                "sha256:347d70688a4f620ee434007bc3b622592c459d0c45cbc275d0c8c3db0d2cb3e5",
                "sha256:0118eeeab20f23cb5712fe7b96dd0a3460b185c3f9fb0bdb59062a3972f5b9af",
                "sha256:a027351c56d0ec60ff555693e0afdd9ac6536425c3a6cd70cfd99438c32cf33b",
                "sha256:54733ab91a37b26f9dbcdebb53c37d88e967e1aca9e52984d231c7418c858dba",
                "sha256:26fc657c345556a2c48a5cdaa66f5e31ea881a18184bc943ad42cc46e93d7139",
                "sha256:6e2ae602f9d69418f36fd9c178e472fb6e6b468f6aadd3dbd759fcee552a7527",
                "sha256:a617e334a194398d200a112e5d4a39c65aa720650fe0fae732bdb1d7d4fb53a0",
                "sha256:dc43a20406c55385d23901c18c45bc0760bfd389a7daf3cf3e6d1d922692ebea",
                "sha256:82be276b5e5a0c040a1636d33dfab880cd4f6857146a0831f5f32669f00535d7",
                "sha256:5f70bf18a086007016e948b04aed3b82103a36bea41755b6cddfaf10ace3c6ef"
            ]
        },
        "Metadata": {
            "LastTagTime": "2026-10-22T10:19:37.735982653Z"
        },
        "Descriptor": {
            "mediaType": "application/vnd.oci.image.index.v1+json",
            "digest": "sha256:0fa7be9f27c2919e8b1ae619c1e63ceebd189da48faf2a2daa0ad29a688a8456",
            "size": 856
        },
        "Identity": {
            "Build": [
                {
                    "Ref": "8pze3x2938iwig7ojhodnwu9w",
                    "CreatedAt": "2026-10-22T10:19:37.766178731Z"
                }
            ]
        }
    }
]

----------------------------------docker history v1
IMAGE          CREATED         CREATED BY                                      SIZE      COMMENT
617579cfee01   6 minutes ago   EXPOSE [80/tcp]                                 0B        buildkit.dockerfile.v0
<missing>      6 minutes ago   RUN /bin/sh -c htmlhint /usr/share/nginx/htm…   4.1kB     buildkit.dockerfile.v0
<missing>      6 minutes ago   COPY . /usr/share/nginx/html # buildkit         32.8kB    buildkit.dockerfile.v0
<missing>      6 minutes ago   RUN /bin/sh -c apk add --no-cache nodejs npm…   102MB     buildkit.dockerfile.v0
<missing>      6 minutes ago   LABEL autor=Aleksander data=2026-10-14          0B        buildkit.dockerfile.v0
<missing>      11 hours ago    RUN /bin/sh -c set -x     && apkArch="$(cat …   52.4MB    buildkit.dockerfile.v0
<missing>      11 hours ago    ENV ACME_VERSION=0.4.1                          0B        buildkit.dockerfile.v0
<missing>      11 hours ago    ENV NJS_RELEASE=1                               0B        buildkit.dockerfile.v0
<missing>      11 hours ago    ENV NJS_VERSION=1.0.2                           0B        buildkit.dockerfile.v0
<missing>      12 hours ago    CMD ["nginx" "-g" "daemon off;"]                0B        buildkit.dockerfile.v0
<missing>      12 hours ago    STOPSIGNAL SIGQUIT                              0B        buildkit.dockerfile.v0
<missing>      12 hours ago    EXPOSE map[80/tcp:{}]                           0B        buildkit.dockerfile.v0
<missing>      12 hours ago    ENTRYPOINT ["/docker-entrypoint.sh"]            0B        buildkit.dockerfile.v0
<missing>      12 hours ago    COPY 30-tune-worker-processes.sh /docker-ent…   16.4kB    buildkit.dockerfile.v0
<missing>      12 hours ago    COPY 20-envsubst-on-templates.sh /docker-ent…   12.3kB    buildkit.dockerfile.v0
<missing>      12 hours ago    COPY 15-local-resolvers.envsh /docker-entryp…   12.3kB    buildkit.dockerfile.v0
<missing>      12 hours ago    COPY 10-listen-on-ipv6-by-default.sh /docker…   12.3kB    buildkit.dockerfile.v0
<missing>      12 hours ago    COPY docker-entrypoint.sh / # buildkit          8.19kB    buildkit.dockerfile.v0
<missing>      12 hours ago    RUN /bin/sh -c set -x     && addgroup -g 101…   5.75MB    buildkit.dockerfile.v0
<missing>      12 hours ago    ENV DYNPKG_RELEASE=1                            0B        buildkit.dockerfile.v0
<missing>      12 hours ago    ENV PKG_RELEASE=1                               0B        buildkit.dockerfile.v0
<missing>      12 hours ago    ENV NGINX_VERSION=1.31.8                        0B        buildkit.dockerfile.v0
<missing>      12 hours ago    LABEL maintainer=NGINX Docker Maintainers <d…   0B        buildkit.dockerfile.v0
<missing>      12 hours ago    CMD ["/bin/sh"]                                 0B        buildkit.dockerfile.v0
<missing>      12 hours ago    ADD alpine-minirootfs-3.24.3-x86_64.tar.gz /…   9.08MB    buildkit.dockerfile.v0


----------------------docker history latest
0fa7be9f27c2   7 minutes ago   EXPOSE [80/tcp]                                 0B        buildkit.dockerfile.v0
<missing>      7 minutes ago   RUN /bin/sh -c htmlhint /usr/share/nginx/htm…   4.1kB     buildkit.dockerfile.v0
<missing>      7 minutes ago   COPY . /usr/share/nginx/html # buildkit         32.8kB    buildkit.dockerfile.v0
<missing>      7 minutes ago   RUN /bin/sh -c apk add --no-cache nodejs npm…   102MB     buildkit.dockerfile.v0
<missing>      7 minutes ago   LABEL autor=Aleksander data=2026-10-14          0B        buildkit.dockerfile.v0
<missing>      11 hours ago    RUN /bin/sh -c set -x     && apkArch="$(cat …   52.4MB    buildkit.dockerfile.v0
<missing>      11 hours ago    ENV ACME_VERSION=0.4.1                          0B        buildkit.dockerfile.v0
<missing>      11 hours ago    ENV NJS_RELEASE=1                               0B        buildkit.dockerfile.v0
<missing>      11 hours ago    ENV NJS_VERSION=1.0.2                           0B        buildkit.dockerfile.v0
<missing>      12 hours ago    CMD ["nginx" "-g" "daemon off;"]                0B        buildkit.dockerfile.v0
<missing>      12 hours ago    STOPSIGNAL SIGQUIT                              0B        buildkit.dockerfile.v0
<missing>      12 hours ago    EXPOSE map[80/tcp:{}]                           0B        buildkit.dockerfile.v0
<missing>      12 hours ago    ENTRYPOINT ["/docker-entrypoint.sh"]            0B        buildkit.dockerfile.v0
<missing>      12 hours ago    COPY 30-tune-worker-processes.sh /docker-ent…   16.4kB    buildkit.dockerfile.v0
<missing>      12 hours ago    COPY 20-envsubst-on-templates.sh /docker-ent…   12.3kB    buildkit.dockerfile.v0
<missing>      12 hours ago    COPY 15-local-resolvers.envsh /docker-entryp…   12.3kB    buildkit.dockerfile.v0
<missing>      12 hours ago    COPY 10-listen-on-ipv6-by-default.sh /docker…   12.3kB    buildkit.dockerfile.v0
<missing>      12 hours ago    COPY docker-entrypoint.sh / # buildkit          8.19kB    buildkit.dockerfile.v0
<missing>      12 hours ago    RUN /bin/sh -c set -x     && addgroup -g 101…   5.75MB    buildkit.dockerfile.v0
<missing>      12 hours ago    ENV DYNPKG_RELEASE=1                            0B        buildkit.dockerfile.v0
<missing>      12 hours ago    ENV PKG_RELEASE=1                               0B        buildkit.dockerfile.v0
<missing>      12 hours ago    ENV NGINX_VERSION=1.31.8                        0B        buildkit.dockerfile.v0
<missing>      12 hours ago    LABEL maintainer=NGINX Docker Maintainers <d…   0B        buildkit.dockerfile.v0
<missing>      12 hours ago    CMD ["/bin/sh"]                                 0B        buildkit.dockerfile.v0
<missing>      12 hours ago    ADD alpine-minirootfs-3.24.3-x86_64.tar.gz /…   9.08MB    buildkit.dockerfile.v0


Odpowiedzi na pytania: moje warstwy to te które mają najnowszy czas (ile minut temu został zbuildowany obraz), pozostałe pochodzą z obrazu bazowego

------------zad2
zawartosc build jest taka sama:
Thu Oct 22 10:30:22 UTC 2026

docker ps:
CONTAINER ID   IMAGE                    COMMAND                  CREATED              STATUS              PORTS                                     NAMES
9a41887a915e   aleksander-frontend:v2   "/docker-entrypoint.…"   About a minute ago   Up About a minute   0.0.0.0:8000->80/tcp, [::]:8000->80/tcp   frontend2
58f0b90acc33   aleksander-frontend:v2   "/docker-entrypoint.…"   2 minutes ago        Up 2 minutes        0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   frontend

Czas jest taki sam ponieważ RUN został wykonany tylko raz i był to czas uruchomienia pierwszego kontenera

linia root po nadpisaniu cmd:
root   /usr/share/nginx/html;


wynik docker exec:
html
index.html
script.js
style.css

wynik docker exec html:
50x.html
build.txt
index.html

docker sprawdził plik index.html z folder /nginx zamiast z folderu /html
build jest sprawny poniewaz jest to normalny plik html bez błędu wiec nic nie wykryje htmlhint

usuniecie latest:
Untagged: aleksander-frontend:latest
Deleted: sha256:0fa7be9f27c2919e8b1ae619c1e63ceebd189da48faf2a2daa0ad29a688a8456

w docker images v2 nadal istnieje

usuniecie v2
Untagged: aleksander-frontend:v2
Deleted: sha256:99c31c66221201dd4339c358ed20b292798ab415f934095e93bd240b5a17d435