# Self-Host Open-Source Kortix: Setup

A bare Linux box becomes a running self-hosted instance of open-source Kortix in a few commands. Kortix is the open-source AI Management System, and it deploys as one Docker Compose stack. The path runs from the evaluation shortcut to the sandbox provider key, updates and backups, following the [Kortix self-hosting documentation](https://kortix.com/docs/host).

## What you are installing

One Docker Compose stack runs four services: the frontend, the API, the LLM gateway and the Supabase distribution. Agent sessions run on a separate sandbox provider, not on this stack. The default provider is Daytona; Platinum and E2B are also supported. This split matters when you debug: a session failure is usually a sandbox provider problem, while a dashboard failure is a stack problem.

## Requirements

- A Linux box for the one-shot script. Another OS takes the manual path below.
- A domain with an A/AAAA record for the domain itself and for `api.<domain>`, both pointing at the box.
- Ports 80 and 443 open. The bundled Caddy proxy uses them to issue a TLS certificate.
- An 8 GiB host is enough to start. Each API container is limited to 640 MiB by default.

## One-shot bootstrap

A bare Linux box has a one-shot path as well. One command installs Docker, installs the `kortix` CLI and starts the stack, taking your domain and an email address as flags. It runs on Linux only. Take the manual path below when you want each step under your own control, or open the [Kortix self-hosting documentation](https://kortix.com/docs/host) to copy the script command.

## Manual path

Use this on macOS, or when you want each step under your own control.

```bash
# 1. Install the CLI
curl -fsSL https://kortix.com/install | bash

# 2. Point DNS first: A/AAAA for the domain and for api.<domain>, ports 80 and 443 open

# 3. Initialize and start
kortix self-host init --domain kortix.example.com
kortix self-host start

# 4. Verify
kortix self-host status
kortix self-host logs
kortix self-host doctor
```

## Evaluation mode

To try Kortix with no domain, use a Cloudflare tunnel instead:

```bash
kortix self-host init --tunnel cloudflare
kortix self-host start
```

The tunnel URL changes on every restart. This mode is for evaluation, not production.

## Set the sandbox provider key

After the stack starts, run the interactive setup:

```bash
kortix self-host configure
```

It prompts for the sandbox provider key and, optionally, a managed-git token. Then sign in to the dashboard and connect your own LLM key in the model picker. A self-hosted instance uses your own key by default, so model cost runs through your provider account.

## Memory limit

Each API container has a 640 MiB memory limit by default. Keep the default on an 8 GiB host. On a 16 GiB host where API traffic reaches that limit, raise it to 1 GiB and confirm it took effect:

```bash
kortix self-host env set KORTIX_API_MEMORY_LIMIT=1024m
docker stats --no-stream
```

## Updates

Every instance updates itself automatically. Pin an exact version when you need a reviewed release, and turn the auto-updater off when a box must not move on its own:

```bash
kortix self-host update --tag 0.9.84
kortix self-host update --auto-update off
```

## Backups

Kortix has no separate backup system. Copy three paths before you run a destructive command:

- `~/.config/kortix/self-host/<instance>/volumes/db/data` holds the Postgres database.
- `~/.config/kortix/self-host/<instance>/volumes/storage` holds file storage.
- `~/.config/kortix/self-host/<instance>/.env` holds every secret and signing key the instance uses.

Restore by putting the three paths back on a host with the same domain, then start the stack again.

## Verify the install

A healthy instance answers on your domain, `kortix self-host status` reports the stack up, and `kortix self-host doctor` reports no failing checks. Start a session from the dashboard or from a terminal with `kortix sessions new --prompt "hello"` and confirm it boots a sandbox. That last step proves the sandbox provider key is wired correctly, which the Compose stack alone cannot tell you.
