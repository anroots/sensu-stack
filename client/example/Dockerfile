FROM anroots/sensu-client

RUN apt-get update && \
	apt-get install -y bc build-essential && \
	gem install sensu-plugins-memory-checks sensu-plugins-cpu-checks sensu-plugins-disk-checks && \
	apt-get clean -y && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY conf.d /etc/sensu/conf.d/

CMD dockerize \
	-template /etc/sensu/conf.d/rabbitmq.tmpl:/etc/sensu/conf.d/rabbitmq.json \
	-template /etc/sensu/conf.d/client.tmpl:/etc/sensu/conf.d/client.json \
	-wait tcp://$RABBITMQ_PORT_5672_TCP_ADDR:5672 \
	/opt/sensu/bin/sensu-client -d /etc/sensu/conf.d