FROM paidax/dev-containers:cuda10.0-py3.7-v1.1

ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Etc/CN

RUN apt update && \
    apt install -y \
    tzdata \
    wget \
    git \
    libsndfile1 && \
    apt clean && \
    rm -rf /var/lib/apt/lists/*
RUN pip install --no-cache-dir torch==1.11.0+cu113 torchvision==0.12.0+cu113 torchaudio==0.11.0 --extra-index-url https://download.pytorch.org/whl/cu113 && \
    pip install --no-cache-dir  tensorflow-gpu==1.15.5
# Note: tensorflow-gpu==1.15 may cause some error while using cv model. May change it later

RUN pip install --no-cache-dir --upgrade Cython==0.29.35 && \
    pip install --no-cache-dir pysptk==0.1.21 --no-build-isolation && \
    pip install --no-cache-dir  \
    modelscope \
    modelscope[multi-modal] && \
    pip install --no-cache-dir  modelscope[nlp] -f https://modelscope.oss-cn-beijing.aliyuncs.com/releases/repo.html && \
    pip install --no-cache-dir  modelscope[cv] -f https://modelscope.oss-cn-beijing.aliyuncs.com/releases/repo.html && \
    pip install --no-cache-dir  modelscope[audio] -f https://modelscope.oss-cn-beijing.aliyuncs.com/releases/repo.html && \
    pip uninstall mmcv && \
    pip install --no-cache-dir  -U openmim && \
    mim install mmcv-full && \
    pip install --no-cache-dir "modelscope[audio,cv,nlp,multi-modal,science]" -f https://modelscope.oss-cn-beijing.aliyuncs.com/releases/repo.html
# Fix:fix while building wheels for pysptk, raise error because of cython's new version.