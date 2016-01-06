FROM smebberson/alpine-consul-base
MAINTAINER Scott Mebberson <scott@scottmebberson.com>

ENV NOMAD_VERSION=0.2.3

# Download and install Nomad
# We are building it ourselves, because Alpine Linux doesn't use glibc
# Set XC_OS and XC_ARCH to avoid building for all platforms,
# see https://github.com/hashicorp/nomad/blob/master/scripts/build.sh
RUN export GOPATH=/go PATH=$PATH:/go/bin && \
    apk add --update go git gcc musl-dev make bash zip && \
    export XC_OS=$(go env GOOS) XC_ARCH=$(go env GOARCH) && \
    go get github.com/hashicorp/nomad && \
    cd $GOPATH/src/github.com/hashicorp/nomad && \
    git checkout -q --detach "v$NOMAD_VERSION" && \
    make bootstrap && make bin && \
    mv bin/nomad /bin && \
    rm -rf $GOPATH && \
    apk del go git gcc musl-dev make bash zip && \
    rm -rf /var/cache/apk/* && \
    addgroup nomad && \
    adduser -D -G nomad nomad && \
    mkdir -p /data/nomad && \
    chown -R nomad:nomad /data/nomad

# Add the files
ADD root /
