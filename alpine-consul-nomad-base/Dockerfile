FROM smebberson/alpine-consul-nomad
MAINTAINER Scott Mebberson <scott@scottmebberson.com>

# Remove file from base image (not needed with Nomad client) and install client specific needs
RUN apk add --update curl && \
    rm -rf /var/cache/apk/* && \
    rm /etc/consul/conf.d/nomad.json

# Add the files
ADD root /
