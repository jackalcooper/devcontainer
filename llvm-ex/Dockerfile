ARG BASE_IMAGE=elixir:latest

FROM ${BASE_IMAGE} as dev-base

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
    apt-get install libmlir-15-dev mlir-15-tools && \
    rm llvm.sh &&  \
    rm -rf /var/lib/apt/lists/* && \
    curl https://sh.rustup.rs -sSf | sh -s -- -y
