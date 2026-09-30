# Developer Tools & Toolchains

Developer mode is only as good as the toolchains on your machine. The **Tools**
view (wrench icon) handles detection and installation.

## Detection

Opening the Tools view walks your PATH and asks each known toolchain for its version —
**76 of them**, covering languages, build systems, debuggers, cloud CLIs, and utilities.

- Green dot = ready, with the version string.
- Gray dot = not found.

Click **Re-detect** any time (e.g. after installing something new).

### Repair PATH

If a tool you just installed still shows as "not found", or `winget` is "not recognised" in
the integrated terminal, click **Repair PATH**.

This re-reads PATH from the Windows registry and pushes it into the running terminal. It is
needed because a desktop app inherits the environment it was launched with, which can predate
a PATH change — so a tool installed after Axion started is invisible until PATH is refreshed.
The status line reports how many entries were read and whether the WindowsApps folder (which
holds `winget`) is present.

## Installing tools

The **Tools Marketplace** lists open-source compilers, SDKs, and debug adapters with
one-click installs — **76 entries** across these groups:

- **Languages & runtimes** — .NET SDK 10, Node.js LTS, Python 3.12, Go, Rustup, JDK 21,
  Dart SDK, Ruby + DevKit, PHP, Kotlin, Swift, Perl, Lua, R, Julia, Deno, Bun, pnpm, Yarn
- **Compilers & build systems** — WinLibs GCC, LLVM/Clang, MSYS2, Zig, CMake, Ninja, Make,
  NASM, Yasm, GNU Binutils, Visual Studio Build Tools, Windows SDK
- **Debuggers & diagnostics** — GDB, LLDB, WinDbg, Sysinternals Suite, Process Monitor,
  debugpy (Python DAP), Delve (Go DAP)
- **Graphics & GPU** — DirectX Shader Compiler, Vulkan SDK, CUDA Toolkit, OpenCL Headers
- **Cloud & DevOps** — Docker Desktop, Podman, kubectl, Helm, Terraform, AWS CLI,
  Azure CLI, gcloud CLI
- **Databases** — PostgreSQL, SQLite, Redis
- **Networking** — Wireshark, Nmap, curl, wget, OpenSSH, PuTTY, MobaXterm, WinSCP
- **Storage & data** — rclone, Azure Storage Explorer, MinIO, DVC, MLflow, Ollama
- **Media & docs** — FFmpeg, ImageMagick, Pandoc, Mermaid CLI, Doxygen, Sphinx, MkDocs
- **Utilities** — ripgrep, jq, fd, bat, fzf, 7-Zip, Windows Terminal, PowerShell 7

Clicking **Install** runs the command (usually `winget install ...`) **in the integrated
terminal**, so you see every step. Nothing silent, nothing hidden.

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

The same problems are also **underlined in the editor itself** — red for errors, amber
for warnings, blue for information. **Hover a squiggle** to see the message and which
server reported it.

Below the list is a **language server status strip** showing each server and whether it
is running. A server that is not installed says so plainly rather than pretending your
code is clean.

### Completion (Ctrl+Space)

Put the caret where you want to type and press **Ctrl+Space**. Axion asks the language
server for suggestions and shows them in a popup:

- each row shows the suggestion's **kind** (Method, Class, Property, and so on) and its
  detail,
- **Up / Down** move the highlight,
- **Enter** or **Tab** inserts the highlighted suggestion,
- **Esc** closes the popup, and double-clicking a row also inserts it.

Suggestions are ranked against the word you have already typed: an exact match first,
then a name that starts with it (shorter wins), then a match in the middle, then
camelCase initials - so typing `gtn` finds `getTokenName`. Inserting replaces the word
you were typing and leaves the rest of the line alone.

### Folding ranges

The **Folding** tab lists every block the language server says can be collapsed — function
bodies, `if` blocks, comment runs — with how many lines each one hides:

```
[comment] lines 1-2   0 hidden
[block]   lines 4-7   2 hidden
[block]   lines 9-13  3 hidden
[block]   lines 10-12 1 hidden
```

Click a block to fold or unfold it, or use **Collapse All** / **Expand All**. Folded lines are
hidden in the editor; the start line stays visible so you can see where the block begins.

### Workspace symbols (Ctrl+T)

The **Symbols** tab searches the whole project for a symbol. Type part of a name and see every
matching function, class, or method — including ones in files you have never opened:

```
[Function] add      math.rs:1
[Function] add_all  math.rs:5
```

Clicking a row opens that file at that line. Results are ranked so an exact name match comes
first, then names starting with what you typed, then the rest.

### Outline

The **Outline** tab lists what is in the file you are editing — its structs, classes, methods,
fields, and functions — nested the way they are in the source:

```
[Struct] Point        4 lines
  [Field] x
  [Field] y
[Object] impl Point   5 lines
  [Method] sum
[Function] main       4 lines
```

Clicking a row jumps the editor to that line. The outline refreshes automatically when you
switch files, and there is a **Refresh** button.

### Format document (Shift+Alt+F)

Asks the language server to tidy up the whole file — indentation, spacing, and line breaks —
and writes the result. A status line tells you what happened: how many edits were applied,
`Already formatted — nothing to change`, or `No formatter available for this file type`.

### Signature help

While you type inside a function call, a hint appears above the caret showing the
signature and which parameter you are on:

```
fn add(a: i32, b: i32) -> i32   (parameter 1 of 2)
```

It appears when you type `(` or `,` and hides again when you type `)`, `;`, or a newline.
If a function has several overloads, the hint follows the one you are actually in.

### Code actions (Ctrl+.)

Put the caret on a problem and press **Ctrl+.** — Axion asks the language server what it
can do and lists the fixes it offers: *add the missing import*, *remove the unused
variable*, *insert the explicit type*. Each row shows whether it is a **Quick fix**, a
**Refactor**, or a **Source action**, and the server's preferred one is marked.

**Click a fix to apply it.** Open editor tabs reload afterwards, so you see the change
straight away.

### Rename symbol (F2)

Put the caret on a name and press **F2**. Type the new name and press **Preview** — Axion
asks the language server for a rename plan and shows **every file and every change** it
would make. Nothing is written until you press **Apply**.

A rename rewrites real code, so the preview exists to let you check it first. Open editor
tabs reload after a rename, so you see the new name straight away.

### Hover information

Rest the pointer on a name and Axion asks the language server what it is, showing the
answer as a tooltip — the type or signature plus any documentation the server has.

If the cursor is on a **problem** (a squiggle), you get the problem's message instead,
because that is more urgent than a description.

### Go to definition

Put the caret on a name and press **F12** (or **Ctrl+Click** it). Axion asks the language
server where that name is declared and opens the file at that line.

### Find references (Shift+F12)

Put the caret on a name and press **Shift+F12**. Axion lists every place that name is
used in the **References** tab of the diagnostics panel - including the declaration
itself. **Click a row** to jump straight to it.

!!! tip "The three editor gestures"
    **Ctrl+Space** completes, **F12** goes to the definition, **Shift+F12** finds
    references. All three need a language server running for the file type.

### Call hierarchy (Ctrl+Alt+H)

Put the caret on a function name and press **Ctrl+Alt+H**. The **Calls** tab shows two lists:

- **CALLED BY** — the functions that call this one
- **CALLS** — the functions this one calls

Each row says which line makes the call, and clicking it opens that file at that line. This
answers "if I change this, what breaks?" and "what does this actually do?" without you having
to search by hand.

### Inlay hints

The language server's inferred types are drawn inline as muted italic labels, so
`let x = 42;` shows `: i32` without you having to hover over it.

They are **off by default**, because they add visual noise and most people only want them
occasionally. Toggle them from the Hints panel.

### Semantic tokens

The language server tells the editor which words are variables, which are types, and which
are functions, and the editor colours them accordingly. This is more accurate than matching
text patterns, because the server actually understands the language — it can tell a type
named `Point` from a variable named `Point`.

This runs automatically when a file is open.

### Selection ranges (Alt+Up / Alt+Down)

Put the caret in some code and press **Alt+Up**: the selection grows outward one step at a
time — the caret, then the word, then the expression, then the statement, then the enclosing
block, then the whole function. **Alt+Down** steps back down.

This is the standard expand/shrink pair, and it is much faster than dragging to select a
whole block by hand.

!!! note "Servers are optional"
    Axion never bundles a language server. If one is missing, the Problems tab simply
    stays empty and the status strip shows the install hint - nothing breaks.

## Debugger (DAP)

Axion debugs your program through a real **debug adapter** — the same protocol VS Code
uses. Set a breakpoint, run, and inspect the call stack and variables.

There are **46 adapters**, covering these languages and runtimes:

| Group | Languages |
|-------|-----------|
| **Mainstream** | Python (debugpy), C# (netcoredbg), Go (Delve), Node.js, Rust (CodeLLDB / GDB) |
| **JVM** | Java (JDI), Kotlin (JDI), Scala |
| **Native** | C / C++ (GDB or LLDB), Zig, Assembly, Fortran, Swift (LLDB) |
| **Scripting** | Ruby (rdbg), PHP (Xdebug), Perl, Lua, R, Julia, MATLAB, Wolfram |
| **Web & mobile** | TypeScript (ts-node), Deno, Bun, Vue, Svelte, React Native, Electron, Tauri |
| **Game & 3D** | Unity, Godot (GDScript), Blender (Python) |
| **Functional** | Haskell, Elixir, Erlang, Clojure |
| **Shell & config** | PowerShell, Bash |
| **Infrastructure** | SQL (sqlite), Terraform, Ansible, Docker Compose, Kubernetes |

Each adapter names the file extensions it handles, so Axion picks the right one from the file
you have open. If the adapter's program is not installed, the view shows the install hint
instead of pretending debugging works.

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
| `build` | ? both the plain-string and `{ "dockerfile": → }` forms |
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