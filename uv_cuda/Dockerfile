ARG BASE_IMAGE
FROM ${BASE_IMAGE}

SHELL ["/bin/bash", "-c"]

RUN  apt-get update && apt-get install -y \
  locales \
  curl \
  wget \
  zip \
  unzip \
  git \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

RUN locale-gen ja_JP.UTF-8 && update-locale LANG=ja_JP.UTF-8

ENV LANG=ja_JP.UTF-8 \
  LANGUAGE=ja_JP:ja \
  LC_ALL=ja_JP.UTF-8

RUN curl -LsSf https://astral.sh/uv/install.sh | sh