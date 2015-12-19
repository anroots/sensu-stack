FROM uchiwa/uchiwa
MAINTAINER Ando Roots <ando@sqroot.eu>

ENV HTTP_USER=hiro HTTP_PASS=nakamura SENSU_NAME="Default Sensu Datacenter" UCHIWA_HOST="0.0.0.0" UCHIWA_PORT=80 UCHIWA_REFRESH=5
EXPOSE 80

RUN wget https://github.com/jwilder/dockerize/releases/download/v0.0.4/dockerize-linux-amd64-v0.0.4.tar.gz && \
	tar -C /usr/local/bin -xzvf dockerize-linux-amd64-v0.0.4.tar.gz && \
	mkdir /etc/uchiwa

COPY config.tmpl /etc/uchiwa/
CMD dockerize -template /etc/uchiwa/config.tmpl:/etc/uchiwa/config.json /go/bin/app -c /etc/uchiwa/config.json
