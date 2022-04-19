ARG BASE_IMAGE=elixir:latest

FROM ${BASE_IMAGE} as dev-base

ENV DEBIAN_FRONTEND=noninteractive
WORKDIR /root
RUN --mount=type=cache,id=apt-dev,target=/var/cache/apt \
    apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    ca-certificates \
    ccache \
    wget \
    curl \
    git \
    gdb \
    ninja-build \
    rm -rf /var/lib/apt/lists/* && \
    cd /usr/local && \
    wget https://github.com/Kitware/CMake/releases/download/v3.22.0/cmake-3.22.0-linux-x86_64.sh && \
    bash cmake-3.22.0-linux-x86_64.sh --skip-license && \
    rm cmake-3.22.0-linux-x86_64.sh

FROM dev-base as devcontainer-llvm
ARG LLVM_VERSION=14
ARG RELEASE_DATE
ENV RELEASE_DATE=${RELEASE_DATE}
WORKDIR /workspace
RUN --mount=type=cache,id=apt-dev,target=/var/cache/apt \
    wget https://apt.llvm.org/llvm.sh &&  \
    chmod +x llvm.sh &&  \
    sudo ./llvm.sh ${LLVM_VERSION} all && \
    rm llvm.sh &&  \
    rm -rf /var/lib/apt/lists/*
