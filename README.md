# MDIO Docker Images


The default MDIO releases (`latest` and `0.3.1` tags) are on Python 3.11. We provide 3.10, 3.9, and 3.8 containers as well.

[![Docker Build](https://github.com/TGSAI/mdio-docker/actions/workflows/build.yml/badge.svg)](https://github.com/TGSAI/mdio-docker/actions/workflows/build.yml)

| Image                     | Description                                    | Versions                                                                                                                                                                                                                                |
|---------------------------|------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ghcr.io/tgsai/mdio`      | Base image to use MDIO with full functionality | [![][tgsai-mdio-latest] ![][tgsai-mdio-release] <br /> ![][tgsai-mdio-py310-release] ![][tgsai-mdio-py39-release] ![][tgsai-mdio-py38-release] ](https://github.com/tgsai/mdio-docker/pkgs/container/mdio-dask)                         |
| `ghcr.io/tgsai/mdio-dask` | Dask image to use MDIO in Dask Distributed     | [![][tgsai-mdio-dask-latest] ![][tgsai-mdio-dask-release] <br /> ![][tgsai-mdio-dask-py310-release] ![][tgsai-mdio-dask-py39-release] ![][tgsai-mdio-dask-py38-release]](https://github.com/tgsai/mdio-docker/pkgs/container/mdio-dask) |

[tgsai-mdio-latest]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio-latest-purple
[tgsai-mdio-release]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio-0.3.1-purple
[tgsai-mdio-py38-release]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio-0.3.1--py3.8-purple
[tgsai-mdio-py39-release]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio-0.3.1--py3.9-purple
[tgsai-mdio-py310-release]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio-0.3.1--py3.10-purple

[tgsai-mdio-dask-latest]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio--dask-latest-purple
[tgsai-mdio-dask-release]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio--dask-0.3.1-purple
[tgsai-mdio-dask-py38-release]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio--dask-0.3.1--py3.8-purple
[tgsai-mdio-dask-py39-release]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio--dask-0.3.1--py3.9-purple
[tgsai-mdio-dask-py310-release]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio--dask-0.3.1--py3.10-purple

## Example

Pull the container image like this:

```shell
docker pull ghcr.io/tgsai/mdio
```

Then you can execute things like this:
```shell
docker run --rm -v $HOST_PATH:$CONTAINER_PATH \
  mdio segy import \
    -i $CONTAINER_PATH/seismic.segy \
    -o $CONTAINER_PATH/seismic.mdio \
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
    -i $CONTAINER_PATH/seismic.segy \
    -o $CONTAINER_PATH/seismic.mdio \
    -loc 181,185 \
    -names inline,crossline
```

## Developer Environment

TBA
