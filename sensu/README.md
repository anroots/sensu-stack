# anroots/sensu

[![Docker Stars](https://img.shields.io/docker/stars/anroots/sensu.svg)](https://hub.docker.com/r/anroots/sensu)
[![Docker Pulls](https://img.shields.io/docker/pulls/anroots/sensu.svg)](https://hub.docker.com/r/anroots/sensu)
[![Image Layers](https://badge.imagelayers.io/anroots/sensu.svg)](https://imagelayers.io/?images=anroots/sensu)

Base Docker image for `anroots/sensu-*` images.

Installs the [Sensu monitoring package](https://sensuapp.org) and [Dockerize](https://github.com/jwilder/dockerize) on a Debian distribution.

Dockerize is used to generate dynamic configuration for Sensu: parameters like RabbitMQ server IP can be read from environment variables during container execution.