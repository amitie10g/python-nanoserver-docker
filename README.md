# Python Docker Image for Nano Server

[![Docker Image CI](https://github.com/amitie10g/python-nanoserver/actions/workflows/docker-image.yml/badge.svg)](https://github.com/amitie10g/python-nanoserver/actions/workflows/docker-image.yml)

Windows Nano Server is an SKU designed for the cloud computing environment. But Nano Server is entirely different between the traditional Windows Server operating system. It is just a minimal subset of the existing Windows operating system, so many capabilities are missing.

This repository contains a Python docker image build script and aaa GitHub Actions workflow for Windows Nano Server. For instance, only Python3 is supported.

[Docker Hub](https://hub.docker.com/r/amitie10g/python-nanoserver) | [GitHub Container Registry](https://github.com/amitie10g/python-nanoserver/pkgs/container/python-nanoserver)

## How to use

### From command line

```powershell
docker pull amitie10g/python-nanoserver:latest
docker run -it amitie10g/python-nanoserver:latest
```

### As base image

```dockerfile
FROM amitie10g/python-nanoserver

COPY / C:\\Users\\ContainerUser

USER ContainerAdministrator
RUN pip install <whatever you need>

USER ContainerUser
```

If you want to use this base image within GitHub Actions, consider to use the GitHub Container Registry:

``ghcr.io/amitie10g/python-nanoserver``

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

## Chocolatey?
Python3 (and Python2) can be downloaded using [Chocolatey](https://github.com/amitie10g/chocolatey-docker/pkgs/container/chocolatey) Windows Server-based image and copied to Nano Server and will work as well, but the resulting image will be slightly larger than this base image. Just replace everything in the build step with:

```dockerfile
FROM amitie10g/chocolatey

USER ContainerAdministrator
ARG PYTHON_VERSION=312
RUN choco install -y python$PYTHON_VERSION --params "/InstallDir:C:\Python"
```

This will install Python 3.12.4 and pip.

## Why I've forked this?
To provide up to date versions of Python3 (Jung Hyun Nam pushed the image until the version 3.9, three years ago). I've pushed from 3.7 to 3.13.

## License
Jung Hyun Nam haven't provided a license for his project. So, I released my fork (until permited, at least the GitHub Actions workflow) into the Public domain (the Unlicense).
