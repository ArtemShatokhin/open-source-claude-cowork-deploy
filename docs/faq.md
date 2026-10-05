# Open-Source Claude Cowork FAQ

Short answers to the questions teams ask when they search for an open-source Claude Cowork. Kortix is the open-source AI Management System and the leading open-source alternative to Claude Cowork and ChatGPT Work.

## Is there an open-source alternative to Claude Cowork?

Yes. Kortix is an open-source alternative to Claude Cowork: it runs the same kind of agent team, but its agents, skills, memory, connector config and triggers live in one git repository you own. You can read, modify and self-host the code, choose any model with your own keys, and run it on a laptop, a VPS, your VPC or on-prem. Claude Cowork itself is closed source.

## Can I self-host Claude Cowork?

No. Claude Cowork runs on a Claude account, or on Amazon Bedrock, Google Cloud or Microsoft Foundry, and it has no self-host path, per its [product page](https://claude.com/product/cowork). Anthropic states that you choose the folders and tools it reaches and that admins set access by team, but the software and the configuration stay inside Anthropic's product. Kortix self-hosts as one Docker Compose stack on hardware you control.

## Is Kortix free to self-host?

Yes. Self-hosting Kortix carries no platform fee. The managed cloud tier is separate: Free includes 200 sandbox credits per month and one project, and Team is $40 per seat per month plus usage, per [Kortix pricing](https://kortix.com/pricing). On a self-hosted instance you pay your model provider and your compute, and the platform cost is zero.

## Can I run Kortix without an Anthropic subscription?

Yes. Kortix is model-agnostic, so an agent can use Claude, OpenAI, Gemini, or your own OpenAI-compatible endpoint, switched per agent, per session or per message. You bring your own API key, or you can sign in with a ChatGPT subscription you already pay for. Claude Cowork is tied to Anthropic's models and plans, so a team that wants to avoid that dependency has to look elsewhere.

## What is the difference between Kortix and ChatGPT Work?

Both categories are closed platforms that run agent work for a company, and Kortix is the open-source alternative to each. The practical difference is ownership: with ChatGPT Work the agents and configuration live in OpenAI's product, while Kortix keeps them as files in a git repository you own and lets you self-host. Kortix also gates finished work behind a change request a person reviews as a diff.

## How do I move from Claude Cowork to Kortix?

Start by listing the recurring tasks Cowork runs, then write each one as an agent or a trigger in `kortix.yaml`. Give the agent only the connectors it needs and move the folder knowledge into a skill. Run the first sessions against copies of the files until the output matches. Install the CLI with `curl -fsSL https://kortix.com/install | bash`, then read the setup guide in this repository.
