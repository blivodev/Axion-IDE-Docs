# Marketplace (Skills, Agents, Plugins)

The **Marketplace** (grid icon) is the in-app store for extending the agent:
skills, autonomous agents, MCP bridges, context compactors, and UI plugins — all
open source.

## Categories

| Category | Examples |
|----------|----------|
| **Skills** | TDD Specialist, Refactoring, API Design, SQL Optimization, Regex Wizard, Accessibility Audit, Git Workflow, Docs Writer |
| **Autonomous Agents** | **Axion Agent** (default — installed), Claude (Anthropic), Antigravity (Google), Codex (OpenAI), OpenHands, Aider, SWE-Agent, Code Review agent |
| **Compactors** | Repomix, Code2Prompt, Universal Ctags, Gitingest |
| **MCP Servers** | Blender, Chrome DevTools, GitHub bridges |
| **Plugins** | Media Converter (ffmpeg), Cryptography Toolkit, Image Compressor, JSON Schema Generator, .env Manager, Cron Scheduler, Markdown Exporter |

## Installing

Click **Install** on any card. Installed items show a green badge.

## Using skills & agents

Installed skills and autonomous agents can be toggled into the agent's system prompt
from two places:

- The **Skills & Agents** sparkle icon in the composer toolbar (checkbox per item), or
- The Marketplace card toggle.

Enabled items are injected as directives on every prompt — e.g. the TDD skill
instructs the agent to write tests before code, and the **Axion Agent** contributes
its full capability playbook.

## The Axion Agent

**Axion Agent** is the first-party default agent — it ships installed and enabled,
and can be uninstalled or disabled at any time like any other item. See
[Axion Agent](axion-agent.md) for everything it can do.

## Primary compactor

For compactor entries, **Set as Primary** switches the workspace compactor used to
build prompt context (Repomix, Code2Prompt, Ctags, Gitingest, LSP Native). The
active one is shown in the composer's chip.

---

## External Marketplace (Open VSX)

Below the built-in catalog is the **External Marketplace** panel. It searches a real
external marketplace - **Open VSX** by default - and installs what it provides
automatically.

!!! warning "Only what Axion can actually run"
    Axion has **no VS Code extension host**. Rather than install something that would
    silently do nothing, every extension is inspected before it is offered. Anything
    needing webviews, custom editors, notebook renderers, debug adapters, custom
    side-bar views, walkthroughs, or the web extension host is marked
    **Not supported** with a plain-English reason, and its install button is disabled.

### What gets installed, and how

| Kind | What Axion does with it |
|------|-------------------------|
| **Language Server** | Unpacks it and launches its server over LSP. |
| **MCP Server** | Registers it as a tool bridge in the MCP Hub. |
| **Theme** | Converts its VS Code colours into Axion's 13 theme slots and applies it live. |
| **Snippets** | Imports its snippet files. |
| **Agent Skill** | Registers its instructions as a prompt directive. |

### Using it

1. Open the **Marketplace** view.
2. Type a search (e.g. `python`, `java`, `theme`, `mcp`) and press **Search**.
3. Each result shows its **kind**, a **Compatible / Not supported** badge, and the
   reason it was classified that way.
4. Click **Install** - Axion downloads the `.vsix`, unpacks it, and wires it up.

The **Compatible only** checkbox (on by default) hides unsupported extensions. Turn it
off to see them greyed out with the reason, so nothing is hidden from you.

!!! tip "Installs survive a restart"
    Installed extensions are saved to the encrypted vault and re-registered on the next
    launch, so your themes, language servers, and skills are still there.

Extensions are unpacked into `%LocalAppData%\AxionIDE\extensions\<publisher>.<name>`.
When an extension only publishes a build for another operating system or CPU, Axion
reports *"No compatible build for this platform"* instead of installing something that
cannot run.