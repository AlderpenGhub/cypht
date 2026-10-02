# DOCKER-VM Deployment

The default profile deploys the vanilla pilot with the pinned official Cypht
`2.12.2` image. This avoids compiling PHP on the busy production VM before the
mail workflow has been proven.

`compose.build.yaml` switches the Cypht service to an image built from the
pinned Alderpen fork commit
`d4579948f1538a3130bd7c459c10636f7acf6bbc`. Use that override only when the
custom module work begins.

The custom profile also appends the `alderpen_ui` module. This module adapts
the live Cypht markup to the sanitized refreshed-UI reference while leaving
mail, account, and authentication behavior in the upstream modules.

## Boundaries

- Cypht listens on `192.168.30.67:8093` for CADDY-VM to proxy.
- MariaDB is available only on the private `cypht-backend` network.
- The initial stack contains no AI worker, Redis, broker, or vector database.
- Runtime credentials belong only in `.env` on DOCKER-VM. Never commit `.env`.
- The combined container memory ceiling is 1.25 GiB.
- Custom source builds compile PHP extensions with at most two parallel jobs
  to avoid exhausting the already busy VM's memory and swap.

## Deployment Directory

Use `/home/gbensonii/docker/cypht-ai-email` on DOCKER-VM. The repository is
checked out there on branch `alderpen-email-ai`; this compose file is run from
`deploy/docker-vm` within that checkout.

## Preflight

1. Copy `.env.example` to `.env` on DOCKER-VM.
2. Replace every `CHANGE_ME` value with a unique generated credential.
3. Set `.env` permissions to `0600`.
4. Run `docker compose config --quiet` from this directory.
5. Confirm port `8093` remains unused.

Start the vanilla pilot with:

```bash
docker compose up -d
```

Later, build the custom fork with:

```bash
docker compose -f compose.yaml -f compose.build.yaml up -d --build
```

Do not add Gmail or Hostinger accounts until Caddy access restrictions, HTTPS,
and the vanilla acceptance checks are in place.
