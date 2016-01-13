FROM smebberson/alpine-consul-base:1.0.0
MAINTAINER Scott Mebberson <scott@scottmebberson.com>

ENV CZMQ_VERSION 3.0.2

# Install ZMQ
RUN apk add --update zeromq zeromq-dev build-base file && \
    apk add --update --repository http://dl-3.alpinelinux.org/alpine/edge/main/ libsodium && \
    cd /tmp && \
    wget -q -O czmq.tar.gz http://download.zeromq.org/czmq-${CZMQ_VERSION}.tar.gz && \
    tar zxf czmq.tar.gz && cd czmq-${CZMQ_VERSION} && \
    ./configure; make && make install && \
    apk del zeromq-dev build-base file && \
    rm -rf /var/cache/apk/* && \
    addgroup zmq && \
    adduser -D -s /bin/sh -G zmq zmq
