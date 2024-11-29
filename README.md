Dawid Krajewski 97646

# Sprawozdanie
## Część obowiązkowa

### 1. Kod programu
[Kod](projekt.go)

### 2. Treść pliku Dockerfile
[Dockerfile](Dockerfile)

### 3. Polecenia
#### a. Do zbudowania obrazu
```
docker build -t local/zadanie1 .
[+] Building 1.5s (14/14) FINISHED                                                            docker:desktop-linux
 => [internal] load build definition from Dockerfile                                                          0.0s
 => => transferring dockerfile: 961B                                                                          0.0s
 => [internal] load metadata for docker.io/library/golang:1.23-alpine3.19                                     1.3s
 => [auth] library/golang:pull token for registry-1.docker.io                                                 0.0s
 => [internal] load .dockerignore                                                                             0.0s
 => => transferring context: 2B                                                                               0.0s
 => [builder 1/4] FROM docker.io/library/golang:1.23-alpine3.19@sha256:f72297ec1cf35152ecfe7a4d692825fc608fe  0.0s
 => => resolve docker.io/library/golang:1.23-alpine3.19@sha256:f72297ec1cf35152ecfe7a4d692825fc608fea8f3d3fa  0.0s
 => [internal] load build context                                                                             0.0s
 => => transferring context: 89B                                                                              0.0s
 => CACHED [stage-1 1/4] ADD alpine-minirootfs-3.20.3-x86_64.tar /                                            0.0s
 => CACHED [stage-1 2/4] RUN apk add --update --no-cache curl                                                 0.0s
 => CACHED [stage-1 3/4] WORKDIR /app                                                                         0.0s
 => CACHED [builder 2/4] WORKDIR /app                                                                         0.0s
 => CACHED [builder 3/4] COPY projekt.go .                                                                    0.0s
 => CACHED [builder 4/4] RUN go build projekt.go                                                              0.0s
 => CACHED [stage-1 4/4] COPY --from=builder /app /app                                                        0.0s
 => exporting to image                                                                                        0.1s
 => => exporting layers                                                                                       0.0s
 => => exporting manifest sha256:c5b82dc2d2582a4236028610fedab8900accb1aeac72d2d5129f8d0853b1d143             0.0s
 => => exporting config sha256:9834a0748914558c34b8a29f22b31a7027ab17087aceefee2f5c5073d658bc82               0.0s
 => => exporting attestation manifest sha256:6a75cbecb8ead56cbb00786e65cb3820f7ffe271c153811aceb908d3711fd66  0.0s
 => => exporting manifest list sha256:456b196139e92044c45b9bbca2e8bf74c065616f3a533b7a5f3674df18d90741        0.0s
 => => naming to docker.io/local/zadanie1:latest                                                              0.0s
 => => unpacking to docker.io/local/zadanie1:latest                                                           0.0s
```

#### b. Do uruchomienia kontenera
```
docker run -it -p 8080:8080 local/zadanie1
```

#### c. Sposobu uzyskania informacji, które wygenerował serwer w trakcie uruchamiania kontenera
Informacje same się wyświetlają od razu po uruchomieniu:
```
docker run -it -p 8080:8080 local/zadanie1
Data uruchomienia: 29.11.2024 14:12:29
Autor: Dawid Krajewski
Port: 8080
```

#### d. Sprawdzenia ile warstw posiada obraz
```
docker history local/zadanie1
IMAGE          CREATED          CREATED BY                                      SIZE      COMMENT
456b196139e9   12 minutes ago   CMD ["./projekt"]                               0B        buildkit.dockerfile.v0
<missing>      12 minutes ago   HEALTHCHECK &{["CMD-SHELL" "curl -f http://l…   0B        buildkit.dockerfile.v0
<missing>      12 minutes ago   EXPOSE map[8080/tcp:{}]                         0B        buildkit.dockerfile.v0
<missing>      12 minutes ago   COPY /app /app # buildkit                       7.48MB    buildkit.dockerfile.v0
<missing>      21 hours ago     WORKDIR /app                                    8.19kB    buildkit.dockerfile.v0
<missing>      21 hours ago     RUN /bin/sh -c apk add --update --no-cache c…   6.32MB    buildkit.dockerfile.v0
<missing>      2 weeks ago      ADD alpine-minirootfs-3.20.3-x86_64.tar / # …   8.46MB    buildkit.dockerfile.v0
<missing>      2 weeks ago      LABEL org.opencontainers.image.authors=Dawid…   0B        buildkit.dockerfile.v0
```

### 4. Zrzut ekranu potwierdzający działanie aplikacji
![obraz](https://github.com/user-attachments/assets/147fdeab-f1ed-4d6a-819a-40901134adea)

## Część dodatkowa, punkt 2
### Zawartość pliku Dockerfile_dod
[Dockerfile_dod](Dockerfile_dod)

### Polecenie użyte to zbudowania obrazu
```
docker buildx build -f Dockerfile_dod --ssh zad1git=[lokalizacja mojego ssh] \
--platform linux/arm64,linux/amd64 -t docker.io/krakos01/sw:zad1-dodatkowe \
--cache-to type=registry,ref=docker.io/krakos01/sw:zad1-dodatkowe-build-cache \
--cache-from type=registry,ref=docker.io/krakos01/sw:zad1-dodatkowe-build-cache --push .
[+] Building 175.3s (35/35) FINISHED                                                   docker-container:dc-builder
 => [internal] load build definition from Dockerfile_dod                                                      0.0s
 => => transferring dockerfile: 1.47kB                                                                        0.0s
 => resolve image config for docker-image://docker.io/docker/dockerfile:1.3                                   1.2s
 => [auth] docker/dockerfile:pull token for registry-1.docker.io                                              0.0s
 => CACHED docker-image://docker.io/docker/dockerfile:1.3@sha256:42399d4635eddd7a9b8a24be879d2f9a930d0ed040a  0.0s
 => => resolve docker.io/docker/dockerfile:1.3@sha256:42399d4635eddd7a9b8a24be879d2f9a930d0ed040a61324cfdf59  0.0s
 => [internal] load build definition from Dockerfile_dod                                                      0.0s
 => [internal] load .dockerignore                                                                             0.0s
 => => transferring context: 2B                                                                               0.0s
 => [linux/amd64 internal] load metadata for docker.io/library/golang:1.23-alpine3.19                         0.4s
 => [linux/arm64 internal] load metadata for docker.io/library/golang:1.23-alpine3.19                         0.6s
 => [auth] library/golang:pull token for registry-1.docker.io                                                 0.0s
 => importing cache manifest from docker.io/krakos01/sw:zad1-dodatkowe-build-cache                            1.5s
 => => inferred cache manifest type: application/vnd.oci.image.index.v1+json                                  0.0s
 => [linux/amd64 builder 1/6] FROM docker.io/library/golang:1.23-alpine3.19@sha256:f72297ec1cf35152ecfe7a4d6  0.0s
 => => resolve docker.io/library/golang:1.23-alpine3.19@sha256:f72297ec1cf35152ecfe7a4d692825fc608fea8f3d3fa  0.0s
 => [internal] load build context                                                                             0.0s
 => => transferring context: 59B                                                                              0.0s
 => [linux/arm64 builder 1/6] FROM docker.io/library/golang:1.23-alpine3.19@sha256:f72297ec1cf35152ecfe7a4d6  0.0s
 => => resolve docker.io/library/golang:1.23-alpine3.19@sha256:f72297ec1cf35152ecfe7a4d692825fc608fea8f3d3fa  0.0s
 => [auth] krakos01/sw:pull token for registry-1.docker.io                                                    0.0s
 => CACHED [linux/amd64 builder 2/6] WORKDIR /app                                                             0.0s
 => CACHED [linux/amd64 builder 3/6] RUN apk update &&     apk upgrade &&     apk add --no-cache openssh-cli  0.0s
 => CACHED [linux/amd64 builder 4/6] RUN mkdir -p -m 0600 ~/.ssh && ssh-keyscan github.com >> ~/.ssh/known_h  0.0s
 => CACHED [linux/arm64 builder 2/6] WORKDIR /app                                                             0.0s
 => CACHED [linux/arm64 builder 3/6] RUN apk update &&     apk upgrade &&     apk add --no-cache openssh-cli  0.0s
 => CACHED [linux/arm64 builder 4/6] RUN mkdir -p -m 0600 ~/.ssh && ssh-keyscan github.com >> ~/.ssh/known_h  0.0s
 => [linux/arm64 builder 5/6] RUN --mount=type=ssh,id=zad1git git clone git@github.com:krakos01/Zadanie1_SW.  6.3s
 => [linux/amd64 builder 5/6] RUN --mount=type=ssh,id=zad1git git clone git@github.com:krakos01/Zadanie1_SW  12.5s
 => [linux/arm64 builder 6/6] RUN go build projekt.go                                                       109.8s
 => [linux/amd64 builder 6/6] RUN go build projekt.go                                                         8.5s
 => CACHED [linux/amd64 stage-1 1/4] ADD alpine-minirootfs-3.20.3-x86_64.tar /                                0.0s
 => CACHED [stage-1 2/4] RUN apk add --update --no-cache curl                                                 0.0s
 => CACHED [linux/amd64 stage-1 3/4] WORKDIR /app                                                             0.0s
 => [linux/amd64 stage-1 4/4] COPY --from=builder /app /app                                                   0.1s
 => CACHED [linux/arm64 stage-1 1/4] ADD alpine-minirootfs-3.20.3-x86_64.tar /                                0.0s
 => CACHED [stage-1 2/4] RUN apk add --update --no-cache curl                                                 0.0s
 => CACHED [linux/arm64 stage-1 3/4] WORKDIR /app                                                             0.0s
 => [linux/arm64 stage-1 4/4] COPY --from=builder /app /app                                                   0.0s
 => exporting to image                                                                                       52.6s
 => => exporting layers                                                                                       1.0s
 => => exporting manifest sha256:57b2676c443a1696cac6d9d37540bc331941726e1956728222ea11d087ba1afd             0.0s
 => => exporting config sha256:33e25a3f2ee6401077dc3782f0b973483d60faa84104facb626e290123fde171               0.0s
 => => exporting attestation manifest sha256:be29c292b2bc857f74e81054897bea01c0a4bf3979b25d560e027a308546163  0.0s
 => => exporting manifest sha256:7e560674e519e74c4e45a78524e3d583109ce811940387726ac075eb32977232             0.0s
 => => exporting config sha256:d5021dda42caff8861c8d9c7b61f81813723842ff6b518062526848470de189f               0.0s
 => => exporting attestation manifest sha256:b1a1a7370715cd93a4baea68fb8d8a3156d676f83a7f5047ae825150aa5598a  0.0s
 => => exporting manifest list sha256:95ffbeb73bdcd9146dc1e8f47daeb873d8a82a594a0b385db3c2b927f6039bff        0.0s
 => => pushing layers                                                                                        49.0s
 => => pushing manifest for docker.io/krakos01/sw:zad1-dodatkowe@sha256:95ffbeb73bdcd9146dc1e8f47daeb873d8a8  2.5s
 => [auth] krakos01/sw:pull,push token for registry-1.docker.io                                               0.0s
 => exporting cache to registry                                                                               4.1s
 => => preparing build cache for export                                                                       4.1s
 => => writing layer sha256:20eb112219ac538dde901e21c15da3573b9d92caad0ab53998b58ffec7b12a0a                  0.6s
 => => writing layer sha256:30e3c8cc7fc2ae824e9be2b450b90bdf49a19754b5d591adf89c9b20fc02aa88                  0.3s
 => => writing layer sha256:77192e30d3fbc2488d9c0013e5d2cedec5ec11000b1e0c1c7008545e5788e0f7                  0.3s
 => => writing layer sha256:7a0cacad0ea8c49ce797ef2a159e288c4e71988952b9157ec465ee94affc3cac                  0.6s
 => => writing layer sha256:b48410e7857a4ba1486e1c97a00023e8db3c295d2e449d6c65f76f40bef5540c                  0.0s
 => => writing layer sha256:da9db072f522755cbeb85be2b3f84059b70571b229512f1571d9217b77e1087f                  0.2s
 => => writing config sha256:bff15164c72b4959f1abd77f70cc95efd36d90d5a7ee3f6549ede69ba042e3a3                 1.1s
 => => writing cache manifest sha256:83108be8296c1d5843d2f0002bfd2088f94eb185f412445437d2f865fe6c8ab7         0.8s

View build details: docker-desktop://dashboard/build/dc-builder/dc-builder0/vvob95dyne6vzxy7c1mscz3rx
```

### Uruchomienie kontenera
```
docker run -it -p 8080:8080 docker.io/krakos01/sw:zad1-dodatkowe
Unable to find image 'krakos01/sw:zad1-dodatkowe' locally
zad1-dodatkowe: Pulling from krakos01/sw
20eb112219ac: Download complete
b48410e7857a: Download complete
77192e30d3fb: Download complete
Digest: sha256:95ffbeb73bdcd9146dc1e8f47daeb873d8a82a594a0b385db3c2b927f6039bff
Status: Downloaded newer image for krakos01/sw:zad1-dodatkowe
Data uruchomienia: 29.11.2024 15:33:19
Autor: Dawid Krajewski
Port: 8080
```
