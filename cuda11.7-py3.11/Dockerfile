FROM nvidia/cuda:11.7.1-cudnn8-runtime-ubuntu22.04

WORKDIR /home

ARG DEBIAN_FRONTEND=noninteractive

ARG HTTP_PROXY

ENV TZ=Etc/CN
ENV HTTP_PROXY=${HTTP_PROXY}
ENV HTTPS_PROXY=${HTTP_PROXY}

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
    wget https://www.python.org/ftp/python/3.11.4/Python-3.11.4.tgz && \
    tar -xvf Python-3.11.4.tgz && \
    rm -rf Python-3.11.4.tgz && \
    cd Python-3.11.4 && \
    ./configure --enable-optimizations && \
    make install && \
    ln -s /usr/local/bin/python3 /usr/local/bin/python && \
    ln -s /usr/local/bin/pip3 /usr/local/bin/pip && \
    pip install --no-cache-dir pylint black ipdb soundfile && \
    cd / && \
    rm -rf /python

ENV HTTP_PROXY=""
ENV HTTPS_PROXY=""
