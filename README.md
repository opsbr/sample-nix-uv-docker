# Sample: Nix + uv + Docker

This repository shows a minimal FastAPI workflow with:

- `nix` for reproducible system tooling
- `uv` for Python dependency management
- `docker` image builds from the Nix flake

## Prerequisites

- WSL (Ubuntu 24.04)
- Docker Desktop with WSL integration enabled
- Nix

Install Nix via [Nix Installer](https://github.com/NixOS/nix-installer):

```sh
curl -sSfL https://artifacts.nixos.org/nix-installer | sh -s -- install
```

## Quickstart

### 1. Clone

```sh
git clone https://github.com/opsbr/sample-nix-uv-docker.git
cd sample-nix-uv-docker
```

### 2. Enter development shell

```sh
nix develop
```

After entering the shell, the Python virtual environment is active and `uv` is available.

### 3. Run the app locally

```sh
fastapi dev
```

Open `http://127.0.0.1:8000` and you should see:

```json
{"message":"Hello World"}
```

## Build and run with Docker

Build the image via Nix:

```sh
nix build
```

This uses `flake.lock` and `uv.lock` to pin both system and Python dependencies (via [`uv2nix`](https://pyproject-nix.github.io/uv2nix/)).

Load and run the image:

```sh
docker load < result
docker run --rm -it -p 8000:8000 my-app:latest
```
