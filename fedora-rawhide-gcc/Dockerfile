# Build Fedora image
FROM amd64/fedora:rawhide

# see https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/#/run
RUN dnf -y install \
  ca-certificates \
  ccache \
  curl \
  gcc-c++ \
  git \
  glm-devel \
  libwayland-egl \
  mesa-libGL-devel \
  ninja-build \
  SDL2-devel \
  spdlog-devel \
  wayland-devel && \
  dnf clean all

# Install cmake 3.15.4
RUN curl -s "https://cmake.org/files/v3.15/cmake-3.15.4-Linux-x86_64.tar.gz" | tar --strip-components=1 -xz -C /usr/local

# Use vcpkg (https://github.com/Microsoft/vcpkg.git) to compile the dependencies
# that do not have Ubuntu packages.
RUN mkdir /tools \
    && cd /tools \
    && git clone https://github.com/Microsoft/vcpkg.git --depth 1 \ 
    && cd vcpkg \
    && ./bootstrap-vcpkg.sh --useSystemBinaries \
    && VCPKG_FORCE_SYSTEM_BINARIES=1 ./vcpkg install --triplet x64-linux entt

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
