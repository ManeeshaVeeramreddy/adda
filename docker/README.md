# Docker Containerization

## Overview

Docker was used to package the portfolio application into a container so that it could run consistently across different environments.

The application source code is maintained in a separate repository:

[portfolio-simple](https://github.com/ManeeshaVeeramreddy/portfolio-simple)

## Docker Technology

- Docker Engine
- Nginx
- Alpine Linux
- Docker Hub

## Dockerfile

The portfolio application uses Nginx as its base image.

```dockerfile
FROM nginx:alpine

COPY . /usr/share/nginx/html/

EXPOSE 80
```

## Explanation

1. `FROM nginx:alpine` – Uses the lightweight Nginx Alpine image.
2. `COPY . /usr/share/nginx/html/` – Copies the portfolio application files into the Nginx web root.
3. `EXPOSE 80` – Documents the HTTP port used by Nginx inside the container.

## Docker Image

**Docker Hub image:** `maneesha0805/portfolio:v1`

The image was published to Docker Hub and subsequently pulled onto the AWS EC2 instance.

## Verification

The following commands were used to inspect the Docker image:

```bash
docker images
docker history maneesha0805/portfolio:v1
```

The image history confirms the Nginx base image and the portfolio files copied into the container.

## AWS Deployment

The Docker image `maneesha0805/portfolio:v1` runs on the existing AWS EC2 instance.

The container port is mapped to:

```text
127.0.0.1:8080 -> 80/tcp
```

Caddy acts as the reverse proxy and provides HTTPS access to the website.

**Live application:** https://maneeshareddy.duckdns.org
