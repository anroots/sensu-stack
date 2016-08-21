# Changelog

All Notable changes to `anroots/sensu-*` will be documented in this file. The project follows [keepachangelog.com](http://keepachangelog.com) and [SemVer 2.0.0](http://semver.org).

## 0.3.0 - 2016-08-21

### Changed
- [#6] Upgrade Uchiwa from `0.15.0` to `1.17.1` and version-lock it (do not use `latest`)
- [#6] Upgrade Sensu from `0.22.0` to `0.25.7`

## 0.2.0 - 2016-03-19

### Deprecated
- [#4][] `anroots/sensu-client:nagios` is no longer maintained and will be removed in an upcoming release. Implementations that want to use Nagios plugins can create their own Dockerfile - [see example][link-nagios-dockerfile]

### Changed
- [#4][] Removed manual setting of `EMBEDDED_RUBY` to true: this is now done by default by Sensu
- [#4][] Upgrade Dockerize from `0.0.4` to `0.2.0`
- [#4][] Upgrade Sensu from `0.20.3` to `0.22.0`. Installation method changed from the official Sensu repository to downloading a .deb due to the repository having an outdated version of Sensu
- [#4][] Rename `TUTUM_` environment variables to `DOCKERCLOUD_`
- [#4][] Add `-wait` parameter to startup: wait for Redis, Api and Rabbitmq to become available before starting Sensu
- [#4][] Use `sensu-install` to install plugins to the `anroots/sensu-client:example` image

## 0.1.0 - 2015-12-19

Initial release

[link-nagios-dockerfile]: https://github.com/anroots/sensu-stack/blob/4d563d634ee98fabf95ac4981c66c1c8e78948e2/client/nagios/Dockerfile
[#4]: https://github.com/anroots/sensu-stack/pull/4
[#6]: https://github.com/anroots/sensu-stack/pull/6