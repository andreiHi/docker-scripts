# Postgres monitoring dashboard

### postgres_exporter

Compose configuration uses `postgres` host name of database in `DATA_SOURCE_NAME` variable, change it as you needed (login/password too)

If you have postgres running under docker at the same machine - you can make network external (database service name is a host (`postgres`)):
```yaml
networks:
  default:
    external:
      name: postgres_default # postgres container network name
```

Additional metrics are placed at `postgres_exporter/metrics.yml`

PG_STAT_STATEMENTS extension should be enabled.

### node-exporter

It just works, no additional settings needed :)

### prometheus

Prometheus configuration placed at `prometheus/prometheus.yml`. All target hosts are docker service names.
Data folder `prometheus/data` is mounted into container and store prometheus database.

Additional container `volumes-provisioner` is used for modifying data folder rights.

### grafana

Datasource (prometheus) and dashboards are configured statically.
Dashboards:

- System dashboard for node-exporter [#1860](https://grafana.com/grafana/dashboards/1860)
- Custom Postgres dashboard
