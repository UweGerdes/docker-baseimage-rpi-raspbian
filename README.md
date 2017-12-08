# Docker uwegerdes/baseimage-rpi-stretch

A common base image for my Dockerfiles on Raspberry Pi 3 with Raspbian for my docker projects.

The base for this image is resin/rpi-raspbian:stretch but it might change in the future. For others architectures (arm64v8, arm32v6 and arm32v5) there are images too - replace it in the `Dockerfile` before build. Check `uname -m` for a hint - the standard Raspbian for Pi 3 is 32 bit.

## Installing Docker

Install Docker with:

```bash
curl -sSL https://get.docker.com | sh
sudo adduser pi docker
```

## Building with settings

If you want to build it with other settings load the Dockerfile in an empty directory, perhaps edit it to your needs.

If you have an apt-cacher-ng proxy server (try [uwegerdes/apt-cacher-ng](https://github.com/UweGerdes/docker-apt-cacher-ng)) you should check `hostname -i` or change it to an address available in your local network (not localhost) or omit the APT_PROXY line in the command above.

There is also a timezone parameter TZ. The terminal type is sent to the build context too so coloured output might be possible.

Build the image with (you might change/omit the build-args, mind the dot in the last line):

```bash
$ docker build -t uwegerdes/baseimage-rpi-stretch \
	--build-arg APT_PROXY="http://192.168.1.18:3142" \
	--build-arg TZ="Europe/Berlin" \
	--build-arg TERM="${TERM}" \
	.
```

## Usage

Use this baseimage in other `Dockerfile`s, they should work with this version or my [default baseimage](https://github.com/UweGerdes/docker-baseimage-rpi-stretch):

```
FROM uwegerdes/baseimage-rpi-stretch
```

## Settings

The build-args are saved and used by all images depending on this image.

