ARG BASE_IMAGE
FROM ${BASE_IMAGE}

SHELL ["/bin/bash", "-c"]

RUN { \
  echo 'export LANG=ja_JP.UTF-8'; \
  } >> ${HOME}/.bashrc

RUN  apt-get update && apt-get install -y \
    locales-all \
    language-pack-ja-base \
    curl \
    wget \
    zip \
    unzip \
    git \
    && apt-get clean

RUN curl -LsSf https://astral.sh/uv/install.sh | sh