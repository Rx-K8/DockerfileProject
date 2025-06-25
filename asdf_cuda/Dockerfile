ARG BASE_IMAGE
FROM ${BASE_IMAGE}

# 非対話モードの設定とタイムゾーン設定（これがないと途中で入力が求められてimageが作れない）
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Tokyo

SHELL ["/bin/bash", "-c"]

RUN { \
    echo 'export LANG=ja_JP.UTF-8'; \
    echo 'export PATH="${ASDF_DATA_DIR:-$HOME/.asdf}/shims:$PATH"'; \
    echo 'export PATH=${PATH}:${HOME}/.asdf'; \
    echo '. <(asdf completion bash)'; \
  } >> ${HOME}/.bashrc

RUN apt-get update && apt-get install -y \
    locales-all \
    language-pack-ja-base \
    curl \
    wget \
    zip \
    unzip \
    git \
    software-properties-common \
    build-essential \
    libbz2-dev \
    libdb-dev \
    libreadline-dev \
    libffi-dev \
    libgdbm-dev \
    liblzma-dev \
    libncursesw5-dev \
    libsqlite3-dev \
    libssl-dev \
    zlib1g-dev \
    uuid-dev \
    tk-dev \
    && add-apt-repository -y ppa:longsleep/golang-backports \
    && apt-get update \
    && apt-get install -y golang-go \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/asdf-vm/asdf.git --branch v0.18.0 ${HOME}/.asdf \
    && cd ${HOME}/.asdf \
    && make

RUN { \
    export PATH="${ASDF_DATA_DIR:-$HOME/.asdf}/shims:$PATH"; \
    export PATH=${PATH}:${HOME}/.asdf; \
    asdf plugin add python https://github.com/asdf-community/asdf-python.git; \
    asdf install python 3.11.13; \
    asdf set -u python 3.11.13; \
    asdf reshim python; \
    pip install -U pip; \
  }