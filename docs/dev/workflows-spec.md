# Workflows (Specification)

**Status: groundwork shipped** (model, JSON persistence, node-style step editor).
Full visual canvas and execution wiring land in a future release.

## Goal

A **node-style visual page** where the user builds step chains the AI must follow —
which software, binary, or model to use per step, and what the AI should remember
and do at each step. Workflows connect to Auto-Continue, DAG roles, skills, and the
composer.

## Data model (shipped)

```json
{
  "Name": "Release Prep",
  "Description": "Verify, version, and ship",
  "Steps": [
    {
      "Title": "Build",
      "Tool": "dotnet build -c Release",
      "Directive": "Fix any compile error before continuing.",
      "LinkedSkill": "",
      "LinkedRole": "Inherit from Auto Router"
    }
  ]
}
```

- Stored as `*.workflow.json` in `<workspace>/.axion/workflows/` (workspace scope)
  and `%AppData%/AxionIDE/workflows/` (global library). Workspace wins by name.

## Shipped in the groundwork

- **Workflows view** (sidebar): workflow list (new / delete / reload) + a
  **node-style vertical step editor** — every step is a node card with a connector
  arrow, editable Title, Tool/binary/model, Directive, Linked skill, and Linked
  DAG role (which carries its assigned model).
- JSON save/load, add/remove/move steps, per-workspace + global libraries.

## Execution phases

1. **Phase 1 — execution wiring**: when a DAG/Auto-Continue run starts with a
   workflow selected, inject each step's directive into the system prompt in order
   and honor the step's tool/model.
2. **Phase 2 — node canvas**: freeform multi-branch graph (conditions, parallel
   branches) beyond the linear chain.
3. **Phase 3 — marketplace sharing** of workflows.

## Links to other features

- **Auto-Continue**: a workflow can drive what each continuation does.
- **DAG roles**: `LinkedRole` reuses the per-mode model assignment.
- **Skills**: `LinkedSkill` activates a marketplace skill for the step.
- **Tools**: `Tool` names binaries from the Tools marketplace.
