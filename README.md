# Sensu Stack [![Travis](https://img.shields.io/travis/anroots/sensu-stack.svg)](https://travis-ci.org/anroots/sensu-stack) [![License](https://img.shields.io/badge/license-MIT-brightgreen.svg)](https://github.com/anroots/sensu-stack/blob/master/LICENSE.md) [![Docker Pulls](https://img.shields.io/docker/pulls/anroots/sensu.svg)](https://hub.docker.com/r/anroots/sensu)

This is the [Sensu monitoring framework](https://sensuapp.org), running in Docker containers, with [Uchiwa](https://github.com/sensu/uchiwa) as the web-based frontend.

> Sensu is often described as the “monitoring router”. Essentially, Sensu takes the results of “check” scripts run across many systems, and if certain conditions are met, passes their information to one or more “handlers”. Checks are used, for example, to determine if a service like Apache is up or down. - [sensuapp.org](https://sensuapp.org/docs/latest/overview)

## Install

This project is opinionated towards [Docker Cloud](https://cloud.docker.com) deployment.

### Deploy to Docker Cloud

Press the button below to deploy this [stackfile](https://docs.docker.com/docker-cloud/feature-reference/stacks/) to your Docker Cloud account.

[![Deploy to Docker Cloud](https://files.cloud.docker.com/images/deploy-to-dockercloud.svg)](https://cloud.docker.com/stack/deploy)

### Deploy to Other Docker Capable Hosts

Use Docker Compose to deploy the stack to any Docker capable host.

- Place the contents of [docker-compose.yml](docker-compose.yml) into your server
- Run `docker-compose up`

## Usage

### Web Admin Panel

The default configuration maps the Uchiwa frontend to [http://localhost:3000](http://localhost:3000). Default credentials (*change those!*) are:

- **User**: `hiro`
- **Password**: `nakamura`

### Add Your Own Checks

Extend `anroots/sensu-client` and `anroots/sensu-server` to add your own configuration and checks. See Dockerfiles in [server/example](server/example) and [client/example](client/example) directories.

## Image Structure

- `debian`
  - `anroots/sensu` - base image for Sensu
    - `anroots/sensu-api`
    - `anroots/sensu-client` - barebones setup for Sensu client (no checks)
      - `anroots/sensu-client:example` - Sensu client which includes basic host-level checks (memory, CPU, disk usage)
        - `anroots/sensu-client:nagios` - Sensu client that includes a huge library of [nagios-plugins](https://github.com/harisekhon/nagios-plugins)
    - `anroots/sensu-server` - barebones setup for Sensu server (no checks)
      - `anroots/sensu-client:example` - Sensu server with one scheduled check
- `uchiwa/uchiwa`
  - `anroots/uchiwa`

## Change Log

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Security

If you discover any security related issues, please email ando@sqroot.eu instead of using the issue tracker.

## Credits

- [Ando Roots](http://sqroot.eu)
- [All Contributors](../../contributors)

## Licence

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.