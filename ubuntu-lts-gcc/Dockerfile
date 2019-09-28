# Build Ubuntu image
FROM amd64/ubuntu:bionic

# see https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/#/run
RUN apt-get update && \
  apt-get install -y --no-install-recommends \
  git \
  g++ \
  build-essential \
  ca-certificates \
  ccache \
  cmake \
  libgl1-mesa-dev \
  libwayland-dev \
  lsb-release \
  ninja-build \
  pkg-config

# dependencies will be provided by hunter via cmake

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
