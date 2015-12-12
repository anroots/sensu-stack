# anroots/uchiwa

[![Docker Stars](https://img.shields.io/docker/stars/anroots/uchiwa.svg)](https://hub.docker.com/r/anroots/uchiwa)
[![Docker Pulls](https://img.shields.io/docker/pulls/anroots/uchiwa.svg)](https://hub.docker.com/r/anroots/uchiwa)
[![Image Layers](https://badge.imagelayers.io/anroots/uchiwa.svg)](https://imagelayers.io/?images=anroots/uchiwa)


## Usage

This container must be linked to Sensu API.

```bash
$ docker run --name=uchiwa --link sensu_api:api -p 3000:80 anroots/uchiwa
```

## Environment Variables

- `HTTP_USER` _string, default "hiro"_ - Username for HTTP login
- `HTTP_PASS` _string, default "nakamura"_ - Password for HTTP login 
- `SENSU_NAME` _string, default "Default Sensu Datacenter"_ - Name of the Sensu API (used as datacenter name)
- `UCHIWA_HOST` _string, default 0.0.0.0_ - Address on which Uchiwa will listen
- `UCHIWA_PORT` _int, default 80_ - Port on which Uchiwa will listen
- `UCHIWA_REFRESH` _int, default 5_ - Determines the interval to pull the Sensu APIs, in seconds
