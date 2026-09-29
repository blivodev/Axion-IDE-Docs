# Building & Debugging

## Build

```bash
dotnet build                       # Debug, all projects
dotnet build src/Axion.App -c Release
```

The suite must stay **100% green**: `dotnet test` (currently 41 tests).

## Run

```bash
dotnet run --project src/Axion.App
```

## Publish (self-contained exe)

```bash
dotnet publish src/Axion.App -c Release -r win-x64 --self-contained true \
  -p:PublishSingleFile=true -o publish/vX.Y.Z/win-x64-standalone
```

## Release checklist (repo rules)

1. Bump `<Version>` in **all 5 `.csproj` files**, plus the title/badge in
   `WorkspaceWindow.axaml`, `WelcomeWindow.axaml`, and the boot log + About dialog
   in the ViewModel/code-behind.
2. Add a `CHANGELOG.md` entry (Keep a Changelog format).
3. `dotnet test` — 100% green.
4. Commit, push to **GitHub** (`git push https://github.com/blivodev/Axion-IDE.git main`)
   and the Gitea mirror.
5. `npx repomix --style xml` to refresh the repository context pack.
6. Publish the exe into `publish/vX.Y.Z/win-x64-standalone/` and **delete all older
   release folders** — only the last two releases may exist in `publish/`.

## Debugging tips

- **Startup XAML crashes** (e.g. invalid `KeyGesture`) fail *after* the build —
  launch the exe and watch stderr; the stack trace names the exact axaml line.
- **XAML structure errors** show as AVLN errors at build time; validate nesting
  with an XML parser for the exact line.
- The boot log (`Logs` tab) and `SystemLogsText` carry `[TAG]`-prefixed lines for
  every subsystem (`[DAG]`, `[QUEUE]`, `[AUTOSAVE]`, `[GIT]`, `[TOOLS]`, ...).
- The activity database (`%AppData%\AxionIDE\activity.db`) is a ground truth for
  what the agent actually did.
