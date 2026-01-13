FROM docker.1ms.run/nvidia/cuda:11.3.1-cudnn8-devel-ubuntu20.04

ENV TORCH_CUDA_ARCH_LIST="6.0 6.1 7.0 7.5 8.0 8.6+PTX"
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    wget \
    build-essential \
    g++ \
    gcc \
    libgl1-mesa-glx \
    libglib2.0-0 \
    openmpi-bin \
    openmpi-common \
    libopenmpi-dev \
    libgtk2.0-dev \
    git \
    ninja-build \
    && rm -rf /var/lib/apt/lists/*

ENV CONDA_DIR=/opt/conda
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-py38_4.12.0-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh
ENV PATH=$CONDA_DIR/bin:$PATH

RUN pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple


RUN pip install --no-cache-dir torch==1.9.1+cu111 torchvision==0.10.1+cu111 torchaudio==0.9.1 -f https://download.pytorch.org/whl/torch_stable.html

RUN pip install --no-cache-dir mmcv-full==1.4.0 -f https://download.openmmlab.com/mmcv/dist/cu111/torch1.9.0/index.html
RUN pip install --no-cache-dir mmdet==2.14.0 mmsegmentation==0.14.1


RUN pip install --no-cache-dir \
    "pillow<10.0.0" \
    yapf==0.33.0 \
    numpy==1.19.5 \
    pandas==1.4.4 \
    scikit-image==0.19.3 \
    matplotlib==3.5.2 \
    numba==0.48.0 \
    networkx==2.2 \
    trimesh==2.35.39 \
    plyfile==0.7.4 \
    lyft-dataset-sdk==0.0.8 \
    nuscenes-devkit==1.1.9 \
    setuptools==59.5.0 \
    einops fvcore seaborn iopath==0.1.9 timm==0.6.13 typing-extensions==4.5.0 pylint ipython==8.12 \
    protobuf==3.19.6 \
    werkzeug==2.0.3 \
    tensorboard==2.9.1 \
    markdown==3.3.7

ENV FORCE_CUDA="1"
RUN git clone https://gh-proxy.org/https://github.com/open-mmlab/mmdetection3d.git /mmdetection3d && \
    cd /mmdetection3d && \
    git checkout v0.17.1 && \
    python setup.py install

RUN python -m pip install 'git+https://gh-proxy.org/https://github.com/facebookresearch/detectron2.git@v0.6'