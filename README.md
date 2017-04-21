# docker_registry
Everything needed to setup a Docker Registry service


See also:
- https://docs.docker.com/registry/


It is assumed that
- LetsEncrypt is used for providing TLS certificates
- Access is restricted using basic authentication

All environment variables a required.

| Variable                 | Meaning                                   |
| ------------------------ | ----------------------------------------- |
| DOCKER_REGISTRY_HOSTNAME | Name of host registered with LetsEncrypt  |


| Variable              | Path to directory containing...                     |
| --------------------- | --------------------------------------------------- |
| DOCKER_REGISTRY_DATA  | Registry's data                                     |
| DOCKER_REGISTRY_CERTS | LetsEncrypt's TLS certificates                      |
| DOCKER_REGISTRY_AUTH  | Authorization information                           |

Note that LetsEncrypt's certificates are normally rooted at `/etc/letsencrypt`. This is the directory (or a symlink to it) that should be passed as `DOCKER_REGISTRY_CERTS`. The Docker Compose script will grab the correct certificates from this tree.


## Authentication
Example, on the host running the registry service, do this to create a file containing the password:

```bash
docker run --entrypoint htpasswd registry:2 -Bbn testuser testpassword > \
    auth/htpasswd
```

On the development machine, use `docker login <hostname>` before pushing and pulling images to authenticate with the registry.


## Using the image

Example script for starting the registry:

```bash
#!/usr/bin/env bash
prefix=/opt/docker_registry
export DOCKER_REGISTRY_DATA="$prefix/data"
export DOCKER_REGISTRY_CERTS="$prefix/letsencrypt"
export DOCKER_REGISTRY_AUTH="$prefix/auth"
export DOCKER_REGISTRY_HOSTNAME="my.registry.com"

docker-compose up
```

Here, it is assumed that the registry's data, LetsEncrypt certificates, and the directory containing the password file are rooted at `/opt/docker_registry`. You can change this to however you like to setup things.
