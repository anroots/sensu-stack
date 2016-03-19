# Changelog

All Notable changes to `anroots/sensu-*` will be documented in this file. The project follows [keepachangelog.com](http://keepachangelog.com) and [SemVer 2.0.0](http://semver.org).

## 0.2.0 - 2016-03-19

### Deprecated
- `anroots/sensu-client:nagios` is no longer maintained and will be removed in the upcoming release. Implementations that want to use Nagios plugins can create their own Dockerfile - [see example][link-nagios-dockerfile]

### Changed
- Removed manual setting of `EMBEDDED_RUBY` to true: this is now done by default by Sensu
- Upgrade Dockerize from 0.0.4 to 0.2.0
- Upgrade Sensu to 0.22.2
- Rename `TUTUM_` environment variables to `DOCKERCLOUD_`
- Add `-wait` parameter to startup: wait for Redis, Api and Rabbitmq to become available before starting Sensu

## 0.1.0 - 2015-12-19

Initial release

[link-nagios-dockerfile]: https://github.com/anroots/sensu-stack/blob/4d563d634ee98fabf95ac4981c66c1c8e78948e2/client/nagios/Dockerfile