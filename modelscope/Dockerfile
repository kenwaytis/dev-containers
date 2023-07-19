FROM paidax/dev-containers:cuda11.3-py3.7

ARG DEBIAN_FRONTEND=noninteractive
ARG HTTP_PROXY

ENV TZ=Etc/CN
ENV HTTP_PROXY=${HTTP_PROXY}
ENV HTTPS_PROXY=${HTTP_PROXY}

RUN apt update && \
    apt install -y \
    tzdata \
    libsndfile1 && \
    apt clean && \
    rm -rf /var/lib/apt/lists/*

RUN pip install --no-cache-dir torch==1.11.0+cu113 torchvision==0.12.0+cu113 torchaudio==0.11.0 --extra-index-url https://download.pytorch.org/whl/cu113
RUN pip install --no-cache-dir  tensorflow-gpu==1.15
# Note: tensorflow-gpu==1.15 may cause some error while using cv model. May change it later

RUN pip install --no-cache-dir && \
    git clone https://github.com/r9y9/pysptk && \
    cd pysptk && \
    python setup.py develop && \
    cd .. && \
    rm -rf pysptk

RUN pip install --no-cache-dir  \
    modelscope \
    modelscope[multi-modal] && \
    pip install --no-cache-dir  modelscope[nlp] -f https://modelscope.oss-cn-beijing.aliyuncs.com/releases/repo.html && \
    pip install --no-cache-dir  modelscope[cv] -f https://modelscope.oss-cn-beijing.aliyuncs.com/releases/repo.html && \
    pip install --no-cache-dir  modelscope[audio] -f https://modelscope.oss-cn-beijing.aliyuncs.com/releases/repo.html && \
    pip uninstall mmcv && \
    pip install --no-cache-dir  -U openmim && \
    mim install mmcv-full

