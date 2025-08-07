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

## Setup for neat integration with local server
### Create ssh keys for login from cloud server to local server
```sh
ssh-keygen -t ed25519 -f ~/.ssh/remote-login
ssh-copy-id -i ~/.ssh/remote-login.pub robot@100.78.154.44
```
verify
```sh
ssh -i ~/.ssh/remote-login robot@100.78.154.44
```

### Make shutdown on local without password
```sh
sudo visudo
>>>>>>
# enable shutdown without password
robot ALL=(ALL) NOPASSWD: /sbin/shutdown
```