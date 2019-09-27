# Build Ubuntu image
FROM amd64/ubuntu:rolling

# see https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/#/run
RUN apt-get update && \
  apt-get install -y --no-install-recommends \
  g++ \
  build-essential \
  ca-certificates \
  ccache \
  cmake \
  libsdl2-dev \
  libglm-dev \
  libspdlog-dev \
  libwayland-dev \
  lsb-release \
  ninja-build

# Install cmake 3.15
RUN apt-get install -y --no-install-recommends wget && \
  wget https://github.com/Kitware/CMake/releases/download/v3.15.3/cmake-3.15.3-Linux-x86_64.sh && \
  chmod +x cmake-3.15.3-Linux-x86_64.sh && \
  apt remove -y cmake && \
  ./cmake-3.15.3-Linux-x86_64.sh --skip-license --prefix=/usr/local

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
