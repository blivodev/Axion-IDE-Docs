# Getting Started

## Requirements

- Windows 10/11 (x64)
- No .NET runtime needed — the published build is self-contained

## Install

1. Download `Axion.App.exe` from the [releases page](https://github.com/blivodev/Axion-IDE/releases)
   (`publish/vX.Y.Z/win-x64-standalone/`).
2. Run it. That's it — the exe is fully self-contained.

## First launch

On first launch you get the Welcome Screen:

1. Click **Open Folder** and pick (or create) a workspace folder.
2. Axion opens the main window, starts a PowerShell terminal, indexes the project
   for semantic search, and loads your last open tabs.

## The layout

```text
+------+----------------------------------------+----------------+
| Icon |  Tab strip: [Axion AI Assistant][files]| Project        |
| rail +----------------------------------------+ Explorer       |
|      |  Center view (mode dependent)          | +--------------|
|      |                                        | | Terminal     |
|      |  Composer + icon toolbar at bottom     | | Context      |
+------+----------------------------------------+ | Usage / Logs |
                                                 +--------------+
```

- **Left icon rail** — switches center views (Assistant, DAG, MCP, Fallback, ...).
- **Right sidebar** — Project Explorer on top; Terminal / Context / Usage / Logs /
  Models / AC / Plan & Tasks tabs below.
- **Bottom status bar** — theme state, auto-continue caps, router profile, git branch.

## Configure an AI provider (do this first)

Chat needs at least one **fallback tier** with an API key:

1. Open **Fallback** in the icon rail (shield icon).
2. The default chain ships with **OpenRouter** as tier 1 — click **Edit**, paste your
   API key, and pick a model.
3. Send a chat message. Streaming now authenticates with your key automatically.

See [Fallback Tiers](fallback-tiers.md) for multi-tier failover.

## Keyboard shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+N` | New file |
| `Ctrl+O` | Open folder |
| `Ctrl+S` / `Ctrl+Shift+S` | Save / Save all |
| `Ctrl+Enter` (in composer) | Send or queue the prompt |
| `Ctrl+Shift+P` | Command palette |
| `Ctrl+M` (suggested) | Cycle workspace mode |

## Auto-save

Unsaved tabs show an **asterisk (*)**. Axion auto-saves:

- every **30 seconds**, and
- after **10 unsaved edits** in the active file.

Each auto-save is logged in **Logs**.
