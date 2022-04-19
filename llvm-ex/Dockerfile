ARG BASE_IMAGE=elixir:latest

FROM ${BASE_IMAGE} as dev-base

ARG LLVM_VERSION=15
ARG RELEASE_DATE="unknown"
ENV DEBIAN_FRONTEND=noninteractive

WORKDIR /root
RUN --mount=type=cache,id=apt-dev,target=/var/cache/apt \
    apt-get update && apt-get install -y --no-install-recommends \
    lsb-release wget software-properties-common \
    build-essential \
    ca-certificates \
    ccache \
    curl \
    git \
    gdb \
    cmake \
    ninja-build && \
    wget https://apt.llvm.org/llvm.sh && \
    chmod +x llvm.sh &&  \
    ./llvm.sh ${LLVM_VERSION} all && \
    rm llvm.sh &&  \
    apt-get install -y libmlir-${LLVM_VERSION}-dev mlir-${LLVM_VERSION}-tools && \
    rm -rf /var/lib/apt/lists/* && \
    curl https://sh.rustup.rs -sSf | sh -s -- -y
