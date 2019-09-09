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

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
