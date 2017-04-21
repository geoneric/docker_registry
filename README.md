# docker_registry
Everything needed to setup a Docker Registry service


It is assumed that
- LetsEncrypt is used for providing TLS certificates
- Access is restricted using basic authentication


| Variable              | Path to directory containing...                     |
| --------------------- | --------------------------------------------------- |
| DOCKER_REGISTRY_DATA  | Registry's data                                     |
| DOCKER_REGISTRY_CERTS | LetsEncrypt's TLS certificates                      |
| DOCKER_REGISTRY_AUTH  | Authorization information                           |


## Authentication
Example
```bash
docker run --entrypoint htpasswd registry:2 -Bbn testuser testpassword > \
    auth/htpasswd
```
