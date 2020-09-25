# [linuxserver/booksonic-air](https://github.com/linuxserver/docker-booksonic-air)

[![GitHub Stars](https://img.shields.io/github/stars/linuxserver/docker-booksonic-air.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&logo=github)](https://github.com/linuxserver/docker-booksonic-air)
[![GitHub Release](https://img.shields.io/github/release/linuxserver/docker-booksonic-air.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&logo=github)](https://github.com/linuxserver/docker-booksonic-air/releases)
[![GitHub Package Repository](https://img.shields.io/static/v1.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=linuxserver.io&message=GitHub%20Package&logo=github)](https://github.com/linuxserver/docker-booksonic-air/packages)
[![GitLab Container Registry](https://img.shields.io/static/v1.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=linuxserver.io&message=GitLab%20Registry&logo=gitlab)](https://gitlab.com/Linuxserver.io/docker-booksonic-air/container_registry)
[![MicroBadger Layers](https://img.shields.io/microbadger/layers/linuxserver/booksonic-air.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge)](https://microbadger.com/images/linuxserver/booksonic-air "Get your own version badge on microbadger.com")
[![Docker Pulls](https://img.shields.io/docker/pulls/linuxserver/booksonic-air.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=pulls&logo=docker)](https://hub.docker.com/r/linuxserver/booksonic-air)
[![Docker Stars](https://img.shields.io/docker/stars/linuxserver/booksonic-air.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=stars&logo=docker)](https://hub.docker.com/r/linuxserver/booksonic-air)
[![Jenkins Build](https://img.shields.io/jenkins/build?labelColor=555555&logoColor=ffffff&style=for-the-badge&jobUrl=https%3A%2F%2Fci.linuxserver.io%2Fjob%2FDocker-Pipeline-Builders%2Fjob%2Fdocker-booksonic-air%2Fjob%2Fmaster%2F&logo=jenkins)](https://ci.linuxserver.io/job/Docker-Pipeline-Builders/job/docker-booksonic-air/job/master/)
[![LSIO CI](https://img.shields.io/badge/dynamic/yaml?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=CI&query=CI&url=https%3A%2F%2Flsio-ci.ams3.digitaloceanspaces.com%2Flinuxserver%2Fbooksonic-air%2Flatest%2Fci-status.yml)](https://lsio-ci.ams3.digitaloceanspaces.com/linuxserver/booksonic-air/latest/index.html)

[Booksonic-air](http://booksonic.org) is a platform for accessing the audibooks you own wherever you are. At the moment the platform consists of
Booksonic Air - A server for streaming your audiobooks, successor to the original Booksonic server and based on Airsonic. Booksonic App - An DSub based Android app for connection to Booksonic-Air servers. .

## Supported Architectures

Our images support multiple architectures such as `x86-64`, `arm64` and `armhf`. We utilise the docker manifest for multi-platform awareness. More information is available from docker [here](https://github.com/docker/distribution/blob/master/docs/spec/manifest-v2-2.md#manifest-list) and our announcement [here](https://blog.linuxserver.io/2019/02/21/the-lsio-pipeline-project/).

Simply pulling `linuxserver/booksonic-air` should retrieve the correct image for your arch, but you can also pull specific arch images via tags.

The architectures supported by this image are:

| Architecture | Tag |
| :----: | --- |
| x86-64 | amd64-latest |
| arm64 | arm64v8-latest |
| armhf | arm32v7-latest |

## Version Tags

This image provides various versions that are available via tags. `latest` tag usually provides the latest stable version. Others are considered under development and caution must be exercised when using them.

| Tag | Description |
| :----: | --- |
| latest | Stable booksonic-air releases |

## Usage

Here are some example snippets to help you get started creating a container from this image.

### docker

```
docker create \
  --name=booksonic-air \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Europe/London \
  -e CONTEXT_PATH=url-base \
  -p 4040:4040 \
  -v </path/to/appdata/config>:/config \
  -v </path/to/audiobooks>:/audiobooks \
  -v </path/to/podcasts>:/podcasts \
  -v </path/to/othermedia>:/othermedia \
  --restart unless-stopped \
  linuxserver/booksonic-air
```


### docker-compose

Compatible with docker-compose v2 schemas.

```yaml
---
version: "2.1"
services:
  booksonic-air:
    image: linuxserver/booksonic-air
    container_name: booksonic-air
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
      - CONTEXT_PATH=url-base
    volumes:
      - </path/to/appdata/config>:/config
      - </path/to/audiobooks>:/audiobooks
      - </path/to/podcasts>:/podcasts
      - </path/to/othermedia>:/othermedia
    ports:
      - 4040:4040
    restart: unless-stopped
```

## Parameters

Docker images are configured using parameters passed at runtime (such as those above). These parameters are separated by a colon and indicate `<external>:<internal>` respectively. For example, `-p 8080:80` would expose port `80` from inside the container to be accessible from the host's IP on port `8080` outside the container.

### Ports (`-p`)

| Parameter | Function |
| :----: | --- |
| `4040` | Application WebUI |


### Environment Variables (`-e`)

| Env | Function |
| :----: | --- |
| `PUID=1000` | for UserID - see below for explanation |
| `PGID=1000` | for GroupID - see below for explanation |
| `TZ=Europe/London` | Specify a timezone to use EG Europe/London. |
| `CONTEXT_PATH=url-base` | Base url for use with reverse proxies etc. |

### Volume Mappings (`-v`)

| Volume | Function |
| :----: | --- |
| `/config` | Configuration files. |
| `/audiobooks` | Audiobooks. |
| `/podcasts` | Podcasts. |
| `/othermedia` | Other media. |



## Environment variables from files (Docker secrets)

You can set any environment variable from a file by using a special prepend `FILE__`.

As an example:

```
-e FILE__PASSWORD=/run/secrets/mysecretpassword
```

Will set the environment variable `PASSWORD` based on the contents of the `/run/secrets/mysecretpassword` file.

## Umask for running applications

For all of our images we provide the ability to override the default umask settings for services started within the containers using the optional `-e UMASK=022` setting.
Keep in mind umask is not chmod it subtracts from permissions based on it's value it does not add. Please read up [here](https://en.wikipedia.org/wiki/Umask) before asking for support.


## User / Group Identifiers

When using volumes (`-v` flags), permissions issues can arise between the host OS and the container, we avoid this issue by allowing you to specify the user `PUID` and group `PGID`.

Ensure any volume directories on the host are owned by the same user you specify and any permissions issues will vanish like magic.

In this instance `PUID=1000` and `PGID=1000`, to find yours use `id user` as below:

```
  $ id username
    uid=1000(dockeruser) gid=1000(dockergroup) groups=1000(dockergroup)
```

## Application Setup

Whilst this is a more up to date rebase of the original Booksonic server, upgrading in place is not supported and a fresh install has been recommended. Default user/pass is admin/admin

## Docker Mods
[![Docker Mods](https://img.shields.io/badge/dynamic/yaml?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=mods&query=%24.mods%5B%27booksonic-air%27%5D.mod_count&url=https%3A%2F%2Fraw.githubusercontent.com%2Flinuxserver%2Fdocker-mods%2Fmaster%2Fmod-list.yml)](https://mods.linuxserver.io/?mod=booksonic-air "view available mods for this container.")

We publish various [Docker Mods](https://github.com/linuxserver/docker-mods) to enable additional functionality within the containers. The list of Mods available for this image (if any) can be accessed via the dynamic badge above.


## Support Info

* Shell access whilst the container is running:
  * `docker exec -it booksonic-air /bin/bash`
* To monitor the logs of the container in realtime:
  * `docker logs -f booksonic-air`
* Container version number
  * `docker inspect -f '{{ index .Config.Labels "build_version" }}' booksonic-air`
* Image version number
  * `docker inspect -f '{{ index .Config.Labels "build_version" }}' linuxserver/booksonic-air`

## Versions

* **15.09.20:** - Initial Release.