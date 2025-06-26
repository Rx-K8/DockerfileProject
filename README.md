# 🐳 DockerfileProject

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Docker](https://img.shields.io/badge/Docker-Ready-blue.svg)](https://www.docker.com/)
[![CUDA](https://img.shields.io/badge/CUDA-Supported-green.svg)](https://developer.nvidia.com/cuda-zone)

> **NVIDIA CUDA 環境を使用した開発環境を Docker で構築するためのプロジェクト**
>
> 機械学習や GPU コンピューティングに必要な CUDA 環境を簡単にセットアップできます。

## 🚀 クイックスタート

### 1. リポジトリのクローン

```bash
git clone <このリポジトリのURL>
cd DockerfileProject
```

### 2. Docker イメージのビルド

**基本構文:**

```bash
docker build \
  --build-arg BASE_IMAGE=<ベースイメージ> \
  -t <タグ名> \
  -f <Dockerfileパス> <ビルドコンテキスト>
```

**使用例:**

```bash
# asdf 環境でのビルド
docker build \
  --build-arg BASE_IMAGE=nvidia/cuda:12.4.1-cudnn-devel-ubuntu22.04 \
  -t miyalab/cuda-asdf:12.4.1-cudnn-devel-ubuntu22.04 \
  -f asdf_cuda/Dockerfile .

# uv 環境でのビルド
docker build \
  --build-arg BASE_IMAGE=nvidia/cuda:12.4.1-cudnn-devel-ubuntu22.04 \
  -t miyalab/cuda-uv:12.4.1-cudnn-devel-ubuntu22.04 \
  -f uv_cuda/Dockerfile .
```

### 3. コンテナの起動

**基本構文:**

```bash
docker run -it --gpus all \
  --name <コンテナ名>
  -v <ホストパス>:<コンテナパス> \
  <イメージ名> <コマンド>
```

**使用例:**

```bash
docker run -it --gpus all \
  --name miyalab_container \
  -v $(pwd):/workspace \
  -v "${HOME}/.cache/huggingface":/root/.cache/huggingface \
  -w /workspace \
  miyalab/cuda-uv:12.4.1-cudnn-devel-ubuntu22.04 bash
```

## 📋 ベースイメージ一覧

| CUDA バージョン | Ubuntu | イメージ名                                    |
| :-------------- | :----- | :-------------------------------------------- |
| 12.4.1          | 22.04  | `nvidia/cuda:12.4.1-cudnn-devel-ubuntu22.04`  |
| 12.1.1          | 22.04  | `nvidia/cuda:12.1.1-cudnn8-devel-ubuntu22.04` |
| 11.8.0          | 22.04  | `nvidia/cuda:11.8.0-cudnn8-devel-ubuntu22.04` |

> 💡 **その他のバージョン**: [NVIDIA CUDA Docker Hub](https://hub.docker.com/r/nvidia/cuda) で利用可能な他のバージョンも使用できます。

## 参考リンク

- [Dockerfile を書くベストプラクティス](https://docs.docker.jp/develop/develop-images/dockerfile_best-practices.html)
- [NVIDIA CUDA Docker Hub](https://hub.docker.com/r/nvidia/cuda)
- [PyTorch 公式インストールガイド](https://pytorch.org/get-started/locally/)
- [asdf 公式ドキュメント](https://asdf-vm.com/guide/getting-started.html)
- [go 公式ドキュメント(Ubuntu)](https://go.dev/wiki/Ubuntu)
- [python のインストールに必要なライブラリ](https://www.python.jp/install/ubuntu/index.html)
