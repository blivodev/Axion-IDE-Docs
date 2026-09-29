# Usage Analytics

The **Usage** view shows where your tokens and money go — all computed from the
persistent activity history (also visible in the **Models** tab).

## Breakdowns

Four grouped summaries, each with calls, input/output tokens, and estimated cost:

- **By provider** — e.g. OpenRouter vs local GPU
- **By model** — e.g. `anthropic/claude-3.7-sonnet` vs `gpt-4o-mini`
- **By day** — `2026-09-28` buckets
- **By month** — `2026-09` buckets

A **search box** filters everything by provider, model, execution mode, or task
description. A **Sort** selector orders groups by Cost, Calls, Tokens, or Name.

## Credits and balances

- **+ Add Credit** records a manual top-up (e.g. `$20` for OpenRouter) — persisted
  locally.
- The balance table shows per provider: credits added, estimated spend, and the
  **remaining balance** (color-coded).
- **⟳ Live Balance** fetches the *actual* remaining credit from a provider API.
  Currently supported: **OpenRouter** (`GET /v1/credits`, using the API key stored
  on its enabled fallback tier). More providers can be added as they expose
  endpoints.

## Where the data comes from

Every AI call records: timestamp, provider, model, input/output tokens, estimated
cost (built-in per-model pricing table), execution mode, and router profile. Every
auto-continue step records its unique ID and action. Everything persists in a local
SQLite database (`activity.db`) — see the **Models** and **AC** tabs.
