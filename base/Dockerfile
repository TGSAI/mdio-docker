FROM mambaorg/micromamba:2-debian12-slim

LABEL org.opencontainers.image.source=https://github.com/tgsai/mdio-docker
LABEL org.opencontainers.image.description="MDIO image with all functionality (cloud, distributed, zfp)."
LABEL org.opencontainers.image.documentation="https://mdio-python.readthedocs.io"
LABEL org.opencontainers.image.licenses="Apache-2.0"

ARG release
ARG python=3.13
ARG dask=2025.3.0

ENV MDIO_VERSION=$release
ENV PYTHON_VERSION=$python
ENV DASK_VERSION=$dask

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
    gcsfs \
    s3fs \
    adlfs \
    zfpy \
    tini \
    && micromamba clean --all --yes

# See README for why this entrypoint: https://github.com/mamba-org/micromamba-docker
# Tini is good: https://github.com/krallin/tini/issues/8#issuecomment-146135930
ENTRYPOINT ["/usr/local/bin/_entrypoint.sh", "tini", "-g", "--", "mdio"]
