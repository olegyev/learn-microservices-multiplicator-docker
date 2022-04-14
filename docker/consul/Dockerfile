# This image is used to run a container-as-a-function that only should import
# default configuration (see ./consul-kv-docker.json -> "value" is Base64 encoded)
# to a Consul image (see consul-importer service within the ../docker-compose.yml).
FROM consul:1.7.2
COPY ./consul-kv-docker.json /usr/src/consul/
WORKDIR /usr/src/consul
ENV CONSUL_HTTP_ADDR=consul:8500
# Try to import default configuration to a running Consul container until success.
# Then stop executing container created by this image.
ENTRYPOINT until consul kv import '@consul-kv-docker.json'; do echo "Waiting for Consul"; sleep 2; done