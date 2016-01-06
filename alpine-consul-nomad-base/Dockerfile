FROM smebberson/alpine-consul-nomad
MAINTAINER Scott Mebberson <scott@scottmebberson.com>

# not needed with nomad client configuration
RUN rm /etc/consul/conf.d/nomad.json

# Add the files
ADD root /
