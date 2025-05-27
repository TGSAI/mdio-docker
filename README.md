# MDIO Docker Images

[![Docker Build](https://github.com/TGSAI/mdio-docker/actions/workflows/build.yml/badge.svg)](https://github.com/TGSAI/mdio-docker/actions/workflows/build.yml)

| Image                     | Description                                    | Versions                                                                                                                                                                                                                                             |
| ------------------------- | ---------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ghcr.io/tgsai/mdio`      | Base image to use MDIO with full functionality | [![][tgsai-mdio-latest] ![][tgsai-mdio-release] <br/> ![][tgsai-mdio-py313-release] <br/> ![][tgsai-mdio-py312-release] <br/> ![][tgsai-mdio-py311-release]](https://github.com/tgsai/mdio-docker/pkgs/container/mdio)                               |
| `ghcr.io/tgsai/mdio-dask` | Dask image to use MDIO in Dask Distributed     | [![][tgsai-mdio-dask-latest] ![][tgsai-mdio-dask-release] <br/> ![][tgsai-mdio-dask-py313-release] <br/> ![][tgsai-mdio-dask-py312-release] <br/> ![][tgsai-mdio-dask-py311-release]](https://github.com/tgsai/mdio-docker/pkgs/container/mdio-dask) |

[tgsai-mdio-latest]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio-latest-purple
[tgsai-mdio-release]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio-0.9.2-purple
[tgsai-mdio-py311-release]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio-0.9.2--py3.11-purple
[tgsai-mdio-py312-release]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio-0.9.2--py3.12-purple
[tgsai-mdio-py313-release]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio-0.9.2--py3.13-purple
[tgsai-mdio-dask-latest]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio--dask-latest-purple
[tgsai-mdio-dask-release]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio--dask-0.9.2-purple
[tgsai-mdio-dask-py311-release]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio--dask-0.9.2--py3.11-purple
[tgsai-mdio-dask-py312-release]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio--dask-0.9.2--py3.12-purple
[tgsai-mdio-dask-py313-release]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio--dask-0.9.2--py3.13-purple

## Example

Pull the container image like this:

```shell
docker pull ghcr.io/tgsai/mdio
```

Then you can execute things like this:

```shell
docker run --rm -v $HOST_PATH:$CONTAINER_PATH \
  mdio segy import \
    $CONTAINER_PATH/seismic.segy \
    $CONTAINER_PATH/seismic.mdio \
    -loc 181,185 \
    -names inline,crossline
```

where `$HOST_PATH` is a directory you want to mount in the container as
`$CONTAINER_PATH`. You can usually make these the same.

If you are in a UNIX based HPC environment, you may want to pass the user id
and group id. This will create files with the right permissions.

```shell
docker run --rm --user $(id -u):$(id -g) -v $HOST_PATH:$CONTAINER_PATH \
  mdio segy import \
    $CONTAINER_PATH/seismic.segy \
    $CONTAINER_PATH/seismic.mdio \
    -loc 181,185 \
    -names inline,crossline
```

## Developer Environment

The main [MDIO repository] has a `devcontainer.json` in it. Please use that
for developing MDIO. No custom container necessary.

If you want to know more about it please read [Development Containers].

They work with VSCode and PyCharm out of the box.

[MDIO Repository]: https://github.com/TGSAI/mdio-python
[Development Containers]: https://containers.dev/
