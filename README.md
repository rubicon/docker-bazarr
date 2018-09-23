[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)](https://linuxserver.io)

The [LinuxServer.io](https://linuxserver.io) team brings you another container release featuring :-

 * regular and timely application updates
 * easy user mappings (PGID, PUID)
 * custom base image with s6 overlay
 * weekly base OS updates with common layers across the entire LinuxServer.io ecosystem to minimise space usage, down time and bandwidth
 * regular security updates

Find us at:
* [Discord](https://discord.gg/YWrKVTn) - realtime support / chat with the community and the team.
* [IRC](https://irc.linuxserver.io) - on freenode at `#linuxserver.io`. Our primary support channel is Discord.
* [Blog](https://blog.linuxserver.io) - all the things you can do with our containers including How-To guides, opinions and much more!
* [Podcast](https://podcast.linuxserver.io) - on hiatus. Coming back soon (late 2018).

# PSA: Changes are happening

From August 2018 onwards, Linuxserver are in the midst of switching to a new CI platform which will enable us to build and release multiple architectures under a single repo. To this end, existing images for `arm64` and `armhf` builds are being deprecated. They are replaced by a manifest file in each container which automatically pulls the correct image for your architecture. You'll also be able to pull based on a specific architecture tag.

TLDR: Multi-arch support is changing from multiple repos to one repo per container image.

# [linuxserver/bazarr](https://github.com/linuxserver/docker-bazarr)
[![](https://images.microbadger.com/badges/version/linuxserver/bazarr.svg)](https://microbadger.com/images/linuxserver/bazarr "Get your own version badge on microbadger.com")
[![](https://images.microbadger.com/badges/image/linuxserver/bazarr.svg)](https://microbadger.com/images/linuxserver/bazarr "Get your own version badge on microbadger.com")
![Docker Pulls](https://img.shields.io/docker/pulls/linuxserver/bazarr.svg)
![Docker Stars](https://img.shields.io/docker/stars/linuxserver/bazarr.svg)

[Bazarr](https://github.com/morpheus65535/bazarr) is a companion application to Sonarr and Radarr. It can manage and download subtitles based on your requirements. You define your preferences by TV show or movie and Bazarr takes care of everything for you.

[![bazarr](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/bazarr.png)](https://github.com/morpheus65535/bazarr)

## Supported Architectures

Our images support multiple architectures such as `X86-64`, `arm64` and `armhf`. We utilise the docker manifest for multi-platform awareness. More information is available from docker [here](https://github.com/docker/distribution/blob/master/docs/spec/manifest-v2-2.md#manifest-list). 

The architectures supported by this image are:

| Architecture | Tag |
| :----: | --- |
| X86-64 | amd64-latest |
| arm64 | arm64v8-latest |
| armhf | arm32v6-latest |

## Usage

Here are some example snippets to help you get started creating a container.

### docker

```
docker create \
  --name=bazarr \
  -e PUID=1001 \
  -e PGID=1001 \
  -e TZ=Europe/London \
  -p 6767:6767 \
  -v </path/to/bazarr/config>:/config \
  -v </path/to/movies>:/movies \
  -v </path/to/tv:/tv \
  linuxserver/bazarr
```


### docker-compose

Compatible with docker-compose v2 schemas.

```
---
version: "2"
services:
  bazarr:
    image: linuxserver/bazarr
    container_name: bazarr
    environment:
      - PUID=1001
      - PGID=1001
      - TZ=Europe/London
    volumes:
      - </path/to/bazarr/config>:/config
      - </path/to/movies>:/movies
      - </path/to/tv:/tv
    ports:
      - 6767:6767
    mem_limit: 4096m
    restart: unless-stopped
```

## Parameters

Container images are configured using parameters passed at runtime (such as those above). These parameters are separated by a colon and indicate `<external>:<internal>` respectively. For example, `-p 8080:80` would expose port `80` from inside the container to be accessible from the host's IP on port `8080` outside the container.

| Parameter | Function |
| :----: | --- |
| `-p 6767` | Allows HTTP access to the internal webserver. |
| `-e PUID=1001` | for UserID - see below for explanation |
| `-e PGID=1001` | for GroupID - see below for explanation |
| `-e TZ=Europe/London` | Specify a timezone to use EG Europe/London |
| `-v /config` | Bazarr data |
| `-v /movies` | Location of your movies |
| `-v /tv` | Location of your TV Shows |

## User / Group Identifiers

When using volumes (`-v` flags) permissions issues can arise between the host OS and the container, we avoid this issue by allowing you to specify the user `PUID` and group `PGID`.

Ensure any volume directories on the host are owned by the same user you specify and any permissions issues will vanish like magic.

In this instance `PUID=1001` and `PGID=1001`, to find yours use `id user` as below:

```
  $ id username
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

&nbsp;
## Application Setup

- Once running the URL will be `http://<host-ip>:6767`.
- You must complete all the setup parameters in the webui before you can save the config.



## Support Info

* Shell access whilst the container is running: `docker exec -it bazarr /bin/bash`
* To monitor the logs of the container in realtime: `docker logs -f bazarr`
* container version number 
  * `docker inspect -f '{{ index .Config.Labels "build_version" }}' bazarr`
* image version number
  * `docker inspect -f '{{ index .Config.Labels "build_version" }}' linuxserver/bazarr`

## Versions

* **11.09.18:** - Initial release.