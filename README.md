# OpenCompose

OpenCompose is an open standardised format for defining multi-container applications. Using a `.yaml` defined file, you create and start all your required services in one run command. This allows developers describe a set of services orchestrated via containers. OpenCompose is an alternative to [Docker Compose](https://github.com/docker/compose) with an open governance of the specification.

## Examples

An example of a complete application utilizing the specification is shown here:

```yaml
version: "0.2"

services:
    frontend:
        image: docker.io/surajd/frontend:v1
        ports:
            - 8080:8080
        type: external

    backend:
        image: docker.io/surajd/backend:v1
        ports:
            - 3000:3000
        environment:
            MONGODB_PASSWORD: pass
            MONGODB_USER: user
            MONGODB_DATABASE: db
            MONGODB_SERVER: mongodb:27017

    mongodb:
        image: tomaskral/mongodb-centos7
        ports:
            - 27017:27017
        volumes:
            - db-store:/var/lib/mongodb/data
        environment:
            MONGODB_PASSWORD: pass
            MONGODB_USER: user
            MONGODB_DATABASE: db
            MONGODB_ADMIN_PASSWORD: root

volumes:
    db-store:
        size: "2Gi"
        mode: ReadWriteOnce
```

## Specification

The current version of OpenCompose is __0.1__. 

We aim to keep the specification simple and understandable. The current version of the spec is provided in the [SPECIFICATION.asc](SPECIFICATION.asc) file.

## Proof-Of-Concept / CLI implementation

The Proof-of-Concept for the OpenCompose is based on a fork of [Kompose](https://github.com/kubernetes-incubator/kompose).

The code as well as instructions on how to use this tool can be found at [github.com/pradeepto/kompose/tree/opencompose](https://github.com/pradeepto/kompose/tree/opencompose).

[![asciicast](https://asciinema.org/a/7f7dw37n37m5kfn7v9uh1pn1w.png)](https://asciinema.org/a/7f7dw37n37m5kfn7v9uh1pn1w)

## Contributing

We are looking for ideas, proposals, comments and feedback on OpenCompose. Please use GitHub issues to file issues or proposals.

Also please refer the [CONTRIBUTING.asc](CONTRIBUTING.asc) document.

## Miscellaneous
The spec and more related documents in this repository are in [AsciiDoc](http://asciidoctor.org) format. It helps if you have some kind of tooling install that helps understands and renders asciidoc nicely.

* [Chrome Extension](https://github.com/asciidoctor/asciidoctor-chrome-extension)
