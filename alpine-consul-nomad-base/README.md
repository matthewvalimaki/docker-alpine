# alpine-consul-nomad-base

An image that contains [Nomad] within a Docker container, bundled with Alpine Linux and [s6][s6]. This image is designed to work hand-in-hand with [smebberson/alpine-consul-nomad][alpineconsulnomad].

This image is designed to be extended from, with specific services added to it via Consul, along with appropriate health checks.

## Versions

- `1.0.0`, `latest` [(Dockerfile)](https://github.com/smebberson/docker-alpine/blob/master/alpine-consul-nomad-base/Dockerfile)

[See VERSIONS.md for image contents.](https://github.com/smebberson/docker-alpine/blob/master/alpine-consul-nomad-base/VERSIONS.md)

## Usage

To use this image include `FROM smebberson/alpine-consul-nomad-base` at the top of your `Dockerfile`, or simply `docker run --name consul-nomad-base --link "alpine-consul:consul-agent" smebberson/alpine-consul-nomad-base`.

It's very import to include a link to a container running a Consul agent (regardless if that Consul agent is running in server mode or not). The link within the container must be `consul-agent` which is used within `/etc/services.d/consul/run` to provide an IP that the Consul agent should join. Without this, the container will error and quit.

[s6]: http://www.skarnet.org/software/s6/
[consul]: https://www.consul.io/
[alpineconsulnomad]: https://registry.hub.docker.com/u/smebberson/alpine-consul-nomad/

## Customisation

This container comes setup as follows:

- [consul-template][consul-template] is provided and automatically started if templates are provided.

To use [consul-template][consul-template] simply add your templates to `root/etc/consul-template/templates/my-service/` and then make `consul-template` configuration aware of your templates by adding a configuration file in `root/etc/consul-template/conf.d/my-service` (use sub folders to make `VOLUME /etc/consul-template/templates/my-service` possible).

[consul-template]: https://github.com/hashicorp/consul-template