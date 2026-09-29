# Fallback Tiers

Fallback tiers are your AI providers. They form an ordered failover chain, and the
**first enabled tier** is what chat streams from.

## The chain

Open the **Fallback** view (shield icon). Each tier shows:

- Provider + model
- Base URL (OpenAI-compatible endpoint)
- API key (stored in the encrypted vault)
- Timeout and per-tier enable toggle

Reorder tiers with the arrows, add tiers with **Add Fallback Tier**, and edit the
selected tier on the right. **Save Chain** persists the configuration.

## How routing uses the chain

- **Chat**: the first *enabled* tier receives the request directly — model, endpoint,
  and API key are all passed through, so streaming authenticates automatically.
- **DAG tasks**: each role uses the tier you assigned to it (see
  [DAG Pipeline](dag-pipeline.md)); *Inherit from Auto Router* defers to the router.
- If a request fails, the chain concept applies: later enabled tiers are the
  fallback targets.

## Chain presets

Save the current chain under a name (e.g. *Cheap nightly*, *Quality first*):

- **Save chain as preset** — stores every tier with its settings.
- **Apply to active chain** — swaps the live chain to a saved preset.
- Per **execution mode**, assign a different preset and optionally **pair it with
  Auto-Continue** — activating the mode then also switches the chain.

## Import / export

Chains round-trip as JSON: **Import Config** / **Export Config** in the header.
This makes it easy to share a provider setup between machines.
