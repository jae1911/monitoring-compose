# monitoring-compose

Compose files for a monitoring system.

## Requirements

- Docker (19.03.0+)
- Docker Compose

## What does it contains

- [Grafana](https://grafana.com)
- [Prometheus](https://prometheus.io)
- [Uptime Kuma](https://github.com/louislam/uptime-kuma)
- [DMARC Metrics Exporter](https://github.com/jgosmann/dmarc-metrics-exporter/)
- [JSON Exporter](https://github.com/prometheus-community/json_exporter)

## HowTo

1. Create the environment file `.env` containing (of course replace the UID and GID with your own):

````
GF_SECURITY_ADMIN_PASSWORD=iamsecret
MY_UID=777
MY_GID=777
````

2. `docker compose up -d uptime-kuma` and set it up
3. Fill the uptime-kuma credentials in the `prometheus.yml` to be able to scrape data from it
4. `docker compose up -d` bring the rest of the services up

You can now go on your Grafana hostname and set it up.
