# DAG Pipeline

The **Autonomous Sub-Agent Pipeline** runs a goal through a directed acyclic graph of
specialized sub-agents — Architect → Planner → Coder → Analyzer → Tester → Security →
Docs → Benchmark → Debugger → Stager.

## Running a pipeline

1. Open the **DAG** view (icon rail) or keep it inside the Assistant.
2. Optionally type a goal in the composer first — otherwise a default goal is used.
3. Click **Run Sub-Agent DAG**.

Each task **streams a real AI response** from the model assigned to its role (see
below), the repository context is compacted once per run and shared by all tasks,
and parsed diffs land on the task.

## Assigning models per execution mode

The **Per-Execution-Mode Model Assignment** card in the DAG view lists all 10 roles.
Each row is a dropdown of your **enabled fallback tiers** plus *Inherit from Auto
Router*:

- Pick a tier per role — e.g. Architect on Claude, Tester on the cheapest model.
- **Consolidate to one model** applies the first row to everything.
- **Apply to all** on a row spreads that row's model to every other role.

The mapping is logged when the run starts, and each task card shows its model as a
green badge.

## Watching the run

- The **Plan & Tasks** tab shows the live plan with LEDs per step.
- The DAG cards update: Pending → Running → Completed / Failed.
- **Logs** capture every transition, including the model each task ran on.
- A task whose upstream dependency failed is **skipped** with a clear reason.

## Pipeline modes

The **Mode** button cycles presets: FullAutonomous, StandardEngineering, FastPatch,
SecurityAndCompliance, DocumentationAndTests, Debugger, Custom. You can also build a
**Custom DAG** in the editor card and import/export pipelines as JSON.
