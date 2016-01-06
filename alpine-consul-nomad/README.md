alpine-consul-nomad
====================

An image for using [Nomad], bundled with [Alpine Linux][alpinelinux] and [s6][s6] and [Consul][consul].

This image is perfect if you're looking to run [Nomad] within a Docker setup and wanting to benefit from [Consul][consul] for service registration and discovery. It's also very small clocking in at only ~62.65MB.

**_Yet another container for running Nomad?_**

Yes, but this one is built from [smebberson/alpine-consul-base][alpinebase] that contains [s6][s6] for process management, and [Consul][consul] for service registration and discovery. Small, fast and flexible.

_**Aren't you only supposed to run one process per container?**_

Hell no! The following are good examples of when multiple processes within one container might be necessary:

- Automatically updating [Nomad] settings when a down-stream application server restarts (and the IP changes).
- Running a logging daemon to centralize log management (i.e. [logentries][logentries], [loggly][loggly], [logstash][logstash]).
- When you need to run a script on application server crash (to tidy something up), as the standard [Docker container restart policies][drsp] won't provide this.

In all of these instances, there is one primary services and secondary support services. When the secondary support services fail, they should be automatically restarted. When the primary service fails, the container itself should restart.

## Versions

- `1.0.0` [(Dockerfile)](https://github.com/smebberson/docker-alpine/blob/master/alpine-consul-nomad/Dockerfile)

[See VERSIONS.md for image contents.](https://github.com/smebberson/docker-alpine/blob/master/alpine-consul-nomad/VERSIONS.md)

## Usage

To use this image include `FROM smebberson/alpine-consul-nomad` at the top of your `Dockerfile`, or simply `docker run -p 80:80 -p 443:443 --name nomad smebberson/alpine-consul-nomad`.

## Customisation

This container comes setup as follows:

- [s6][s6] will automatically start [Nomad] for you.
- If [Nomad] dies, so will the container.
- [Consul][consul] service registration, and health check of the [Nomad] service.

A service of name `nomad-server` is automatically setup within Consul, and a health check define to report availability of the service to Consul.

### Consul service registration

By default the file at `/etc/consul/conf.d/nomad.json` will register an `nomad-server` service, on port `4647` with [Consul][consul]. It also registers a 5s health check that reports on the availability of the service. If you'd like to configure perhaps more ports, or change the health check simply create a new file that meets the requirements of a [Consul service definition][consulservicedef] and add it (in your Dockerfile) to your image, replacing the already existing `nomad.json`.

[alpinelinux]: https://www.alpinelinux.org/
[consul]: https://consul.io/
[s6]: http://www.skarnet.org/software/s6/
[s6-svc]: http://skarnet.org/software/s6/s6-svc.html
[s6-built-statically]: https://github.com/smebberson/docker-ubuntu-base/blob/master/s6/s6-build
[logentries]: https://logentries.com/
[loggly]: https://www.loggly.com/
[logstash]: http://logstash.net/
[drsp]: https://docs.docker.com/reference/commandline/cli/#restart-policies
[Nomad]: https://www.nomadproject.io
[alpinebase]: https://registry.hub.docker.com/u/smebberson/alpine-base/
[s6]: http://www.skarnet.org/software/s6/
[dockerlogs]: https://docs.docker.com/reference/commandline/cli/#logs
[consulservicedef]: https://www.consul.io/docs/agent/services.html
