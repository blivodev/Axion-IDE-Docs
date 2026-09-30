# Marketplace (Skills, Agents, Plugins)

The **Marketplace** (grid icon) is the in-app store for extending the agent:
skills, autonomous agents, MCP bridges, context compactors, and UI plugins — all
open source.

## Categories

The catalog is large — roughly 190 entries across five categories. The table below shows the
count and a representative sample of each; use the filter buttons at the top of the
Marketplace to browse a category in full.

| Category | Count | Examples |
|----------|-------|----------|
| **Skills** | 58 | TDD Specialist, Refactoring, API Design, SQL Optimization, Regex Wizard, Accessibility Audit, Git Workflow, Docs Writer, Domain-Driven Design, CQRS & Event Sourcing, GraphQL Schema, gRPC & Protobuf, OAuth & OIDC, Cryptography Review, Threat Modelling, OWASP Top 10, Load Testing, Chaos Engineering, Contract Testing, Property-Based Testing, Mutation Testing, Snapshot Testing, End-to-End Browser Testing, Accessibility Testing, Observability Design, SLO & Error Budget, Incident Response, Runbook Authoring, Cloud Cost Optimisation, Data Modelling, ETL & Data Pipeline, Event Streaming, Caching Strategy, Concurrency & Locking, Memory Profiling, API Versioning, Feature Flag, Monorepo Tooling, Docs-as-Code, Architecture Decision Records, Code Review, Legacy Code Rescue, Dependency Audit |
| **Autonomous Agents** | 49 | **Axion Agent** (default — installed), Claude (Anthropic), Antigravity (Google), Codex (OpenAI), Gemini (Google), DeepSeek Coder, Qwen Coder, OpenHands, Aider, SWE-Agent, Code Review, Legacy Migration, Performance Optimisation, Security Remediation, Documentation, API Reference, Test Gap, Flaky Test Hunter, Dead Code Removal, Dependency Upgrade, CVE Triage, Localisation, Accessibility Remediation, Database Schema, Query Optimisation, Infrastructure, Kubernetes, CI Pipeline, Release, Changelog, Pull Request Review, Issue Triage, Bug Reproduction, Codebase Onboarding, Architecture Review, Cloud Cost, Log Analysis, Postmortem, Compliance, SBOM, Refactoring, Docstring |
| **Compactors** | 34 | Repomix, Code2Prompt, Universal Ctags, Gitingest, Tree-sitter AST, Signature-Only, Diff-Only, Import Graph, Call Graph, Semantic Chunk, Embedding Rank, BM25 Keyword, Hybrid Retrieval, Cross-Encoder Rerank, Recursive Summariser, Hierarchical Summary, Rolling Window, Near-Duplicate, Whitespace Minifier, Comment Stripper, Test-Aware, Config, Schema, OpenAPI, Log, Stack Trace, Dependency List, Git History, Blame, Docs, Notebook, Binary Asset, Token Budget, Prompt Cache |
| **MCP Servers** | 3 | Blender, Chrome DevTools, GitHub bridges — see [MCP Servers](mcp-servers.md) for the full catalog of 400+ |
| **Plugins** | 47 | Media Converter (ffmpeg), Cryptography Toolkit, Image Compressor, JSON Schema Generator, .env Manager, Cron Scheduler, Markdown Exporter, Cron Expression Builder, JSONPath Explorer, YAML Tools, XML Tools, CSV Tools, Hash & Checksum, JWT Inspector, Timestamp Converter, Three-Way Merge, Regex Explainer, Text Statistics, Case Converter, Line Tools, Escape & Unescape, Placeholder Text, QR Code, SVG Optimiser, Icon Set Generator, Screenshot Annotator, Screen Recorder, Clipboard History, Scratch Notes, TODO Scanner, License Header, Environment Diff, Port Forwarding, Database Browser, API Mock Server, Load Simulation, Dependency Graph |

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