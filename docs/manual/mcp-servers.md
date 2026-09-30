# MCP Servers

Axion connects to **Model Context Protocol** servers so agents can use external tools
(3D, browsers, databases, desktops...).

## Marketplace (one-click installs)

The MCP view starts with the **Marketplace**: a curated catalog of **400+ servers**. Search
it by name, category, or capability, or browse by category.

| Category | Examples |
|----------|----------|
| **Official** | `filesystem`, `memory`, `sequential-thinking`, `fetch`, `time`, `everything`, `git`, `github`, `gitlab`, `slack`, `google-drive`, `notion` |
| **Desktop** | `windows-mcp`, `macos-mcp`, `linux-desktop-mcp`, `wsl2`, `remote-session` |
| **Data** | `postgres`, `sqlite`, `mysql`, `redis`, `mongodb`, `elasticsearch`, `snowflake`, `bigquery`, `clickhouse`, `duckdb`, `neo4j`, `supabase`, `airtable`, `google-sheets` |
| **Cloud** | `aws`, `azure`, `gcloud`, `cloudflare`, `firebase`, `vercel`, `netlify`, `railway`, `fly-io`, `digitalocean` |
| **DevOps** | `docker`, `docker-hub`, `kubernetes`, `helm`, `terraform`, `podman`, `npm-registry`, `nuget`, `pypi` |
| **Observability** | `sentry`, `grafana`, `prometheus` |
| **Quality & Security** | `sonarqube`, `snyk`, `trivy`, `starvault` |
| **Productivity** | `linear`, `jira`, `confluence`, `asana`, `trello`, `monday`, `obsidian` |
| **Commerce & CRM** | `stripe`, `shopify`, `hubspot`, `salesforce`, `zendesk` |
| **Search & Browser** | `brave-search`, `exa-search`, `puppeteer`, `playwright`, `google-maps` |
| **Documents & Media** | `pdf-reader`, `office-docs`, `image-tools`, `youtube-transcript`, `screen-recorder`, `audio-capture` |
| **Virtualization** | `qemu`, `virtualbox` |
| **AI** | `huggingface`, `openapi-bridge` |

1. Search or browse the catalog.
2. Click **Install** — the server appears as CONNECTED in the hub. No connection
   strings needed.

## Default toolkit (Axion Agent)

These servers ship **connected by default** so the [Axion Agent](axion-agent.md)
works out of the box:

`memory` · `sequential-thinking` · `filesystem` · `sqlite` · `fetch` ·
`brave-search` · `puppeteer`

They are ordinary hub cards — disconnect or remove them any time, and reinstall from
the Marketplace or by GitHub URL.

## Install from GitHub

Paste any `https://github.com/user/mcp-server-repo` URL into the **Install from
GitHub** field and click install. The server registers as
`npx -y github:user/repo`.

## Manual install

Need something custom? Click **Add MCP Server** (the ⚙️ area above the list) and
fill in:

- **Server identifier** — e.g. `nadia-mcp`
- **Transport** — `stdio / CLI` or HTTP/SSE
- **Command / executable** — e.g. `node C:\tools\server.js`

## Managing servers

Each connected server card shows its tool count and exposes **Inspect Tools**
(opens the Interactive Tool Runner where you can call a tool with JSON arguments)
and **Toggle** (connect/disconnect). Use **Import/Export Config** to move your full
MCP setup between machines — the format is compatible with `mcp.json`.
