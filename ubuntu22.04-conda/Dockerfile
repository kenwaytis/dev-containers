FROM ubuntu:22.04
ARG DEBIAN_FRONTEND=nointeractive
ENV TZ=Etc/CN

RUN apt install -y \
    build-essential \
    tzdata \
    wget \
    git && \
    apt clean && \
    rm -rf /var/lib/apt/lists/*

RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
    bash Miniconda3-latest-Linux-x86_64.sh -b -p /opt/conda && \
    rm -rf Miniconda3-latest-Linux-x86_64.sh

ENV PATH="/opt/conda/bin:${path}"
