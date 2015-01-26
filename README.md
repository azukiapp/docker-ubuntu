[azukiapp/ubuntu](https://registry.hub.docker.com/u/azukiapp/ubuntu/)
================

Base docker image to run Ubuntu

- Ubuntu 14.04
- Git
- VIM

##azk
Example of using that image with the [azk](http://azk.io):

```
/**
 * Documentation: http://docs.azk.io/Azkfile.js
 */

// Adds the systems that shape your system
systems({
  "ubuntu": {
    // Dependent systems
    depends: [],
    // More images:  http://images.azk.io
    image: "azukiapp/ubuntu",
    // Steps to execute before running instances
    provision: [],
    workdir: "/azk/#{manifest.dir}",
    shell: "/bin/bash",
    command: "# command to run app",
    wait: {"retry": 20, "timeout": 1000},
    mounts: {
      '/azk/#{manifest.dir}': path("."),
    },
    scalable: {"default": 2},
    http: {
      // ubuntu.azk.dev
      domains: [ "#{system.name}.#{azk.default_domain}" ]
    },
    envs: {
      // set instances variables
      EXAMPLE: "value",
    },
  },
});
```

Building the base image
-----------------------

To create the base image `azukiapp/ubuntu`, execute the following command on the `ubuntu` folder:

```sh
$ docker build -t azukiapp/ubuntu .
```
