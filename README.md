# Traefik with SSL Certificate in a Docker Swarm

Install the Docker Engine by following the official guide: https://docs.docker.com/engine/install/

Install the Docker Swarm by following the official guide: https://docs.docker.com/engine/swarm/swarm-tutorial/create-swarm/

Create a network for Traefik, config and secrets for storing the Traefik configuration, certificate and key on the Docker Swarm manager node before applying the configuration.

Create a network for Traefik using the command:

`docker network create -d overlay traefik-network`

Create a secret for storing the certificate using the command:

`docker secret create wildcard-heyvaldemar-net.crt /path/to/wildcard-heyvaldemar-net.crt`

Create a secret for storing the key using the command:

`docker secret create wildcard-heyvaldemar-net.key /path/to/wildcard-heyvaldemar-net.key`

Create a config for storing the Traefik configuration using the command:

`docker config create traefik-dynamic-configuration.yml /path/to/traefik-dynamic-configuration.yml`

Example of `traefik-dynamic-configuration.yml`:

```
tls:
  certificates:
    - certFile: /run/secrets/wildcard-heyvaldemar-net.crt
      keyFile: /run/secrets/wildcard-heyvaldemar-net.key
```

Deploy Traefik in a Docker Swarm using the command:

`docker stack deploy -c traefik-ssl-certificate-docker-swarm.yml traefik`
