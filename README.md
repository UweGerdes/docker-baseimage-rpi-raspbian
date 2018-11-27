# Docker uwegerdes/baseimage-rpi-raspbian

A common base image for my Dockerfiles on Raspberry Pi 3 with Raspbian for my docker projects.

The base for this image is `resin/rpi-raspbian` (armv7l) but it might change in the future. For others architectures (arm64v8, arm32v6 and arm32v5) there are images too - replace it in the `Dockerfile` before build. Check `uname -m` for a hint - the standard Raspbian for Pi 3 is 32 bit.

## Installing Docker

Install Docker with:

```bash
curl -sSL https://get.docker.com | sh
sudo adduser pi docker
```

## Building with arguments

If you want to build it with other settings load the Dockerfile in an empty directory, perhaps edit it to your needs.

You might want to use tagged version of the `resin/rpi-raspbian` image with `BASEIMAGE_VERSION`. You should add the same version to tag the build. Default is `latest`.

If you have an apt-cacher-ng proxy server replace `[APT-PROXY-SERVER]` with your proxy cache hostname or ip. Otherwise omit that line.

There is also a timezone parameter `TZ`. The terminal type is sent to the build context too so coloured output might be possible.

The argument `TERM` helps scripts inside the container to find out information about the environment.

Build the image with (you might change/omit the build-args, mind the dot in the last line):

```bash
$ docker build -t uwegerdes/baseimage-rpi-raspbian:latest \
	--build-arg BASEIMAGE_VERSION="latest" \
	--build-arg APT_PROXY="http://[APT-PROXY-SERVER]:3142" --network=host \
	--build-arg TZ="Europe/Berlin" \
	--build-arg TERM="${TERM}" \
	.
```

## Usage

Use this baseimage in other `Dockerfile`s:

```
FROM uwegerdes/baseimage-rpi-raspbian
```

Or start a container with:

```bash
$ docker run -it \
	--name baseimage-rpi-raspbian \
	uwegerdes/baseimage-rpi-raspbian \
	bash
```

Restart it with:

```bash
$ docker start -ai baseimage-rpi-raspbian
```
