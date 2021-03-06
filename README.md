[azukiapp/ubuntu](http://images.azk.io/#/ubuntu)
==================

Base docker image to run **Linux** applications in [`azk`](http://azk.io)

Versions (tags)
---

<versions>
- [`latest`, `trusty`, `14`, `14.04`](https://github.com/azukiapp/docker-ubuntu/blob/master/trusty/Dockerfile)
</versions>

Image content:
---

- Ubuntu 14.04
- Git
- VIM

### Usage with `azk`

Example of using this image with [azk](http://azk.io):

```js
/**
 * Documentation: http://docs.azk.io/Azkfile.js
 */
 
// Adds the systems that shape your system
systems({
  "my-app": {
    // Dependent systems
    depends: [], // postgres, mysql, mongodb ...
    // More images:  http://images.azk.io
    image: {"docker": "azukiapp/ubuntu"},
    // Steps to execute before running instances
    provision: [
      // "./script.sh",
    ],
    workdir: "/azk/#{manifest.dir}",
    shell: "/bin/bash",
    command: "# command to run app. i.g.: `./start.sh`",
    wait: {"retry": 20, "timeout": 1000},
    mounts: {
      '/azk/#{manifest.dir}': path("."),
    },
    scalable: {"default": 1},
    http: {
      domains: [ "#{system.name}.#{azk.default_domain}" ]
    },
    ports: {
      // http: "8080"
    },
    envs: {
      // set instances variables
      EXAMPLE: "value",
    },
  },
});
```

### Usage with `docker`

To create the image `azukiapp/ubuntu`, execute the following command on the docker-ubuntu folder:

```sh
$ docker build -t azukiapp/ubuntu .
```

To run the image and bind to port 8080:

```sh
$ docker run -it --rm --name my-app -p 8080:8080 -v "$PWD":/myapp -w /myapp azukiapp/ubuntu script.sh
```

Logs
---

```sh
# with azk
$ azk logs my-app

# with docker
$ docker logs <CONTAINER_ID>
```

## License

Azuki Dockerfiles distributed under the [Apache License][license].

[license]: ./LICENSE

