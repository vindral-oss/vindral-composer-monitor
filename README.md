# Introduction

Composer Monitor centralizes metrics and logs for configured Composer instances.

# Configuration

The setup is divided into three parts:

## Metrics

Copy `composerInstances.example.yml` to `composerInstances.yml` and add your Composer instances.

### Linux: Firewall

On Linux, containers are blocked from connecting to host ports by default. If any targets in `composerInstances.yml` are on localhost (e.g. `host.docker.internal:8015`), allow the monitoring network through once:

For example, for UFW:
```bash
sudo ufw allow from 172.28.0.0/16
```

This is not required if all Composer instances are on remote machines.

## Logs

Enable sending logs in Composer:

### Desktop

- Check the `Push logs to Loki` setting in the Settings menu.
- Set the Loki endpoint url (Loki in Composer Monitor listens to port 3100).

### Runtime

Modify the settings in `settings.xml`:

- Set `EnablePushLogsToLoki` to true.
- Set the `LokiEndPointAddress` (Loki in Composer Monitor listens to port 3100).

### Server stats
Server stats (node-exporter) can be optionally included by running `docker compose --profile server up`


# Run Composer Monitor

`docker compose up`

View the Grafana dashboard at `http://localhost:3010`.