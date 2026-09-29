# Extending the IDE

A walkthrough of the most common extension: adding a new feature area end-to-end.
Every step follows the project rules — ELI5 comments, tests green, version bump.

## The recipe: a new view + model + commands

Example: the **Developer Tools** view (toolchain detection + marketplace).

### 1. Model (Axion.Core)

```csharp
// src/Axion.Core/Models/ToolchainModels.cs
public partial class ToolchainInfo : ObservableObject
{
    public string Name { get; set; } = string.Empty;
    // ELI5: Green dot = the tool answered its --version command on this machine.
    [ObservableProperty] private bool _isDetected;
    [ObservableProperty] private string _version = string.Empty;
}
```

### 2. Interface (Axion.Core/Interfaces) — only when a service is needed

Add the interface + register the implementation in `App.axaml.cs`
(`services.AddSingleton<...>`) and inject it into `WorkspaceViewModel`.

### 3. ViewModel (WorkspaceViewModel.cs)

- `[ObservableProperty]` collections + computed properties
- `[RelayCommand]` methods that do the work
- Wire into `InitializeWorkspaceAsync` / the constructor init block

### 4. View (WorkspaceWindow.axaml)

- Add the enum value to `MainViewMode` (Core.Models.Workspace.cs)
- Add `IsXViewActive => ActiveMainView == MainViewMode.X` **and** the
  `[NotifyPropertyChangedFor]` on `_activeMainView`
- Add a `<Grid IsVisible="{Binding IsXViewActive}" RowDefinitions="Auto,...">`
  as a sibling view, and a sidebar button (`NeonSidebarButton`) with a click
  handler in the code-behind
- Update the **MainViewMode coverage test** (`AxionTests.cs`) — it counts modes!

### 5. DI + persistence

Services that store data go in `Axion.Infrastructure/Storage` with a SQLite table
created in `InitializeDatabase()`.

### 6. The checklist

```text
[ ] Model + interface + DI registration
[ ] VM properties/commands with ELI5 comments
[ ] View + sidebar entry + coverage test updated
[ ] dotnet build (0 warnings) + dotnet test (all green)
[ ] CHANGELOG entry + version bump across all 5 csproj + UI strings
[ ] Commit, push GitHub + Gitea, repomix, publish, prune publish/
```

## Other common extensions

| Want to add | Look at |
|-------------|---------|
| A new AI provider | `FallbackTiers` + `AiRouterOptions.Forced*` routing |
| A new DAG role | `AgentRole` enum, `MapRoleToAssignmentName`, `BuildRoleSystemPrompt`, `DagPipelineControl` |
| A new marketplace category | `MarketplaceCategory` + `InitializeMarketplaceCatalog` |
| A new diagnostic tab | `DiagnosticTabControl` in WorkspaceWindow.axaml |
| A new theme | Copy a `Themes/*.axaml`, add it to `ThemeManager` + Settings combo |
