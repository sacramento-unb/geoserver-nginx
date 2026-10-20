# GeoServer Nginx proxy experiment

This repository contains an incomplete Nginx reverse-proxy experiment intended
to route requests to a GeoServer service on port `8080`.

## Current contents

- `nginx/default.conf` defines a proxy from Nginx to `http://geoserver:8080`;
- `render.yaml` describes a Render Docker service;
- `docker-compose.yaml` is currently empty.

## Reproduction status

The project cannot be built or started in its current state. `render.yaml`
references `./Dockerfile`, but that file is not present, and the empty Compose
file defines neither the `geoserver` upstream nor the Nginx service.

The Nginx configuration also sets `X-Forwarded-Proto` to `https` unconditionally.
That is correct only when TLS is actually terminated in front of this proxy.

## Work needed before use

1. Add or identify the intended GeoServer image and version.
2. Add an Nginx image/Dockerfile and copy `nginx/default.conf` into it.
3. Define both services, network, persistent GeoServer data and health checks.
4. Decide where TLS terminates and forward the real scheme.
5. Add bounded upload/proxy timeouts appropriate for geospatial requests.
6. Validate the configuration with `docker compose config` before starting it.

No container was started during the documentation audit. There is no
repository-level license file; confirm reuse and redistribution terms first.
