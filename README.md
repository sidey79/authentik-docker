# authentik-docker

Docker stack for authentik (OIDC IdP), based on `template_docker`.

## Included

- `docker-compose.yml` with:
  - `postgresql`
  - `redis`
  - `authentik-server`
  - `authentik-worker`
- `.env.example` as secret-free template
- `.gitignore` to keep local secret files out of git

## Quick start

```bash
cp .env.example .env
# edit .env and set strong secrets/passwords
docker compose pull
docker compose up -d
```

Open:

- http://localhost:9000
- https://localhost:9443

## Security notes

- Never commit `.env`.
- Keep reverse proxy and TLS termination in front for production.
- Restrict direct access to authentik service ports.

## Reverse proxy integration (recommended)

Use your existing Caddy reverse proxy as entrypoint and expose authentik only internally.
