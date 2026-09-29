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

## Test runner

Axion detects your project's test framework and runs the tests, showing a tidy
pass/fail list instead of raw console noise.

| Framework | Command | Detected by |
|-----------|---------|-------------|
| **.NET** | `dotnet test` | `*.csproj`, `*.sln`, `*.slnx` |
| **pytest** | `python -m pytest -v` | `pytest.ini`, `pyproject.toml`, `tox.ini`, `test_*.py` |
| **Go** | `go test -v ./...` | `go.mod` |
| **Rust** | `cargo test` | `Cargo.toml` |
| **npm** | `npm test` | `package.json` |

### The Tests view

Open **Test Runner** in the icon rail. The header shows the detected framework and a
colour-coded scoreboard - **green** when everything passes, **red** when something
fails - with the run duration.

Press **Run Tests** and results stream in **live**, one row per test:

- a coloured status chip (**P** green pass, **F** red fail, **S** grey skip),
- the test's full name (`Suite.TestName`),
- the file it lives in, and
- how long it took.

**Click a failed test** to jump straight to its file.

**Detect Framework** re-scans the workspace (useful after adding a new test project),
and **Clear Results** empties the list.

!!! note "Frameworks are optional"
    Axion never bundles a test framework. If none is detected, the view says so and
    suggests adding a project file - nothing breaks.

## Dev containers

A **dev container** is a box with all the tools your project needs already installed, so
you do not have to set them up on your own machine. Axion reads your project's
`devcontainer.json` and can build, start, stop, and run commands inside it.

### Requirements

Axion checks for **Docker** or **Podman** - and it checks both that the command exists
*and* that the engine is actually running (Docker Desktop can be installed but stopped).
The Dev Containers view shows each runtime's status.

### The Dev Containers view

Open **Dev Containers** in the icon rail. It shows:

- **Container runtimes** - Docker and Podman with a status dot (green ready, amber
  installed-but-stopped, grey not installed).
- **Container spec** - what your `devcontainer.json` asks for: the image or Dockerfile,
  the workspace folder, and the forwarded ports.
- **Build & run log** - a live log while the container builds and starts.
- **Run in Container** - type a command (e.g. `dotnet test`) and run it inside the box.

### What Axion reads

| Field | Supported |
|-------|-----------|
| `image` | ? |
| `build` | ? both the plain-string and `{ "dockerfile": � }` forms |
| `workspaceFolder` | ? |
| `forwardPorts` | ? plain numbers and `"host:container"` strings |
| `containerEnv` | ? |
| `features` | ? listed |
| `postCreateCommand` | ? run after the container starts |

!!! tip "Comments are allowed"
    `devcontainer.json` permits `//` and `/* */` comments. Axion strips them before
    parsing, so a commented config works fine.

!!! note "Containers are optional"
    Axion never bundles a container runtime. If none is running, the view says so and
    suggests starting Docker Desktop - nothing breaks.

## Planned

Nothing outstanding in this area - the LSP client, debugger, test runner, and dev
containers have all shipped. See the [Design Mode spec](../dev/design-mode-spec.md)
for the remaining Widget SDK work.

The editor core is AvaloniaEdit with an option to adopt an embedded web editor
later (changeable in Settings) - the LSP/DAP layers are editor-agnostic by design.