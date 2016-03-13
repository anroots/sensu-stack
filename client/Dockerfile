FROM anroots/sensu

ENV DOCKERCLOUD_NODE_FQDN= DOCKERCLOUD_IP_ADDRESS= SUBSCRIPTIONS=

COPY conf.d /etc/sensu/conf.d/

CMD dockerize -template /etc/sensu/conf.d/rabbitmq.tmpl:/etc/sensu/conf.d/rabbitmq.json \
	/opt/sensu/bin/sensu-client -d /etc/sensu/conf.d