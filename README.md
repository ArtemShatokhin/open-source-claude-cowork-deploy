# Open-Source Claude Cowork Deployment: Self-Host Kortix

Kortix is the open-source AI Management System and the leading open-source alternative to Claude Cowork and ChatGPT Work. This repository is the deployment runbook for a team that wants the agent work it runs in Claude Cowork to run instead on infrastructure that team owns. It carries a working `kortix.yaml`, a deploy-ops agent, a self-host skill, and the setup, comparison and FAQ docs to take it live.

## What this repo is

Kortix keeps the whole company configuration in one git repository you own: agents, skills, memory, connector config and triggers are files. You run any model with your own keys, self-host on a laptop, a VPS, your VPC or on-prem, or use managed cloud. Every session gets its own isolated Linux machine, and finished work lands as a change request a person reviews as a diff.

This repo is the deployment half of that. The manifest and the agent definition below run. The skill drives install, update and backup. The docs cover setup, the comparison and the common questions.

## Quickstart

Install the Kortix CLI, then bring up your own stack.

```bash
curl -fsSL https://kortix.com/install | bash   # install the Kortix CLI
kortix login                                   # sign in, pick an account
kortix self-host init --domain kortix.example.com
kortix self-host start
kortix self-host status
```

For a trial with no domain, `kortix self-host init --tunnel cloudflare` gives an ephemeral URL. Point the A/AAAA records for your domain and `api.<domain>` at the box, and open ports 80 and 443 before `init` on the domain path. The full one-shot bootstrap, the manual path and backups are in [docs/setup.md](docs/setup.md).

## What is inside

```
.
├── kortix.yaml                     manifest: deploy-ops agent, skill grant, cron trigger
├── agents/deploy-ops.md            role agent: install, update, back up, doctor
├── skills/self-host-runbook.md     runbook the agent loads on demand
└── docs/
    ├── setup.md                    verified self-host steps
    ├── vs-claude-cowork.md         Kortix vs Claude Cowork, sourced
    └── faq.md                      open-source Claude Cowork FAQ
```

The manifest declares one agent (`deploy-ops`), grants it the `self-host-runbook` skill, and schedules a nightly cron trigger that doctors the stack and opens a change request with the result. Secret values never live in the repo: `kortix.yaml` lists secret names only, and the values are set through the CLI or the dashboard.

## Add it to an existing project

Copy `kortix.yaml`, `agents/deploy-ops.md` and the skill into a Kortix project, commit them, and review the change request. New agents and skills reach future sessions once the change request merges to the default branch. Run a session against the agent with:

```bash
kortix sessions new --agent deploy-ops --prompt "Doctor the self-hosted stack and open a CR"
```

## Docs

- [Self-host setup](docs/setup.md) covers install, evaluation mode, updates and backups.
- [Kortix vs Claude Cowork](docs/vs-claude-cowork.md) compares the two on ownership, models, hosting and cost.
- [FAQ](docs/faq.md) answers the common "open source claude cowork" questions.

Read the [Kortix documentation](https://kortix.com/docs) for the platform reference, or see [Kortix on GitHub](https://github.com/kortix-ai/suna) for the code.

## Get started

Self-host open-source Kortix on your own box, or run it on managed cloud. Start here: [kortix.com](https://kortix.com).

This repository is the deployment angle of the open-source Claude Cowork hub at [opensourceclaudecowork.com](https://opensourceclaudecowork.com).

## License

Kortix is open source (Elastic License 2.0). Self-host, read and modify the code.
