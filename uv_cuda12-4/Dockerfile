FROM nvidia/cuda:12.4.1-cudnn-devel-ubuntu22.04

SHELL ["/bin/bash", "-c"]

RUN { \
  echo 'export LANG=ja_JP.UTF-8'; \
  } >> ${HOME}/.bashrc

RUN  apt-get update && apt-get install -y \
    curl \
    wget \
    zip \
    unzip \
    git \
    && apt-get clean

RUN curl -LsSf https://astral.sh/uv/install.sh | sh