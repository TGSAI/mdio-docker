FROM mambaorg/micromamba:1-alpine

ARG release
ARG python=3.10
ARG dask

ENV MDIO_VERSION=$release
ENV PYTHON_VERSION=$python
ENV DASK_VERSION=$dask

RUN micromamba install -c conda-forge -n base \
    python=$PYTHON_VERSION \
    multidimio=$MDIO_VERSION \
    dask-core=$DASK_VERSION \
    distributed=$DASK_VERSION \
    gcsfs \
    s3fs \
    adlfs \
    zfpy \
    && micromamba clean --all --yes