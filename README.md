# Running a service behind Tailscale and Caddy reverse proxy using Docker compose

This repo is for this blog [post](https://ricklan.net/blog/2024/10/running-a-service-behind-tailscale-and-caddy-reverse-proxy-using-docker-compose/).

## Usage

1. `git clone` this repo
2. Modify the Tailscale OAuth secret in [.env](./.env) according to your Tailscale settings.
3. Modify the "hostname" in [docker-compose.yml](./docker-compose.yml) to your Tailscale settings.
4. Modify the domain name in [Caddyfile](./Caddyfile) to your Tailscale settings.
5. Run `docker compose up -d`.
6. Browse to [https://your-service.your-tailscale-network.ts.net](https://your-service.your-tailscale-network.ts.net). There might be a delay for creation of a domain certificate.

Logs of tailscale container during creation of domain certificate:

```txt
2024-10-04 11:10:42 tailscale-1  | 2024/10/04 02:10:42 cert("my-service.my-tailscale-network.ts.net"): registered ACME account.
2024-10-04 11:10:42 tailscale-1  | 2024/10/04 02:10:42 cert("my-service.my-tailscale-network.ts.net"): starting SetDNS call...
2024-10-04 11:10:53 tailscale-1  | 2024/10/04 02:10:53 cert("my-service.my-tailscale-network.ts.net"): did SetDNS
2024-10-04 11:10:55 tailscale-1  | 2024/10/04 02:10:55 cert("my-service.my-tailscale-network.ts.net"): requesting cert...
2024-10-04 11:10:56 tailscale-1  | 2024/10/04 02:10:56 cert("my-service.my-tailscale-network.ts.net"): got cert

```

## Tested

* Docker Desktop on macOS 15 on Apple Silicon.
* Docker on Ubuntu 22.04 LTS on Intel CPU.
