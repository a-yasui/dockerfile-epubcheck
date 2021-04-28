# Development Memo

I forget the buildx command. This is history of building multi-arch docker image.

```
 ⚓  ~/d/dockerfile-epubcheck  master  docker buildx create --name epubcheck
epubcheck
 ⚓  ~/d/dockerfile-epubcheck  master  docker buildx ls
NAME/NODE    DRIVER/ENDPOINT             STATUS   PLATFORMS
epubcheck    docker-container                     
  epubcheck0 unix:///var/run/docker.sock inactive 
default *    docker                               
  default    default                     running  linux/arm64, linux/amd64, linux/riscv64, linux/ppc64le, linux/s390x, linux/386, linux/arm/v7, linux/arm/v6
 ⚓  ~/d/dockerfile-epubcheck  master  docker buildx use epubcheck
 ⚓  ~/d/dockerfile-epubcheck  master  docker buildx inspect --bootstrap
[+] Building 16.7s (1/1) FINISHED                                                                                                                              
 => [internal] booting buildkit                                                                                                                          16.7s
 => => pulling image moby/buildkit:buildx-stable-1                                                                                                       14.9s
 => => creating container buildx_buildkit_epubcheck0                                                                                                      1.8s
Name:   epubcheck
Driver: docker-container

Nodes:
Name:      epubcheck0
Endpoint:  unix:///var/run/docker.sock
Status:    running
Platforms: linux/arm64, linux/amd64, linux/riscv64, linux/ppc64le, linux/s390x, linux/386, linux/arm/v7, linux/arm/v6
 ⚓  ~/d/dockerfile-epubcheck  master  docker buildx build --platform linux/amd64,linux/arm64,linux/arm/v7 -t  atyasu/epubcheck:version-4.2.5 --push .
[+] Building 191.7s (24/24) FINISHED                                                                                                                           
 => [internal] load build definition from Dockerfile                                                                                                      1.2s
 => => transferring dockerfile: 504B                                                                                                                      0.0s
 => [internal] load .dockerignore                                                                                                                         1.4s
 => => transferring context: 2B                                                                                                                           0.0s
 => [linux/arm/v7 internal] load metadata for docker.io/library/alpine:3.13                                                                               5.1s
 => [linux/amd64 internal] load metadata for docker.io/library/alpine:3.13                                                                                4.8s
 => [linux/arm64 internal] load metadata for docker.io/library/alpine:3.13                                                                                4.9s
 => [auth] library/alpine:pull token for registry-1.docker.io                                                                                             0.0s
 => [linux/amd64 1/5] FROM docker.io/library/alpine:3.13@sha256:69e70a79f2d41ab5d637de98c1e0b055206ba40a8145e7bddb55ccc04e13cf8f                          1.4s
 => => resolve docker.io/library/alpine:3.13@sha256:69e70a79f2d41ab5d637de98c1e0b055206ba40a8145e7bddb55ccc04e13cf8f                                      0.8s
 => => sha256:540db60ca9383eac9e418f78490994d0af424aab7bf6d0e47ac8ed4e2e9bcbba 2.81MB / 2.81MB                                                            0.7s
 => => extracting sha256:540db60ca9383eac9e418f78490994d0af424aab7bf6d0e47ac8ed4e2e9bcbba                                                                 0.5s
 => [linux/arm64 1/5] FROM docker.io/library/alpine:3.13@sha256:69e70a79f2d41ab5d637de98c1e0b055206ba40a8145e7bddb55ccc04e13cf8f                          1.7s
 => => resolve docker.io/library/alpine:3.13@sha256:69e70a79f2d41ab5d637de98c1e0b055206ba40a8145e7bddb55ccc04e13cf8f                                      0.6s
 => => sha256:595b0fe564bb9444ebfe78288079a01ee6d7f666544028d5e96ba610f909ee43 2.71MB / 2.71MB                                                            0.8s
 => => extracting sha256:595b0fe564bb9444ebfe78288079a01ee6d7f666544028d5e96ba610f909ee43                                                                 0.6s
 => [linux/arm/v7 1/5] FROM docker.io/library/alpine:3.13@sha256:69e70a79f2d41ab5d637de98c1e0b055206ba40a8145e7bddb55ccc04e13cf8f                         1.6s
 => => resolve docker.io/library/alpine:3.13@sha256:69e70a79f2d41ab5d637de98c1e0b055206ba40a8145e7bddb55ccc04e13cf8f                                      0.8s
 => => sha256:e160e00eb35d5bc2373770873fbc9c8f5706045b0b06bfd1c364fcf69f02e9fe 2.42MB / 2.42MB                                                            0.8s
 => => extracting sha256:e160e00eb35d5bc2373770873fbc9c8f5706045b0b06bfd1c364fcf69f02e9fe                                                                 0.4s
 => [internal] load build context                                                                                                                         2.3s
 => => transferring context: 679B                                                                                                                         0.0s
 => [linux/arm64 2/5] RUN apk add --update bash curl unzip openjdk7 &&     rm /var/cache/apk/*                                                           94.1s
 => [linux/amd64 2/5] RUN apk add --update bash curl unzip openjdk7 &&     rm /var/cache/apk/*                                                           95.2s
 => [linux/arm/v7 2/5] RUN apk add --update bash curl unzip openjdk7 &&     rm /var/cache/apk/*                                                         104.0s
 => [linux/arm64 3/5] RUN curl -L -o "/tmp/$EPUBCHECK.zip" "https://github.com/IDPF/epubcheck/releases/download/v${EPUBCHECK#*-}/$EPUBCHECK.zip"  && unz  4.8s
 => [linux/amd64 3/5] RUN curl -L -o "/tmp/$EPUBCHECK.zip" "https://github.com/IDPF/epubcheck/releases/download/v${EPUBCHECK#*-}/$EPUBCHECK.zip"  && unz  5.3s
 => [linux/arm64 4/5] ADD app /app/                                                                                                                       1.2s
 => [linux/arm64 5/5] WORKDIR /app                                                                                                                        1.4s
 => [linux/amd64 4/5] ADD app /app/                                                                                                                       1.3s
 => [linux/amd64 5/5] WORKDIR /app                                                                                                                        1.3s
 => [linux/arm/v7 3/5] RUN curl -L -o "/tmp/$EPUBCHECK.zip" "https://github.com/IDPF/epubcheck/releases/download/v${EPUBCHECK#*-}/$EPUBCHECK.zip"  && un  3.5s
 => [linux/arm/v7 4/5] ADD app /app/                                                                                                                      0.8s 
 => [linux/arm/v7 5/5] WORKDIR /app                                                                                                                       0.8s 
 => exporting to image                                                                                                                                   71.0s 
 => => exporting layers                                                                                                                                  12.9s 
 => => exporting manifest sha256:d2fff2848a35e762cc9ef98998eeb0d316b9c3a82501d05d91da131f2619afbc                                                         0.2s 
 => => exporting config sha256:ec9889862c1d4769050e3196ba960608ba2bc117f05b20ea6c04d1e511c7d7c0                                                           0.2s 
 => => exporting manifest sha256:6ba8e12de068be0e5e26664366c4a27258b7831ba6b12e0094084dbb9148f413                                                         0.3s 
 => => exporting config sha256:ad88ace37cac221107f5860232fa09850dd3a2bd8e0e4cbde9d6ad1559570e5d                                                           0.2s 
 => => exporting manifest sha256:e7c4d00c97855c5f71f5bc23eeab47b5ed8641f05f0034dfe2c49b2a46e0ccdf                                                         0.2s 
 => => exporting config sha256:ab6f86e0902970f5b7ca6f6ab1c3c06c9ee2ce539321cbf7ed230b08a1d187ff                                                           0.2s 
 => => exporting manifest list sha256:b44e25c3af81664e9de3805d73f29dd4a0e053b575140cec5fd820d349e5fba3                                                    0.2s 
 => => pushing layers                                                                                                                                    54.0s 
 => => pushing manifest for docker.io/atyasu/epubcheck:version-4.2.5                                                                                      2.5s
 => [auth] atyasu/epubcheck:pull,push token for registry-1.docker.io                                                                                      0.0s
 ⚓  ~/d/dockerfile-epubcheck  master  docker buildx build --platform linux/amd64,linux/arm64,linux/arm/v7 -t  atyasu/epubcheck:latest --push .
[+] Building 9.2s (22/22) FINISHED                                                                                                                             
 => [internal] load build definition from Dockerfile                                                                                                      0.4s
 => => transferring dockerfile: 32B                                                                                                                       0.0s
 => [internal] load .dockerignore                                                                                                                         0.5s
 => => transferring context: 2B                                                                                                                           0.0s
 => [linux/arm/v7 internal] load metadata for docker.io/library/alpine:3.13                                                                               1.3s
 => [linux/amd64 internal] load metadata for docker.io/library/alpine:3.13                                                                                1.4s
 => [linux/arm64 internal] load metadata for docker.io/library/alpine:3.13                                                                                1.4s
 => [internal] load build context                                                                                                                         0.3s
 => => transferring context: 89B                                                                                                                          0.0s
 => [linux/arm64 1/5] FROM docker.io/library/alpine:3.13@sha256:69e70a79f2d41ab5d637de98c1e0b055206ba40a8145e7bddb55ccc04e13cf8f                          0.7s
 => => resolve docker.io/library/alpine:3.13@sha256:69e70a79f2d41ab5d637de98c1e0b055206ba40a8145e7bddb55ccc04e13cf8f                                      0.6s
 => [linux/arm/v7 1/5] FROM docker.io/library/alpine:3.13@sha256:69e70a79f2d41ab5d637de98c1e0b055206ba40a8145e7bddb55ccc04e13cf8f                         0.8s
 => => resolve docker.io/library/alpine:3.13@sha256:69e70a79f2d41ab5d637de98c1e0b055206ba40a8145e7bddb55ccc04e13cf8f                                      0.8s
 => [linux/amd64 1/5] FROM docker.io/library/alpine:3.13@sha256:69e70a79f2d41ab5d637de98c1e0b055206ba40a8145e7bddb55ccc04e13cf8f                          0.9s
 => => resolve docker.io/library/alpine:3.13@sha256:69e70a79f2d41ab5d637de98c1e0b055206ba40a8145e7bddb55ccc04e13cf8f                                      0.8s
 => CACHED [linux/arm/v7 2/5] RUN apk add --update bash curl unzip openjdk7 &&     rm /var/cache/apk/*                                                    0.0s
 => CACHED [linux/arm/v7 3/5] RUN curl -L -o "/tmp/$EPUBCHECK.zip" "https://github.com/IDPF/epubcheck/releases/download/v${EPUBCHECK#*-}/$EPUBCHECK.zip"  0.0s
 => CACHED [linux/arm/v7 4/5] ADD app /app/                                                                                                               0.0s
 => CACHED [linux/arm/v7 5/5] WORKDIR /app                                                                                                                0.0s
 => CACHED [linux/amd64 2/5] RUN apk add --update bash curl unzip openjdk7 &&     rm /var/cache/apk/*                                                     0.0s
 => CACHED [linux/amd64 3/5] RUN curl -L -o "/tmp/$EPUBCHECK.zip" "https://github.com/IDPF/epubcheck/releases/download/v${EPUBCHECK#*-}/$EPUBCHECK.zip"   0.0s
 => CACHED [linux/amd64 4/5] ADD app /app/                                                                                                                0.0s
 => CACHED [linux/amd64 5/5] WORKDIR /app                                                                                                                 0.0s
 => CACHED [linux/arm64 2/5] RUN apk add --update bash curl unzip openjdk7 &&     rm /var/cache/apk/*                                                     0.0s
 => CACHED [linux/arm64 3/5] RUN curl -L -o "/tmp/$EPUBCHECK.zip" "https://github.com/IDPF/epubcheck/releases/download/v${EPUBCHECK#*-}/$EPUBCHECK.zip"   0.0s
 => CACHED [linux/arm64 4/5] ADD app /app/                                                                                                                0.0s
 => CACHED [linux/arm64 5/5] WORKDIR /app                                                                                                                 0.0s
 => exporting to image                                                                                                                                    6.1s
 => => exporting layers                                                                                                                                   0.0s
 => => exporting manifest sha256:d2fff2848a35e762cc9ef98998eeb0d316b9c3a82501d05d91da131f2619afbc                                                         0.2s
 => => exporting config sha256:ec9889862c1d4769050e3196ba960608ba2bc117f05b20ea6c04d1e511c7d7c0                                                           0.2s
 => => exporting manifest sha256:6ba8e12de068be0e5e26664366c4a27258b7831ba6b12e0094084dbb9148f413                                                         0.2s
 => => exporting config sha256:ad88ace37cac221107f5860232fa09850dd3a2bd8e0e4cbde9d6ad1559570e5d                                                           0.2s
 => => exporting manifest sha256:e7c4d00c97855c5f71f5bc23eeab47b5ed8641f05f0034dfe2c49b2a46e0ccdf                                                         0.2s
 => => exporting config sha256:ab6f86e0902970f5b7ca6f6ab1c3c06c9ee2ce539321cbf7ed230b08a1d187ff                                                           0.2s
 => => exporting manifest list sha256:b44e25c3af81664e9de3805d73f29dd4a0e053b575140cec5fd820d349e5fba3                                                    0.2s
 => => pushing layers                                                                                                                                     2.1s
 => => pushing manifest for docker.io/atyasu/epubcheck:latest                                                                                             2.1s
```
