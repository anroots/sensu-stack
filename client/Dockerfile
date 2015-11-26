FROM anroots/sensu

ENV TUTUM_NODE_FQDN= TUTUM_IP_ADDRESS= SUBSCRIPTIONS=

# Ruby and gem are installed because a lot of
# Sensu checks and handlers are written in Ruby and installable via Gem.
# For more, see https://github.com/sensu-plugins
RUN apt-get update && \
	apt-get install -y ruby2.1 ruby2.1-dev rubygems-integration build-essential && \
	apt-get clean -y && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
	ln -s /usr/bin/ruby2.1 /usr/bin/ruby && \
	ln -s /usr/bin/gem2.1 /usr/bin/gem

COPY conf.d /etc/sensu/conf.d/

CMD dockerize -template /etc/sensu/conf.d/rabbitmq.tmpl:/etc/sensu/conf.d/rabbitmq.json \
	/opt/sensu/bin/sensu-client -d /etc/sensu/conf.d