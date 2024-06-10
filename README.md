# Python Docker Image for Nano Server

[![Docker Image CI](https://github.com/amitie10g/python-nanoserver/actions/workflows/docker-image.yml/badge.svg)](https://github.com/amitie10g/python-nanoserver/actions/workflows/docker-image.yml)

Windows Nano Server is an SKU designed for the cloud computing environment. But Nano Server is entirely different between the traditional Windows Server operating system. It is just a minimal subset of the existing Windows operating system, so many capabilities are missing.

This repository contains a Python docker image build script for Windows Nano Server.

[Docker Hub](https://hub.docker.com/r/amitie10g/python-nanoserver) | [GitHub Container Registry](https://github.com/amitie10g/python-nanoserver/pkgs/container/python-nanoserver)

## How to use

```powershell
docker pull amitie10g/python-nanoserver:latest
docker run -it amitie10g/python-nanoserver:latest
```

## How to build

You can build your Nano Server-based Python image with the below command.

```powershell
$EACH_PYTHON_VERSION='3.8.2'
$EACH_WIN_VERSION='2004'
$IMAGE_TAG="${EACH_PYTHON_VERSION}_${EACH_WIN_VERSION}"

$TARGET_PYTHON_PIP_VERSION='20.1.1'
$TARGET_PYTHON_GET_PIP_URL='https://github.com/pypa/get-pip/raw/d59197a3c169cef378a22428a3fa99d33e080a5d/get-pip.py'

docker build \
    -t python-nanoserver:$IMAGE_TAG \
    --build-arg WINDOWS_VERSION=$EACH_WIN_VERSION \
    --build-arg PYTHON_VERSION=$EACH_PYTHON_VERSION \
    --build-arg PYTHON_RELEASE=$EACH_PYTHON_VERSION \
    --build-arg PYTHON_PIP_VERSION=$TARGET_PYTHON_PIP_VERSION \
    --build-arg PYTHON_GET_PIP_URL=$TARGET_PYTHON_GET_PIP_URL \
    .
```

This image includes pip and virtualenv.

## Django Example

The `django_example` directory contains how to build a Nano Server-based Django application container.
