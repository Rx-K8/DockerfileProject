<!-- filepath: /home/keito_fukuoka2/stations/DockerfileProject/uv_cuda12-4/README.md -->
# uv_cuda12-4 Docker環境

CUDA 12.4.1環境にuvパッケージマネージャーがインストールされたDockerイメージです。

## 概要

このDockerfileは以下の環境を提供します：
- **ベースイメージ**: nvidia/cuda:12.4.1-cudnn-devel-ubuntu22.04
- **Python管理**: uv（高速なPythonパッケージマネージャー）
- **基本ツール**: curl, wget, zip, unzip, git

## 使い方

### 1. イメージのビルド

```bash
docker build -t uv-cuda12-4 .
```

**オプション解説:**
- `-t uv-cuda12-4`: イメージに `uv-cuda12-4` という名前（タグ）を付ける
- `.`: 現在のディレクトリにあるDockerfileを使用してビルド

### 2. コンテナの実行

```bash
# 基本的な実行
docker run -it --gpus all uv-cuda12-4 bash

# コンテナ名を指定して実行
docker run -it --gpus all --name my-uv-cuda-container uv-cuda12-4 bash

# ボリュームマウントありで実行
docker run -it --gpus all -v $(pwd):/workspace uv-cuda12-4 bash

# コンテナ名とボリュームマウントを同時に指定
docker run -it --gpus all --name my-uv-cuda-container -v $(pwd):/workspace uv-cuda12-4 bash
```

**オプション解説:**
- `-i`: インタラクティブモード（標準入力を開いたままにする）
- `-t`: 疑似TTYを割り当て（ターミナル環境を提供）
- `--gpus all`: ホストのすべてのGPUをコンテナで利用可能にする
- `--name my-uv-cuda-container`: コンテナに `my-uv-cuda-container` という名前を付ける
- `-v $(pwd):/workspace`: 現在のディレクトリを `/workspace` としてコンテナ内にマウント
- `uv-cuda12-4`: 使用するイメージ名
- `bash`: コンテナ起動時に実行するコマンド

### 3. uvの使用例

コンテナ内で以下のように使用できます：

```bash
# Pythonプロジェクトの初期化
uv init my-project
cd my-project

# Pythonのインストール
uv python install 3.11

# 依存関係のインストール
uv add numpy pandas torch

# スクリプトの実行
uv run python main.py
```

### 4. CUDA対応PyTorchのインストール

この環境（CUDA 12.4.1）でPyTorchをインストールする場合は、以下の方法を使用してください：

#### 特定バージョンの指定

```bash
# 特定バージョンを指定してインストール
uv add torch==2.6.0 torchvision==0.21.0 torchaudio==2.6.0 --index-url https://download.pytorch.org/whl/cu124
```

**CUDA対応版インストールのポイント:**
- CUDA 12.4環境ではCUDA 12.1対応版（`+cu121`）を使用
- `--index-url`でPyTorchの公式CUDAリポジトリを指定
- CUDA 12.1対応版はCUDA 12.4と互換性があります
- CPU版のみが必要な場合は通常の`uv add torch`でOK

## 注意事項

- GPUを使用する場合は `--gpus all` オプションが必要です
- uvは自動的にPython環境を管理するため、事前のPythonインストールは不要です
- 作業ディレクトリは適宜ボリュームマウントしてください
- CUDA対応PyTorchを使用する場合は必ず適切な`--index-url`を指定してください

## 参考リンク

- [uv公式ドキュメント](https://docs.astral.sh/uv/)
- [NVIDIA CUDA Docker Hub](https://hub.docker.com/r/nvidia/cuda)
- [PyTorch公式インストールガイド](https://pytorch.org/get-started/locally/)
- [PyTorch CUDA Wheels](https://download.pytorch.org/whl/torch/)