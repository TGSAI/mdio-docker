# This is a multi-stage build to minimize image size
# You can specify python version and linux distro as build args
# Stage 1: Build python venv + dependencies
# Stage 2: Install some system level developer tools
# Stage 3: Combine Stage 2 + Venv

ARG PYTHON_VERSION=3.11
ARG LINUX_DISTRO=slim-bullseye

FROM python:${PYTHON_VERSION}-${LINUX_DISTRO} as venv_base
# Stage 1: Create venv and install MDIO dependencies only

ENV PYTHONFAULTHANDLER=1 \
    PYTHONUNBUFFERED=1

ENV PIP_DISABLE_PIP_VERSION_CHECK=1 \
    PIP_NO_CACHE_DIR=1 \
    PIP_ROOT_USER_ACTION=ignore

RUN python -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
WORKDIR mdio-python

# Install all of MDIO dependencies
# 1. Get latest release from MDIO
# 2. Unpack it to WORKDIR
# 3. Install poetry and nox (dev tools)
# 4. Install all of MDIO dependencies with poetry
RUN apt-get update \
    && apt-get install -y --no-install-recommends  \
      curl \
    && rm -rf /var/lib/apt/lists/* \
    && curl -s https://api.github.com/repos/tgsai/mdio-python/releases/latest \
      | python -c 'import sys, json; print(json.load(sys.stdin)["tarball_url"])' \
      | xargs curl -LJ \
      | tar zx --strip=1 \
    && pip install \
      poetry  \
      nox \
      nox-poetry \
    && poetry config virtualenvs.create false \
    && poetry install \
      --no-root \
      --with dev \
      --with interactive \
      --all-extras \
      --no-ansi

FROM python:${PYTHON_VERSION}-${LINUX_DISTRO} as system_tools
# STAGE 2
# Install `git` and graphviz
# - git for pre-commit stuff
# - graphviz for debugging dask graphs

RUN apt-get update \
    && apt-get install -y --no-install-recommends  \
      git \
      graphviz \
    && rm -rf /var/lib/apt/lists/*

FROM system_tools
# STAGE 3
# Based on STAGE 2
# 1. Set Python interpreter
# 2. Add expected source dir to PYTHONPATH
# 3. Copy the venv from STAGE 1

ENV PYTHONFAULTHANDLER=1 \
    PYTHONUNBUFFERED=1 \
    PIP_NO_CACHE_DIR=1 \
    PATH="/opt/venv/bin:$PATH" \
    SHELL=/bin/bash \
    PYTHONPATH=/mdio-python/src

COPY --from=venv_base --chmod=777 /opt/venv /opt/venv

WORKDIR /mdio-python
