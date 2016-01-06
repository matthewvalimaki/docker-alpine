FROM smebberson/alpine-consul-nomad
MAINTAINER Scott Mebberson <scott@scottmebberson.com>

# This file comes from base image and is not needed with Nomad client configuration
RUN rm /etc/consul/conf.d/nomad.json

# Add the files
ADD root /
