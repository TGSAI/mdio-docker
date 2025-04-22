FROM mambaorg/micromamba:1-bookworm-slim

LABEL org.opencontainers.image.source=https://github.com/tgsai/mdio-docker
LABEL org.opencontainers.image.description="MDIO image with no entrypoint for Dask"
LABEL org.opencontainers.image.documentation="https://mdio-python.readthedocs.io"
LABEL org.opencontainers.image.licenses="Apache-2.0"

ARG release
ARG python=3.13
ARG dask=2025.3.0
ARG distributed=2025.3.0
ARG lz4=4.3.3
ARG cloudpickle=3.1.1
ARG bokeh=3.7.2

# Cloud IO
ARG gcsfs=2025.3.2
ARG s3fs=2025.3.2
ARG adlfs=2024.12.0

ARG zarr=3.0.7

ENV PYTHON_VERSION=${python}
ENV MDIO_VERSION=${release}
ENV DASK_VERSION=${dask}
ENV DISTRIBUTED_VERSION=${distributed}
ENV LZ4_VERSION=${lz4}
ENV CLOUDPICKLE_VERSION=${cloudpickle}
ENV BOKEH_VERSION=${bokeh}
ENV GCSFS_VERSION=${gcsfs}
ENV S3FS_VERSION=${s3fs}
ENV ADLFS_VERSION=${adlfs}
ENV ZARR_VERSION=${zarr}

# Rename mambauser to mdiouser
# See README for explanation: https://github.com/mamba-org/micromamba-docker
ARG NEW_MAMBA_USER=mdiouser
ARG NEW_MAMBA_USER_ID=1000
ARG NEW_MAMBA_USER_GID=1000
USER root
RUN usermod "--login=${NEW_MAMBA_USER}" "--home=/home/${NEW_MAMBA_USER}" \
        --move-home "-u ${NEW_MAMBA_USER_ID}" "${MAMBA_USER}" && \
    groupmod "--new-name=${NEW_MAMBA_USER}" \
             "-g ${NEW_MAMBA_USER_GID}" "${MAMBA_USER}" && \
    # Update the expected value of MAMBA_USER for the
    # _entrypoint.sh consistency check.
    echo "${NEW_MAMBA_USER}" > "/etc/arg_mamba_user" && \
    :
ENV MAMBA_USER=$NEW_MAMBA_USER
USER $MAMBA_USER

# Install MDIO and extras
RUN micromamba install -c conda-forge -n base \
    python=$PYTHON_VERSION \
    multidimio=$MDIO_VERSION \
    dask-core=$DASK_VERSION \
    distributed=$DASK_VERSION \
    lz4=$LZ4_VERSION \
    cloudpickle=$CLOUDPICKLE_VERSION \
    bokeh=$BOKEH_VERSION \
    gcsfs=$GCSFS_VERSION \
    s3fs=$S3FS_VERSION \
    adlfs=$ADLFS_VERSION \
    zarr=$ZARR_VERSION \
    tini \
    && micromamba clean --all --yes \
    && find /opt/conda/ -type f,l -name '*.a' -delete \
    && find /opt/conda/ -type f,l -name '*.pyc' -delete \
    && find /opt/conda/ -type f,l -name '*.js.map' -delete \
    && find /opt/conda/lib/python*/site-packages/bokeh/server/static -type f,l -name '*.js' -not -name '*.min.js' -delete \
    && rm -rf /opt/conda/pkgs

# See README for why this entrypoint: https://github.com/mamba-org/micromamba-docker
# Tini is good: https://github.com/krallin/tini/issues/8#issuecomment-146135930
# No MDIO here because this is used to start worker/scheduler
ENTRYPOINT ["/usr/local/bin/_entrypoint.sh", "tini", "-g", "--"]
