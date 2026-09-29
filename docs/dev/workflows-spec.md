# Workflows (Specification)

**Status: execution wiring shipped** — the armed workflow's step chain is injected
into DAG pipeline tasks and auto-continue steps (v0.14.0+), with list selection
(v0.14.1) and role tags (v0.15.1). The freeform node canvas and marketplace sharing
are still ahead.

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

## Shipped so far

- **Workflows view** (sidebar): workflow list (new / delete / reload) + a
  **node-style vertical step editor** — every step is a node card with a connector
  arrow, editable Title, Tool/binary/model, Directive, Linked skill, and Linked
  DAG role.
- JSON save/load, add/remove/move steps, per-workspace + global libraries.
- **Arm for next run** (v0.14.0): the armed workflow's ordered steps, tools, skills,
  and role tags are injected into **every DAG task system prompt** and **every
  auto-continue step**; arming/disarming and DAG injection are logged.
- **Selection & highlights** (v0.14.1): click between saved workflows; the open one is
  highlighted, and the UI state never leaks into the shared JSON.
- **Role tags** (v0.15.1): a step's Linked DAG role is emitted as `[run as: …]` in the
  directive; `Inherit from Auto Router` stays untagged.

## Execution phases

1. ~~**Phase 1 — execution wiring**~~ **Shipped** (v0.14.0–v0.15.1): the armed
   workflow's steps are injected into DAG/Auto-Continue runs, carrying their tool,
   skill, and role tags.
2. **Phase 2 — node canvas**: freeform multi-branch graph (conditions, parallel
   branches) beyond the linear chain.
3. **Phase 3 — marketplace sharing** of workflows.

## Links to other features

- **Auto-Continue**: a workflow can drive what each continuation does.
- **DAG roles**: `LinkedRole` tags the step with the role that should own it (`[run as: …]`).
- **Skills**: `LinkedSkill` activates a marketplace skill for the step.
- **Tools**: `Tool` names binaries from the Tools marketplace.
