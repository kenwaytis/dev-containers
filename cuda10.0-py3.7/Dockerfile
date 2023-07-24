FROM ubuntu:18.04

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
    tzdata \
    wget \
    gnupg \
    gnupg1 \
    gnupg2 \
    git && \
    apt clean && \
    rm -rf /var/lib/apt/lists/*

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys A4B469963BF863CC && \
    wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-repo-ubuntu1804_10.0.130-1_amd64.deb && \
    dpkg -i cuda-repo-ubuntu1804_10.0.130-1_amd64.deb && \
    apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub && \
    apt-get update && \
    apt-get install -y cuda && \
    apt clean && \
    rm -rf /var/lib/apt/lists/*

RUN wget https://developer.nvidia.com/compute/machine-learning/cudnn/secure/7.6.5.32/Production/10.0_20191031/Ubuntu18_04-x64/libcudnn7_7.6.5.32-1%2Bcuda10.0_amd64.deb && \
    dpkg -i libcudnn7_7.6.5.32-1%2Bcuda10.0_amd64.deb

RUN mkdir /python && \
    cd /python && \
    wget https://www.python.org/ftp/python/3.7.17/Python-3.7.17.tgz && \
    tar -xvf Python-3.7.17.tgz && \
    rm -rf Python-3.7.17.tgz && \
    cd Python-3.7.17 && \
    ./configure --enable-optimizations && \
    make install && \
    ln -s /usr/local/bin/python3 /usr/local/bin/python && \
    ln -s /usr/local/bin/pip3 /usr/local/bin/pip && \
    pip install --no-cache-dir pylint black ipdb soundfile && \
    cd / && \
    rm -rf /python

ENV HTTP_PROXY=""
ENV HTTPS_PROXY=""

