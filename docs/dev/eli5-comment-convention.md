# ELI5 Comment Convention

**Rule: every non-trivial member in the codebase carries an ELI5 comment, and the
comments are updated in the same change as the code.** This is a standing rule of
the project, not a suggestion.

## The rule

1. Every class, service, command handler, property, and non-obvious block gets an ELI5
   comment — one or two sentences a curious beginner would understand.
2. **XAML counts too.** Every window and custom control opens with an ELI5 comment
   describing its layout or purpose.
3. When you change behavior, **change the comment in the same commit**.
4. Comments explain *why and what for*, not just what the line does.

## Format

```csharp
/// <summary>
/// ELI5: The fallback tiers are your AI providers in a queue. If the first one
/// fails or is too expensive, the next one takes over — like backup singers.
/// </summary>
public ObservableCollection<FallbackTierItem> FallbackTiers { get; }
```

For inline logic:

```csharp
// ELI5: After 10 un-saved edits we save automatically, so work is never more
// than a few seconds from disk. The tab shows an asterisk until then.
public void RegisterEditorChange()
```

## Coverage

Coverage is **100%**: every `.cs` and `.axaml` file under `src/` and `tests/` contains
at least one ELI5 comment (603 comments at the time of writing). Audit before you
commit:

```powershell
Get-ChildItem -Recurse -File -Include *.cs,*.axaml -Path src,tests |
  Where-Object { $_.FullName -notmatch '\\(bin|obj)\\' } |
  Where-Object { (Get-Content $_.FullName -Raw) -notmatch 'ELI5' } |
  Select-Object FullName
```

An empty result means full coverage.

## Where it applies

- Every service in `Axion.Infrastructure` (`SqliteEncryptedDatabase`,
  `HybridAiRouter`, `LibGit2SharpGitService`, `OpenVsxMarketplaceService`,
  `BugReportService`, ...)
- Every command and computed property in `WorkspaceViewModel`
- Every model with non-obvious semantics (`AgentTask.AssignedModel`,
  `ProviderLiveBalance`, `AppMode`, `AutoContinueConfiguration`, ...)
- Every window and custom control in `Axion.App` (`WorkspaceWindow.axaml`,
  `BugReportWindow.axaml`, `TwoColorDiffControl.axaml`, ...)
- Theme files and generated docs

## Why

Axion is built to be read by future contributors (and by agents!) who were not in
the room when a decision was made. ELI5 comments are the cheapest way to keep the
whole system approachable — see the [Developer Wiki](architecture.md) for the
prose version of the same idea.
