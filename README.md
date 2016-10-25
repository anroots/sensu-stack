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

You'll have to create your own Docker image and extend `anroots/sensu-client` and `anroots/sensu-server` to add your own configuration and checks. See Dockerfiles in [server/example](server/example) and [client/example](client/example) directories. Official documentation on checks can be read [here](https://sensuapp.org/docs/latest/checks).

```Dockerfile
FROM anroots/sensu-server:0.3.0

COPY conf.d /etc/sensu/conf.d
```

### Add Your Own Plugins

[sensu-plugins.io](http://sensu-plugins.io/) lists many Sensu plugins that can be used to perform different checks. To install a new plugin, create a new Docker image (extending `anroots/sensu-client`) and [install the plugins you want to use](https://github.com/anroots/sensu-stack/blob/master/client/example/Dockerfile#L6).

```Dockerfile
FROM anroots/sensu-client:0.3.0

# Install sensu plugins that perform system resource checks
RUN apt-get update && \
	apt-get install -y bc build-essential && \
	sensu-install --verbose -P memory-checks,cpu-checks,disk-checks && \
	apt-get purge -y build-essential && \
	apt-get autoremove -y && \
	apt-get clean -y && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
```

## Image Structure

- `debian`
  - `anroots/sensu` - base image for Sensu
    - `anroots/sensu-api`
    - `anroots/sensu-client` - barebones setup for Sensu client (no checks)
      - `anroots/sensu-client:example` - Sensu client which includes basic host-level checks (memory, CPU, disk usage)
    - `anroots/sensu-server` - barebones setup for Sensu server (no checks)
      - `anroots/sensu-client:example` - Sensu server with one scheduled check
- `uchiwa/uchiwa`
  - `anroots/uchiwa`

### Sending Alerts

This image does not come with built-in event handlers - you'll have to choose and configure one yourself. Documentation on handlers can be found [here](https://sensuapp.org/docs/latest/getting-started-with-handlers).

#### E-mail Handler

The following is an example on how to configure Sensu to send e-mails on failing checks.

First of all, we need to install a handler to the Sensu server. Extend `anroots/sensu-server` and install the e-mail handler:

```
# Dockerfile
FROM anroots/sensu-server:example
RUN sensu-install -p mailer
COPY mail.json /etc/sensu/conf.d/
```

Next, add the settings of the e-mail server to use:

```json
# mail.json
{
  "mailer": {
    "mail_from": "server@sensu.sqroot.eu",
    "mail_to": "ando@sqroot.eu",
    "smtp_address": "smtp.mailgun.org",
    "smtp_port": "587",
    "smtp_domain": "sensu.sqroot.eu",
    "smtp_username": "postmaster@sensu.sqroot.eu",
    "smtp_password": "<password>"
  }
}
```

Finally, tell Sensu that the handler exists. It can either be a default handler for all checks or specified on per-check basis.

```json
# Override handlers specified in server.tmpl
"handlers":{
  "default":{
    "type":"set",
    "handlers":[
      "mail"
    ]
  },
  "mail":{
    "type": "pipe",
    "command": "handler-mailer.rb"
  }
}
```

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
