# Marketplace (Skills, Agents, Plugins)

The **Marketplace** (grid icon) is the in-app store for extending the agent:
skills, autonomous agents, MCP bridges, context compactors, and UI plugins — all
open source.

## Categories

| Category | Examples |
|----------|----------|
| **Skills** | TDD Specialist, Refactoring, API Design, SQL Optimization, Regex Wizard, Accessibility Audit, Git Workflow, Docs Writer |
| **Autonomous Agents** | Claude (Anthropic), Antigravity (Google), Codex (OpenAI), OpenHands, Aider, SWE-Agent, Code Review agent |
| **Compactors** | Repomix, Code2Prompt, Universal Ctags, Gitingest |
| **MCP Servers** | Blender, Chrome DevTools, GitHub bridges |
| **Plugins** | Media Converter (ffmpeg), Cryptography Toolkit, Image Compressor, JSON Schema Generator, .env Manager, Cron Scheduler, Markdown Exporter |

## Installing

Click **Install** on any card. Installed items show a green badge.

## Using skills

Installed skills can be toggled into the agent's system prompt from two places:

- The **Skills** sparkle icon in the composer toolbar (checkbox per skill), or
- The Marketplace card toggle.

Enabled skills are injected as directives on every prompt — e.g. the TDD skill
instructs the agent to write tests before code.

## Primary compactor

For compactor entries, **Set as Primary** switches the workspace compactor used to
build prompt context (Repomix, Code2Prompt, Ctags, Gitingest, LSP Native). The
active one is shown in the composer's 🗜️ chip.
