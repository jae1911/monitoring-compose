# monitoring-compose

Compose files for a monitoring system.

## Requirements

- Docker (19.03.0+)
- Docker Compose

## What does it contains

- Grafana
- Prometheus
- Uptime Kuma
- node_exporter (optional, machine stats)

## Notes

- This deployment assumes you use [Traefik](https://traefik.io/traefik/) as a reverse proxy
- This deployment does not uses SMTP (see `GF_SMTP_*` configuration keys for that)
- Some part of the configuration related to OAUTH were omitted to simplify this repo (see `GF_AUTH_GENERIC_OAUTH_*` configuration keys for that)
- Network configuration of the Compose file was omitted
- The real deployment uses a different drive for secrets (including the `prometheus.yml`) but was simplified for this repo

## Volumes

This deployment uses multiple volumes:

- `.` - Current directory, pulled from the configuration repository
- `/mnt/store` - A dedicated storage area

## HowTo

1. Change paths of `/mnt/secrets` and `/mnt/store` to your desired ones.
2. Create the environment file `.env` containing:

````
grafanahostname=grafana.something.tld
kumahostname=kuma.something.tld

GF_SECURITY_ADMIN_PASSWORD=iamsecret
POSTGRES_DB=grafana
POSTGRES_USER=grafana
POSTGRES_PASSWORD=evenmoresecret
````

3. `docker compose up -d uptime-kuma` and set it up
4. Fill the uptime-kuma credentials in the `prometheus.yml` to be able to scrape data from it
5. `docker compose up -d` bring the rest of the services up

You can now go on your Grafana hostname and set it up.

## Additional resources

- [Uptime Kuma sample Grafana dashboard](https://github.com/louislam/uptime-kuma/tree/unofficial/grafana-dashboard)
- [node_exporter sample Grafana dashboard](https://grafana.com/grafana/dashboards/1860-node-exporter-full/)
- [Grafana docs](https://grafana.com/docs/grafana/latest/setup-grafana/configure-grafana/)
- [K8s deployment](https://forge.tedomum.net/tedomum/kity/-/tree/master/kube-monitoring)
- Exporters: https://github.com/pschiffe/mailcow-dockerized/blob/563d5e00e236898edc3d2160f3b1c6be0c437baa/docker-compose.yml#L647 
- Some Configuration and reference stuff: https://github.com/stefanprodan/dockprom