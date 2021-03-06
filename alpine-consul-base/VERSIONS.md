# alpine-consul-base

This file contains all software versions, that correspond to a version of this image itself. Read more about the [alpine-consul-base image here][alpineconsulbase].

## Latest

Same as v2.0.0.

Usage: `smebberson/alpine-consul-base` or `smebberson/alpine-consul-base:latest`.

## v2.0.0

- [smebberson/alpine-consul: v1.1.0][alpineconsul]
- [consul-template: v0.14.0][consultemplate]
- **_breaking change_**: consul configuration directory is now located at `/etc/consul/conf.d/`

Usage: `smebberson/alpine-consul-base:2.0.0`.

## v1.1.0

- [smebberson/alpine-consul: v1.1.0][alpineconsul]

Usage: `smebberson/alpine-consul-base:1.1.0`.

## v1.0.0

- [smebberson/alpine-consul: v1.0.0][smebbersonalpineconsul100]

Usage: `smebberson/alpine-consul-base:1.0.0`.

[alpineconsulbase]: https://github.com/smebberson/docker-alpine/tree/master/alpine-consul-base
[alpineconsul]: https://github.com/smebberson/docker-alpine/tree/master/alpine-consul
[smebbersonalpineconsul100]: https://github.com/smebberson/docker-alpine/tree/df6ba86de86a325fd3544bedfbdf932829feb9d8/alpine-consul
[consultemplate]: https://github.com/hashicorp/consul-template
