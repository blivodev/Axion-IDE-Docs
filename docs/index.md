# Welcome to Axion IDE

**Axion IDE** is an AI-native code editor built with Avalonia and .NET. It pairs a full
coding environment with an autonomous AI agent that plans, executes, and verifies work —
locally on your GPU or in the cloud.

![Axion IDE](assets/axion-banner.png)

## The 30-second tour

| Area | What it does |
|------|--------------|
| **Axion AI Assistant** | Chat with the agent, queue messages, watch the plan execute |
| **DAG Pipeline** | Autonomous sub-agent pipeline — each role runs on the model you assign |
| **Fallback Tiers** | Multi-provider failover chain with API keys and live balances |
| **MCP Hub** | Connect Model Context Protocol servers (marketplace + GitHub installs) |
| **Marketplace** | Built-in catalog **plus** an external marketplace (Open VSX) that only offers what Axion can run |
| **Developer Tools** | Toolchain detection and one-click installs for compilers and debuggers |
| **Usage Analytics** | Token spend, credits, and live provider balances |
| **Report a Bug** | One-click pre-filled issues on GitHub or Gitea - and it opens itself when an error is thrown |

## Three workspace modes

The flat button in the top bar cycles the workspace between:

1. **ASSISTANT** — chat-first. The AI Assistant tab is permanent.
2. **DEVELOPER** — assistant closed, editor front and center.
3. **DESIGN** — visual UI builder: drop widgets, edit properties, export to Avalonia XAML, HTML, or React (see [Design Mode](manual/design-mode.md)).

The selected mode is saved **per workspace** and restored when you reopen it.

## Where to go next

- New here? Start with [Getting Started](manual/getting-started.md).
- Want to configure AI providers? Read [Fallback Tiers](manual/fallback-tiers.md).
- Hit a problem? See [Report a Bug](manual/report-a-bug.md).
- Curious how it works inside? The [Developer Wiki](dev/architecture.md) explains everything ELI5.
