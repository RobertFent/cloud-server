# cloud server
These are the config files for my hetzner hosted vps

## Tailscale
ensure .env contains valid auth key (https://login.tailscale.com/admin/settings/keys)
```bash
docker compose -f tailscale/docker-compose.yml up -d
```

## Home Assistant
```bash
docker compose -f home-assistant/docker-compose.yml up -d
```
ensure that the following lines are in home-assistant/configs/configuration.yaml
```yml
http:
  use_x_forwarded_for: true
  trusted_proxies:
    - 172.22.0.0/16 
```