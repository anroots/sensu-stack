FROM anroots/sensu

ENV API_USER=WqNu4awAaNoP API_PASS=abcXvzSqoSw7
EXPOSE 4567

COPY conf.d /etc/sensu/conf.d/

CMD dockerize -template /etc/sensu/conf.d/api.tmpl:/etc/sensu/conf.d/api.json \
	/opt/sensu/bin/sensu-api -d /etc/sensu/conf.d