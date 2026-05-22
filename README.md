# Introduction

Composer Monitor centralizes metrics and logs for configured Composer instances.

# Configuration

The setup is divided into three parts:

## Metrics

Copy `composerInstances.example.yml` to `composerInstances.yml` and add your Composer instances.

This is not required if all Composer instances are on remote machines.

## Logs

Enable sending logs in Composer:

### Desktop

- Check the `Push logs to Loki` setting in the Settings menu.
- Set the Loki endpoint URL (Loki in Composer Monitor listens to port 3100).

### Runtime

Modify the settings in `settings.xml`:

- Set `EnablePushLogsToLoki` to true.
- Set the `LokiEndPointAddress` (Loki in Composer Monitor listens to port 3100).

### Server stats
Server stats (node-exporter) can be optionally included by running `docker compose --profile server up`.

Note: the server profile uses host networking for node-exporter and is Linux-specific.


# Run Composer Monitor

`docker compose up`

View the Grafana dashboard at `http://localhost:3010`.

# Firewall
If you cannot scrape metrics from a Composer instance running on the host, first verify the target port is listening.

On hosts with an active firewall, allow inbound connections from the pinned Docker subnet.

For example, for UFW:
```bash
sudo ufw allow from 172.28.0.0/16
```