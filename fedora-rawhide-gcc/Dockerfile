# Build Fedora image
FROM amd64/fedora:rawhide

# see https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/#/run
RUN dnf -y install \
  ca-certificates \
  ccache \
  cmake \
  gcc-c++ \
  git \
  glew-devel \
  glm-devel \
  libwayland-egl \
  mesa-libGL-devel \
  ninja-build \
  SDL2-devel \
  spdlog-devel \
  wayland-devel

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app