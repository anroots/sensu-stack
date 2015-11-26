FROM debian:latest
MAINTAINER Ando Roots <ando@sqroot.eu>

ENV DEBIAN_FRONTEND noninteractive

# Install Sensu repo key
COPY sensu.key.gpg /tmp/

# Install Sensu
RUN apt-key add /tmp/sensu.key.gpg && \
	rm /tmp/sensu.key.gpg && \
	echo "deb     http://repos.sensuapp.org/apt sensu main" >> /etc/apt/sources.list.d/sensu.list && \
	apt-get update && \
	apt-get install -y sensu && \
	apt-get clean -y && \
	rm -rf /var/lib/apt/* /var/lib/cache/* /var/log/apt/* /tmp/* /var/tmp/* && \
	rm /etc/sensu/config.json.example

# Dockerize is used to generate config files
# by replacing placeholders with values from the environment
COPY dockerize-0.0.4 /usr/local/bin/dockerize
