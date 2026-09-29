# ELI5 Comment Convention

**Rule: every non-trivial member in the codebase carries an ELI5 comment, and the
comments are updated in the same change as the code.** This is a standing rule of
the project, not a suggestion.

## The rule

1. Every class, service, command handler, and non-obvious property gets an ELI5
   comment — one or two sentences a curious beginner would understand.
2. When you change behavior, **change the comment in the same commit**.
3. Comments explain *why and what for*, not just what the line does.

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

## Where it already applies

- Every service in `Axion.Infrastructure` (`SqliteEncryptedDatabase`,
  `HybridAiRouter`, `LibGit2SharpGitService`, ...)
- Every command and computed property in `WorkspaceViewModel`
- Every model with non-obvious semantics (`AgentTask.AssignedModel`,
  `ProviderLiveBalance`, `AppMode`, ...)
- Theme files, XAML regions, and generated docs

## Why

Axion is built to be read by future contributors (and by agents!) who were not in
the room when a decision was made. ELI5 comments are the cheapest way to keep the
whole system approachable — see the [Developer Wiki](architecture.md) for the
prose version of the same idea.
