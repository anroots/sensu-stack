FROM uchiwa/uchiwa
MAINTAINER Ando Roots <ando@sqroot.eu>

ENV HTTP_USER=hiro HTTP_PASS=nakamura SENSU_NAME="Default Sensu Datacenter" UCHIWA_HOST="0.0.0.0" UCHIWA_PORT=80 UCHIWA_REFRESH=5
EXPOSE 80

RUN wget https://github.com/jwilder/dockerize/releases/download/v0.2.0/dockerize-linux-amd64-v0.2.0.tar.gz && \
	tar -C /usr/local/bin -xzvf dockerize-linux-amd64-v0.2.0.tar.gz && \
	mkdir /etc/uchiwa

COPY config.tmpl /etc/uchiwa/
CMD dockerize -template /etc/uchiwa/config.tmpl:/etc/uchiwa/config.json \
	-wait tcp://$API_PORT_4567_TCP_ADDR:$API_PORT_4567_TCP_PORT \
	/go/bin/app -c /etc/uchiwa/config.json
