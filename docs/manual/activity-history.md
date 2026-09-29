# Activity History (Models & AC tabs)

Everything the agent does is recorded to a local SQLite database and surfaced in
two diagnostic tabs (right sidebar): **Models** and **AC**.

## Models tab

One card per AI call, color-coded:

- **Timestamp** (muted) · **Provider** (cyan) · **Model** (green)
- **in N tokens** (orange) · **out N tokens** · **~cost** (green)
- **Execution mode** and a short task description

## AC tab

One card per **auto-continue step**: timestamp, unique ID (`#a1b2c3d4`), execution
mode, and the action description.

## Persistence

Data lives in `%AppData%\AxionIDE\activity.db` (SQLite, WAL mode). History survives
restarts and is loaded when the app starts; the last 200 entries of each kind are
kept in memory for the tabs.

## Costs

Costs are **estimates** from a built-in per-model pricing table (per 1M tokens,
input/output). Unknown models fall back to a generic mid-tier rate. Manual
provider top-ups are recorded separately — see
[Usage Analytics](usage-analytics.md) for balances.
