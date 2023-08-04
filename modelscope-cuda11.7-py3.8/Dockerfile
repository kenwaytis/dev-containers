FROM paidax/dev-containers:cuda11.7-py3.8-dev-v1.2

ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Etc/CN

RUN apt update && \
    apt install -y \
    libsndfile1 && \
    apt clean && \
    rm -rf /var/lib/apt/lists/*
RUN pip install --no-cache-dir torch torchvision torchaudio \
        transformers==4.31.0 accelerate tiktoken einops

RUN pip install --no-cache-dir ninja && \
    git clone -b v1.0.8 https://github.com/Dao-AILab/flash-attention && \
    cd flash-attention && pip install . && \
    pip install --no-cache-dir csrc/layer_norm && \
    pip install --no-cache-dir csrc/rotary && \
    cd .. && \
    rm -rf flash-attention

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