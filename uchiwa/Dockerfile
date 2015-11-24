FROM uchiwa/uchiwa
MAINTAINER Ando Roots <ando@sqroot.eu>

ENV HTTP_USER=admin HTTP_PASS=admin SENSU_NAME="Default Sensu Datacenter"
EXPOSE 80

RUN apt-get update && \
	apt-get install -y wget && \
	apt-get clean -y && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
	wget https://github.com/jwilder/dockerize/releases/download/v0.0.4/dockerize-linux-amd64-v0.0.4.tar.gz && \
	tar -C /usr/local/bin -xzvf dockerize-linux-amd64-v0.0.4.tar.gz && \
	mkdir /etc/uchiwa

COPY config.tmpl /etc/uchiwa/
CMD dockerize -template /etc/uchiwa/config.tmpl:/etc/uchiwa/config.json /go/bin/app -c /etc/uchiwa/config.json
