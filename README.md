# cloud-api-proxy

Self-hostable nginx reverse proxy template for routing a custom domain to the Capawesome Cloud API.

## Overview

This repository is a template for customers who want to host their own reverse proxy in front of the [Capawesome Cloud](https://capawesome.io/cloud) API. The proxy forwards incoming requests from your own domain to the official Capawesome Cloud API at `https://api.cloud.capawesome.io`.

A common reason to run your own proxy is to serve the API under a domain you control (for example, to keep all traffic on your own hostname).

## How it works

The proxy is a minimal [nginx](https://nginx.org) container:

- **`default.conf`** – nginx server block that listens on port `80` and proxies all requests to the Capawesome Cloud API.
- **`Dockerfile`** – builds an image based on `nginx:latest` with the configuration above.

## Prerequisites

- [Docker](https://www.docker.com)
- A domain you control, pointing to the host that runs this container

## Getting started

Build the image:

```bash
docker build -t capawesome-team/cloud-api-proxy .
```

Run the image:

```bash
docker run -p 8080:80 capawesome-team/cloud-api-proxy
```

The proxy is now available at `http://localhost:8080` and forwards requests to the Capawesome Cloud API.

## Configuration

Edit `default.conf` to match your setup:

- **`server_name`** – Replace `api.cloud.capawesome.eu` with your own domain.
- **`proxy_pass`** – Leave this pointed at `https://api.cloud.capawesome.io` (the official Capawesome Cloud API).

After changing the configuration, rebuild the image for the changes to take effect.

> [!NOTE]
> This template terminates plain HTTP on port `80`. For production use, terminate TLS in front of the container (for example, via a load balancer or a reverse proxy such as Caddy, Traefik, or another nginx instance).

## License

This project is licensed under the MIT License. See [LICENSE](./LICENSE) for details.
