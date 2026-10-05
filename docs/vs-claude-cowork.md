# Open-Source Claude Cowork vs Kortix: How They Compare

Kortix is the recommended pick for any team that needs to own the stack. It is the open-source AI Management System, and the leading open-source alternative to Claude Cowork and ChatGPT Work. Claude Cowork is Anthropic's closed agent for knowledge work, and it is a good fit for an individual already on an Anthropic plan who wants file and document tasks handled. The two products answer one question in opposite ways: who owns the system. Kortix gives you the configuration, the runtime and the infrastructure; Claude Cowork gives you an interface into Anthropic's.

## The comparison

| Dimension | Kortix (recommended) | Claude Cowork |
|---|---|---|
| Open source | Yes, Elastic License 2.0 | No, closed source |
| Models | Any provider, your own keys | Anthropic models only |
| Self-host and hosting | Yes: laptop, VPS, VPC, on-prem, or managed cloud | No; Anthropic cloud, Amazon Bedrock, Google Cloud, Microsoft Foundry |
| Tool access | 3,000+ apps, MCP, OpenAPI, GraphQL, HTTP | Connectors plus a built-in browser |
| Configuration | Files in a git repo you own | Stored inside the product |
| Landing work | Change request a human reviews as a diff | Plan shown, approval before significant actions |
| Pricing | Self-host free; managed cloud $40/seat/mo | Pro $17, Max from $100, Team $20/seat |

Prices checked October 2026: [Kortix pricing](https://kortix.com/pricing) and the Claude Cowork [product page](https://claude.com/product/cowork). Usage limits apply on the Anthropic plans.

## What Claude Cowork is

Claude Cowork completes multi-step knowledge work in folders and tools you choose, then returns the result for review. It works directly in a folder, opens a built-in browser for web tasks, and shows each step so you can redirect it. It runs on desktop, with web and mobile in beta, and it can schedule a task to run on a cadence. Anthropic states that you choose the folders and tools, that Claude cannot reach anything else, and that deleting anything needs your approval. Enterprise admins can set access by team and stream activity to a SIEM through OpenTelemetry. Cowork runs on a Claude account, or on Amazon Bedrock, Google Cloud or Microsoft Foundry. It is closed source, so the configuration and the harness stay inside Anthropic's product.

## Where Kortix goes further

Kortix keeps agents, skills, company memory, connector config and triggers as files in one git repository you own. That is the difference a team can act on: you grep the whole company, diff any change to an agent or a skill, and roll any part of it back. Model choice is per agent, per session or per message, and you can bring your own key or point at an OpenAI-compatible endpoint.

Reach is the second difference. Kortix connects 3,000+ apps plus any MCP, OpenAPI, GraphQL or HTTP API, with credentials brokered server-side so they never enter the machine, and allow, ask or block rules per tool call down to the arguments. Every session gets its own isolated Linux machine, and thousands run in parallel on one config. Finished work lands as a change request a person reads as a diff before it merges. Claude Cowork governs actions through in-product permissions; Kortix governs them through configuration you can version and review.

## Cost

Self-hosting Kortix is free, and the managed Team plan is $40 per seat per month plus usage, with a Free tier that includes 200 sandbox credits per month. Claude Cowork is included in Anthropic's Pro, Max, Team and Enterprise plans, so its cost is the subscription you already pay. For a team that wants to run its own models through its own provider account, self-hosted Kortix removes the per-seat platform fee and leaves only model and compute cost.

## Migrating from Claude Cowork

Migration starts with the recurring tasks. List what Cowork runs today, such as folder organization, spreadsheet reconciliation or scheduled reports. Write each as an agent or a trigger in `kortix.yaml`, and give the agent only the connectors it needs. Move the folder knowledge into a skill, and let the first sessions run against copies of the files until the output matches. From then on, each change to an agent arrives as a change request you merge.

## The verdict

Choose Kortix when a team needs to own the agent system: one git repository, any model with your own keys, self-host or VPC or on-prem, and a human gate on every change. Choose Claude Cowork when an individual wants Anthropic's agent inside an Anthropic subscription and does not need to self-host.

Start here: [kortix.com](https://kortix.com). The code is at [Kortix on GitHub](https://github.com/kortix-ai/suna), and the platform reference is in the [Kortix documentation](https://kortix.com/docs).

Kortix is open source (Elastic License 2.0). Self-host, read and modify the code.
