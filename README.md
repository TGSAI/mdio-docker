# MDIO Docker Images

[![Docker Build](https://github.com/TGSAI/mdio-docker/actions/workflows/build.yml/badge.svg)](https://github.com/TGSAI/mdio-docker/actions/workflows/build.yml)

| Image                | Description                                    | Versions                                                                                                                                                                    |
|----------------------|------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ghcr.io/tgsai/mdio` | Base image to use MDIO with full functionality | [![][tgsai-mdio-py38-release] ![][tgsai-mdio-release] ![][tgsai-mdio-latest] <br /> ![][tgsai-mdio-py39-release]](https://github.com/tgsai/mdio-docker/pkgs/container/mdio) |

[tgsai-mdio-latest]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio-latest-purple
[tgsai-mdio-release]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio-0.2.9-purple
[tgsai-mdio-py38-release]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio-0.2.9--py3.8-purple
[tgsai-mdio-py39-release]: https://img.shields.io/badge/ghcr.io%2Ftgsai%2Fmdio-0.2.9--py3.9-purple

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
