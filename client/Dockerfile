FROM anroots/sensu

ENV TUTUM_NODE_FQDN= TUTUM_IP_ADDRESS= SUBSCRIPTIONS=

COPY conf.d /etc/sensu/conf.d/

CMD dockerize -template /etc/sensu/conf.d/rabbitmq.tmpl:/etc/sensu/conf.d/rabbitmq.json \
	/opt/sensu/bin/sensu-client -d /etc/sensu/conf.d