# authentik-docker

Docker stack for authentik (OIDC IdP), based on `template_docker`.

## Included

- `docker-compose.yml` with:
  - `postgresql`
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

- via reverse proxy only (no host port publishing in this stack)

## Security notes

- Never commit `.env`.
- Keep reverse proxy and TLS termination in front for production.
- Restrict direct access to authentik service ports.

## Reverse proxy integration (recommended)

Use your existing Caddy reverse proxy as entrypoint and expose authentik only internally.

## SMTP relay integration

For outbound mails (invites, password reset, notifications), this stack can use
[`smtp-relay-docker`](https://github.com/sidey79/smtp-relay-docker).

The default `.env.example` points Authentik to SMTP host `smtp-relay` on port `25` inside
`network_backend_net`.

## Networking model

- `authentik-server` is attached to:
  - `authentik_internal` (internal app network)
  - external proxy network `network_backend_net`
- No container ports are published to the host.
- Ensure `network_backend_net` exists before starting this stack.
