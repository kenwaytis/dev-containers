FROM nvidia/cuda:11.8.0-cudnn8-devel-ubuntu22.04

WORKDIR /home

ARG DEBIAN_FRONTEND=noninteractive
 
ENV TZ=Asia/Shanghai

RUN apt update && \
    apt install -y \
    build-essential \
    zlib1g-dev \
    libncurses5-dev \
    libgdbm-dev \
    libnss3-dev \
    libssl-dev \
    libreadline-dev \
    libffi-dev \
    libbz2-dev \
    liblzma-dev \
    libsqlite3-dev \
    tzdata \
    wget \
    git && \
    apt clean && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir /python && \
    cd /python && \
    wget https://www.python.org/ftp/python/3.10.13/Python-3.10.13.tgz && \
    tar -xvf Python-3.10.13.tgz && \
    rm -rf Python-3.10.13.tgz && \
    cd Python-3.10.13 && \
    ./configure --enable-optimizations && \
    make install && \
    ln -s /usr/local/bin/python3 /usr/local/bin/python && \
    ln -s /usr/local/bin/pip3 /usr/local/bin/pip && \
    pip install --no-cache-dir pylint black ipdb soundfile && \
    cd / && \
    rm -rf /python
