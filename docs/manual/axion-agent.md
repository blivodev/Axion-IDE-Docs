# Axion Agent

**Axion Agent** is the default agent of Axion IDE. It ships **installed and enabled**
with the app — uninstall or re-enable it any time from the Marketplace (or untick it
in the composer's **Skills & Agents** flyout).

While enabled, the agent's playbook is injected into every chat prompt, so the AI
knows it can orchestrate the full capability set below.

## Capabilities

| Area | What the agent can do |
|------|-----------------------|
| **IDE self-control** | Drive Axion IDE itself through its MCP bridge — editor buffers, terminal, file explorer, diff apply, git checkpoints, DAG pipeline, workflows. |
| **Web browsing** | Search and read the web (`fetch`, `brave-search`) and automate a real browser (`puppeteer`, Chrome DevTools) — navigate, snapshot, click, type, screenshot. |
| **Memory** | Persist durable project facts in a knowledge graph (`memory` MCP) and recall them before planning. |
| **Sequential thinking** | Structured multi-step reasoning (`sequential-thinking` MCP) for complex work. |
| **Screen control & recording** | Screenshots, mouse/keyboard automation, and demo recording on Windows/Linux (`windows-mcp`, `linux-desktop-mcp`, `screen-recorder`). |
| **Architecture & orchestration** | Plans first, keeps a task list, runs the sub-agent DAG, and delegates to other agents/MCPs. |
| **Installations** | Installs plugins, agents, MCP servers, and skills from the Marketplace on demand. |
| **Testing & SQL** | Writes and runs tests before declaring work done; designs, runs, and optimizes SQL. |
| **Virtualization** | Boots and tests VMs with `qemu` / `virtualbox`; Linux workflows via `wsl2`. |
| **Documentation** | Highly detailed user manuals, ELI5 developer docs, and ELI5 comments on every feature. |
| **Questions** | Asks multiple-choice question cards right in the chat (see below). |
| **Audio** | Captures and manipulates audio (`audio-capture`). |
| **Remote access** | SSH sessions, remote commands, and SFTP sync (`ssh-mcp`). |
| **Cryptography** | Established open-source crypto libraries only — never home-made crypto. |
| **Containers** | Docker/Podman build, run, logs, and compose stacks. |
| **UI design & code** | Interface work in the app's dark charcoal + neon accent style. |

Open source first: the agent prefers open-source tools and industry-standard options
in everything it does.

## Default toolkit

These MCP servers ship **connected by default** so the agent works out of the box
(disconnect any of them from the MCP view):

`memory` · `sequential-thinking` · `filesystem` · `sqlite` · `fetch` ·
`brave-search` · `puppeteer`

Additional capability servers are one click away in the MCP marketplace:
`screen-recorder`, `qemu`, `virtualbox`, `wsl2`, `audio-capture`, `docker`,
`postgres`, and more.

## Question cards

When a decision is genuinely yours, the agent ends its reply with a question block and
the chat renders a **card**:

- **Numbered options** — each with a short description; the agent marks the one it
  **recommends**
- **Free-text box** — type your own answer instead
- **Skip** — dismiss the question

Click an option (or send typed text) and the conversation continues immediately; the
card collapses to `Answered: …` or `Question skipped.`

## Managing the agent

- **Uninstall / disable** — Marketplace → Axion Agent → *Uninstall*, or untick it in
  the composer's **Skills & Agents** flyout.
- **Re-enable** — install it again from the Marketplace; it is a first-party item, so
  it stays in the catalog.
- **StarVault** - the zero-knowledge credential vault, connected over MCP. The agent can
  search entries, retrieve secrets and TOTP codes, generate passwords, API keys,
  certificates and keypairs, run crypto tools, and audit vault health - all without you
  pasting anything. The vault stays **locked** until you unlock it with your master
  password.
