# grafana
Grafana stack deployment items

Prerequsites:

- Install Docker:
    [Install Docker Engine](https://docs.docker.com/engine/install/)
- Install 1password:
    [1password](https://developer.1password.com/docs/cli/get-started)

Create 1password Secret account, grant Read-Only access on Secrets vault. Then:
```bash
export OP_SERVICE_ACCOUNT_TOKEN=<token>
op user get --me
```

Detailed instructions:
- [Install Loki with Docker or Docker Compose](https://grafana.com/docs/loki/latest/setup/install/docker/)
- [Run Grafana Docker image](https://grafana.com/docs/grafana/latest/setup-grafana/installation/docker/)

Clone and verify commands also fix Loki `tmp` directory permissions:
```bash
cd /opt && git clone https://github.com/artyomtsybulkin/grafana
cd /opt/grafana/docker && op inject -i env.properties -o .env
docker compose -f docker-compose.yaml config
docker compose -f docker-compose.yaml create
useradd -u 10001 loki
chown -R loki:loki /var/lib/docker/volumes/loki-tmp/_data
```
If required, then change `/var/lib/docker/volumes` content before start
```bash
docker compose -f docker-compose.yaml start
```

Expect Web UI availability on: http://localhost:3000.
User `Admin` with password `admin`.