# Build Ubuntu image
FROM amd64/ubuntu:bionic

# see https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/#/run
RUN apt-get update && \
  apt-get install -y --no-install-recommends software-properties-common && \
  add-apt-repository ppa:git-core/ppa && \
  apt-get update && \
  apt-get install -y --no-install-recommends \
  build-essential \
  ca-certificates \
  ccache \
  clang-tidy \
  curl \
  git \
  g++ \
  libgl1-mesa-dev \
  libglm-dev \
  libsdl2-dev \
  libx11-dev \
  libwayland-dev \
  lsb-release \
  ninja-build \
  pkg-config

# Install cmake 3.15.4
RUN curl -s "https://cmake.org/files/v3.15/cmake-3.15.4-Linux-x86_64.tar.gz" | tar --strip-components=1 -xz -C /usr/local

# Use vcpkg (https://github.com/Microsoft/vcpkg.git) to compile the dependencies
# that do not have Ubuntu packages.
RUN mkdir /tools \
    && cd /tools \
    && git clone https://github.com/Microsoft/vcpkg.git --depth 1 \ 
    && cd vcpkg \
    && ./bootstrap-vcpkg.sh --useSystemBinaries \
    && VCPKG_FORCE_SYSTEM_BINARIES=1 ./vcpkg install --triplet x64-linux sdl2 spdlog entt spirv-cross spirv-tools cxxopts

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
