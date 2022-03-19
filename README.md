# sml2mqtt
Docker image for [spacemanspiff2007/sml2mqtt](https://github.com/spacemanspiff2007/sml2mqtt)

This project allows to read values of one or more SML-compatible energy meters and publish them via MQTT.

## Usage
1. Create a docker compose configuration (file `docker-compose.yml`) for your environment.
1. Create a sml2mqtt configuration (file `config.yml`) for your environment.
1. Run `docker-compose up -d`

The directory `examples/` contains examples for the configuration files.

### Configuration
Please consult the [sml2mqtt documentation](https://github.com/spacemanspiff2007/sml2mqtt#configuration)
for details on the sml2mqtt configuration file `config.yml`.

It is recommended to set the log file to `/dev/stdout` so that the sml2mqtt log is redirected to the docker log:
```yaml
logging:
  level: INFO
  file: /dev/stdout
```

### Basic Commands
* Start in the background:
  ```shell
  $ docker-compose up -d
  ```
* Stop:
  ```shell
  $ docker-compose down
  ```
* Show the log:
  ```shell
  $ docker-compose logs
  ```
* Show the help:
  ```shell
  $ docker-compose run sml2mqtt sml2mqtt --help
  ```
* Show the structure of the first received SML message:
  ```shell
  $ docker-compose run sml2mqtt sml2mqtt --analyze
  ```
* Start a shell within the docker container:
  ```shell
  $ docker-compose run sml2mqtt sh
  ```

## Requirements
### Software
* Docker Compose

The Docker Compose [documentation](https://docs.docker.com/compose/install/)
contains a comprehensive guide explaining several install options. On recent debian-based systems, Docker Compose may be installed by calling
  ```sh
  $ sudo apt install docker-compose
  ```

## Build
The file `image/Dockerfile` contains everything to build a docker image for sml2mqtt.

The optional build argument `MODULE` may be used to customize the version of the sml2mqtt module to build. Examples:
* When you omit the build argument `MODULE`, the image is built from the latest commit of the `master` branch in the [sml2mqtt git repository](https://github.com/spacemanspiff2007/sml2mqtt).
* `MODULE=sml2mqtt` uses the latest release from pypi, the python package index.
* `MODULE=sml2mqtt=0.5` uses the sml2mqtt module from pypi in version `0.5 `.
* `MODULE=git+https://github.com/spacemanspiff2007/sml2mqtt.git@0.5` uses git tag `0.5` from the git repository.
* `MODULE=git+https://github.com/spacemanspiff2007/sml2mqtt.git@c981d1b` uses git commit `c981d1b4` from the git repository.

The optional build argument `BASE_IMAGE` may be used to customize the base docker image. Examples:
* When you omit the build argument `BASE_IMAGE`, the image is built upon the latest release of [alpine](https://alpinelinux.org/).
* `BASE_IMAGE=alpine:3.12` uses alpine 3.12 as base image.

## References
* This project is an integration of
  * [spacemanspiff2007/sml2mqtt](https://github.com/spacemanspiff2007/sml2mqtt)
  * [Docker](https://www.docker.com)
