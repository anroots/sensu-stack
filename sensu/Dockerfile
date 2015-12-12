FROM debian
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
	rm -rf /var/lib/apt/lists/* /var/lib/cache/* /var/log/apt/* /tmp/* /var/tmp/* && \
	rm /etc/sensu/config.json.example && \
	echo "EMBEDDED_RUBY=true" > /etc/default/sensu

# Update PATH to include the embedded Ruby shipped with Sensu
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/sensu/embedded/bin

# Do not install Gem documentation when installing gems
RUN echo "install: --no-rdoc --no-ri" >> /etc/gemrc

# Dockerize is used to generate config files
# by replacing placeholders with values from the environment
COPY dockerize-0.0.4 /usr/local/bin/dockerize
