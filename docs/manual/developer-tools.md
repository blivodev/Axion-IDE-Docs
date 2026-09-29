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

## Planned

- LSP (Language Server Protocol) client wiring per language — completion,
  diagnostics, and go-to-definition from open-source language servers.
- DAP debugging UI (breakpoints, watch, step) driving netcoredbg / debugpy / dlv.
- Docker dev-environments: run toolchains inside containers.
- Test runner integration and a TODO tree.

The editor core is AvaloniaEdit with an option to adopt an embedded web editor
later (changeable in Settings) — the LSP/DAP layers are editor-agnostic by design.
