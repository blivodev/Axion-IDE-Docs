# Developer Tools & Toolchains

Developer mode is only as good as the toolchains on your machine. The **Tools**
view (wrench icon) handles detection and installation.

## Detection

Opening the Tools view walks your PATH and asks each known toolchain for its
version: **.NET, Node.js, Python, Go, Rust/Cargo, JDK, Dart, Ruby, GCC, Git**.

- Green dot = ready, with the version string.
- Gray dot = not found.

Click **⟳ Re-detect** any time (e.g. after installing something new).

## Installing tools

The **Tools Marketplace** lists open-source compilers, SDKs, and debug adapters
with one-click installs:

- .NET SDK 10, Node.js LTS, Python 3.12, Go, Rustup, JDK 21, Dart SDK,
  Ruby + DevKit, WinLibs GCC, Git, Docker Desktop
- Debug adapters: **debugpy** (Python DAP), **Delve** (Go DAP)
- Utilities: ripgrep

Clicking **⬇ Install** runs the command (usually `winget install ...`) **in the
integrated terminal**, so you see every step. Nothing silent, nothing hidden.

## Language servers (LSP)

Axion talks to real **language servers** for live diagnostics, completion, and
go-to-definition. Open a file and the right server starts automatically.

| Language | Server | Install |
|----------|--------|---------|
| C# | OmniSharp | omnisharp.net |
| Python | Pyright | `npm install -g pyright` |
| TypeScript / JavaScript | typescript-language-server | `npm install -g typescript typescript-language-server` |
| Go | gopls | `go install golang.org/x/tools/gopls@latest` |
| Rust | rust-analyzer | `rustup component add rust-analyzer` |
| Java | jdtls | Eclipse JDT Language Server |
| JSON / HTML / CSS | vscode-langservers-extracted | `npm install -g vscode-langservers-extracted` |
| Bash | bash-language-server | `npm install -g bash-language-server` |
| YAML | yaml-language-server | `npm install -g yaml-language-server` |
| Dockerfile | dockerfile-language-server-nodejs | `npm install -g dockerfile-language-server-nodejs` |

### The Problems tab

Every diagnostic the servers report lands in the **Problems** tab of the diagnostics
panel, with a colour-coded severity chip (red error, amber warning, blue info, grey
hint), the `file:line` location, the message, and which server said it. **Click a row
to jump straight to that line.**

Below the list is a **language server status strip** showing each server and whether it
is running. A server that is not installed says so plainly rather than pretending your
code is clean.

### Go to definition

Put the caret on a name and run **Go to Definition** (command palette). Axion asks the
language server where that name is declared and opens the file at that line.

!!! note "Servers are optional"
    Axion never bundles a language server. If one is missing, the Problems tab simply
    stays empty and the status strip shows the install hint - nothing breaks.

## Debugger (DAP)

Axion debugs your program through a real **debug adapter** - the same protocol VS Code
uses. Set a breakpoint, run, and inspect the call stack and variables.

| Language | Adapter | Install |
|----------|---------|---------|
| Python | debugpy | `pip install debugpy` |
| C# | netcoredbg | github.com/Samsung/netcoredbg |
| Go | Delve | `go install github.com/go-delve/delve/cmd/dlv@latest` |
| Node.js | node | nodejs.org |
| Rust | lldb-dap | Install LLVM / CodeLLDB |

### The Debug view

Open **Debugger** in the icon rail. The toolbar has **Debug**, **Continue**,
**Step Over / Into / Out**, **Pause**, **Toggle Breakpoint**, and **Stop**.

Three panes sit below it:

- **Breakpoints** - every breakpoint you have placed, with a red dot when on and grey
  when off. **Toggle Breakpoint** adds or removes one on the caret line.
- **Call stack** - the "how did we get here?" trail while paused. **Click a frame** to
  see the variables in that function.
- **Variables** - the values in the selected frame, grouped by scope (Locals, Globals),
  with a **debug console** underneath for adapter output.

!!! tip "Save before you debug"
    The debugger reads your file from disk, so Axion saves any unsaved changes in the
    active tab before starting a session.

!!! note "Adapters are optional"
    Axion never bundles a debug adapter. If one is missing, the Debug view says so and
    shows the install hint - nothing breaks.

## Planned

- Docker dev-environments: run toolchains inside containers.
- Test runner integration.

The editor core is AvaloniaEdit with an option to adopt an embedded web editor
later (changeable in Settings) - the LSP/DAP layers are editor-agnostic by design.