# Build Ubuntu image
FROM amd64/ubuntu:rolling

# see https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/#/run
RUN apt-get update && \
  apt-get install -y --no-install-recommends \
  build-essential
  ca-certificates \
  ccache \
  cmake \
  curl \
  git \
  g++ \
  libsdl2-dev \
  libglm-dev \
  libspdlog-dev \
  libwayland-dev \
  lsb-release \
  ninja-build

# Use vcpkg (https://github.com/Microsoft/vcpkg.git) to compile the dependencies
# that do not have Ubuntu packages.
RUN mkdir /tools
    && cd /tools \
    && git clone https://github.com/Microsoft/vcpkg.git -n \ 
    && cd vcpkg \
    && ./bootstrap-vcpkg.sh --useSystemBinaries
    && VCPKG_FORCE_SYSTEM_BINARIES=1 ./vcpkg install --triplet x64-linux entt

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
