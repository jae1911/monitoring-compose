# monitoring-compose

Compose files for a monitoring system.

## Requirements

- Docker
- Docker Compose

## What does it contains

- Grafana
- Prometheus
- Uptime Kuma
- node_exporter (optional, machine stats)

## Notes

- This deployment assumes you use [Traefik](https://traefik.io/traefik/) as a reverse proxy
- This deployment does not uses SMTP (see `GF_SMTP_*` configuration keys for that)
- Some part of the configuration related to OAUTH was omitted to simplify this repo (see `GF_AUTH_GENERIC_OAUTH_*` configuration keys for that)
- Network configuration of the Compose file was omitted

## Volumes

This deployment uses multiple volumes:

- `.` - Current directory, pulled from the configuration repository`
- `/mnt/store` - A dedicated storage area

## HowTo

1. Change paths of `/mnt/secrets` and `/mnt/store` to your desired ones.
2. Create the environment file `.env` containing:

    grafanahostname=grafana.something.tld
    kumahostname=kuma.something.tld

    GF_SECURITY_ADMIN_PASSWORD=iamsecret
    POSTGRES_DB=grafana
    POSTGRES_USER=grafana
    POSTGRES_PASSWORD=evenmoresecret

3. `docker compose up -d uptime-kuma` and set it up
4. Fill the uptime-kuma credentials in the `prometheus.yml` to be able to scrape data from it
5. `docker compose up -d` bring the rest of the services up

You can now go on your Grafana hostname and set it up.

## Additional resources

- [Uptime Kuma sample Grafana dashboard](https://github.com/louislam/uptime-kuma/tree/unofficial/grafana-dashboard)
- [node_exporter sample Grafana dashboard](https://grafana.com/grafana/dashboards/1860-node-exporter-full/)
- [Grafana docs](https://grafana.com/docs/grafana/latest/setup-grafana/configure-grafana/)
