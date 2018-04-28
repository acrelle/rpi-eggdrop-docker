# rpi-eggdrop

Uses a raspberry pi compatible base image, forked from https://hub.docker.com/r/library/eggdrop/

## Source 

https://github.com/acrelle/rpi-eggdrop-docker

## Build

[![](https://images.microbadger.com/badges/version/acrelle/rpi-eggdrop.svg)](https://microbadger.com/images/acrelle/rpi-eggdrop "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/acrelle/rpi-eggdrop.svg)](https://microbadger.com/images/acrelle/rpi-eggdrop "Get your own image badge on microbadger.com")[![Build Status](https://jenkins.relle.uk/buildStatus/icon?job=rpi-eggdrop)](https://jenkins.relle.uk/job/rpi-eggdrop)

https://hub.docker.com/r/acrelle/rpi-eggdrop/

## Usage

Follow above linked instructions to run.

Change 3333 to the port that incoming telnet is exposed on (if enabled).

```
docker run -dt  -v eggdrop_data:/home/eggdrop/eggdrop/data \
-p 3333:3333 acrelle/rpi-eggdrop:latest eggdrop.conf
```

### Docker Compose

The below example is specific to my configuration:

~~~yaml
version: "2"
services:
  eggdrop:
    build: .
    image: acrelle/rpi-eggdrop
    container_name: eggdrop
    restart: always
    volumes:
     - ~/appdata/eggdrop/eggdrop_data:/home/eggdrop/eggdrop/data
     - ~/appdata/eggdrop/eggdrop_scripts:/home/eggdrop/eggdrop/scripts
     - ~/appdata/eggdrop/eggdrop_data/mel:/home/eggdrop/eggdrop/mel
     - ~/appdata/eggdrop/eggdrop_data/save:/home/eggdrop/eggdrop/save
    environment:
     - PUID=1001
     - PGID=100
    ports:
     - 3333:3333
    tty: true
    command: ["^W^.conf"]
~~~
