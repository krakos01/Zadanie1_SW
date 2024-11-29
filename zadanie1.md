Dawid Krajewski 97646

## Sprawozdanie 
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

