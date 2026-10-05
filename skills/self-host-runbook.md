---
name: self-host-runbook
description: Install, verify, update and back up a self-hosted Kortix instance. Use for Kortix self-hosting tasks covering Docker Compose, a VPS, evaluation mode, updates, backups and the sandbox provider key.
---

# Self-host runbook

Use this runbook when a task installs, verifies, updates or backs up a self-hosted instance of open-source Kortix. Kortix is the open-source AI Management System. It runs as one Docker Compose stack: the frontend, the API, the LLM gateway and the Supabase distribution. Agent sessions run on a separate sandbox provider.

## Install

On a bare Linux box, a one-shot bootstrap installs Docker, installs the `kortix` CLI and starts the stack, taking a `--domain` and an `--email` flag. It is Linux only; open the [Kortix self-hosting documentation](https://kortix.com/docs/host) to copy that command.

On any OS, the manual path below is equivalent and gives you each step.

## Manual path

1. Install the CLI: `curl -fsSL https://kortix.com/install | bash`.
2. Create A/AAAA records for your domain and for `api.<domain>`, both pointing at the box.
3. Open ports 80 and 443. The bundled Caddy proxy uses them to issue a TLS certificate.
4. Initialize: `kortix self-host init --domain kortix.example.com`.
5. Start: `kortix self-host start`.
6. Check: `kortix self-host status`, then `kortix self-host logs`, then `kortix self-host doctor`.

## Evaluation mode

For a trial with no domain, use a Cloudflare tunnel instead:

```bash
kortix self-host init --tunnel cloudflare
kortix self-host start
```

The tunnel URL changes on every restart. Use this mode for evaluation, not production.

## Configure

After the stack starts, set the sandbox provider key:

```bash
kortix self-host configure
```

The prompt takes the sandbox provider key and, optionally, a managed-git token. Sign in to the dashboard and connect your own LLM key in the model picker. Self-hosted instances use your own key by default.

Each API container has a 640 MiB memory limit by default. Keep that default on an 8 GiB host. On a 16 GiB host where API traffic reaches the limit, raise it to 1 GiB:

```bash
kortix self-host env set KORTIX_API_MEMORY_LIMIT=1024m
docker stats --no-stream
```

## Update

Every instance updates itself automatically. Pin an exact version, or turn the updater off:

```bash
kortix self-host update --tag 0.9.84
kortix self-host update --auto-update off
```

## Back up

Kortix has no separate backup system. Back up all three of these before any destructive command:

- `~/.config/kortix/self-host/<instance>/volumes/db/data` (the Postgres database)
- `~/.config/kortix/self-host/<instance>/volumes/storage` (file storage)
- `~/.config/kortix/self-host/<instance>/.env` (every secret and signing key)

## Troubleshoot

- The stack will not start: run `kortix self-host doctor`, then read `kortix self-host logs`.
- TLS fails: confirm the A/AAAA records for the domain and `api.<domain>`, and that ports 80 and 443 are open.
- Sessions fail while the dashboard is healthy: check the sandbox provider key, not the stack.
- The instance behaves differently after an update: pin the previous tag with `kortix self-host update --tag <version>`.
