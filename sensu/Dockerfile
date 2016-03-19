FROM debian
MAINTAINER Ando Roots <ando@sqroot.eu>

# Install Sensu
RUN apt-get update && \
	apt-get install -y curl && \
	curl -O https://core.sensuapp.com/apt/pool/sensu/main/s/sensu/sensu_0.22.0-1_amd64.deb && \
	echo '00ad50b3b5ccaef23289bec35b89bea40525eea6 sensu_0.22.0-1_amd64.deb' >> sha1sums.txt && \
	sha1sum -c sha1sums.txt && \
	dpkg -i sensu_0.22.0-1_amd64.deb && \
	apt-get clean -y && \
	rm -rf /var/lib/apt/lists/* /etc/sensu/config.json.example sensu_0.22.0-1_amd64.deb sha1sums.txt

# Update PATH to include the embedded Ruby shipped with Sensu
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/sensu/embedded/bin

# Do not install Gem documentation when installing gems
RUN echo "install: --no-rdoc --no-ri" >> /etc/gemrc

# Dockerize is used to generate config files
# by replacing placeholders with values from the environment
COPY dockerize-0.2.0 /usr/local/bin/dockerize
