# Build Fedora image
FROM amd64/fedora:31

# see https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/#/run
RUN dnf -y install \
  mingw64-gcc-c++ \
  ca-certificates \
  ccache \
  cmake \
  git \
  ninja-build

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
