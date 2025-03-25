# 🐳 Docker Setup for TuriCreate with Jupyter Notebook

## 📝 Overview
This Dockerfile creates a containerized environment for running TuriCreate with Jupyter Notebook, compatible with:
- macOS (including Apple Silicon M1/M2/M3 via Rosetta 2)
- Linux (x86_64)
- Windows (via WSL2)

## 🛠 Prerequisites
- Docker Desktop installed
- For Apple Silicon: Docker Desktop 4.12+ with Rosetta 2 enabled

## 🚀 Quick Start

### Build the Docker Image
```bash
docker build -t turicreate-jupyter .
