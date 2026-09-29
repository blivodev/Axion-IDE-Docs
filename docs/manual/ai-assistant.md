# AI Assistant

The Axion AI Assistant is the permanent chat tab. It streams responses token-by-token,
supports a message queue, and shows a live plan while autonomous work runs.

## Sending messages

Type in the composer and either press the **send button** or **Ctrl+Enter**
(plain Enter inserts a new line).

## Queueing while the agent works

While the agent is streaming, the send button turns **amber**. Clicking it (or
Ctrl+Enter) **queues** the message instead of dropping it:

- Queued messages appear in the **queue panel** above the composer:
  `N messages queued — sent automatically when the agent finishes`.
- Each queued message has three actions:
  - **➤ Send now** — jumps the queue (sent as soon as the current run ends)
  - **✎ Modify** — returns it to the composer for editing
  - **✕ Delete** — removes it; it will never be sent
- **↩ Undo last** takes the most recent queued message back into the composer.

## Streaming with your provider

Responses stream from your **enabled fallback tier** — the router sends the request
to the tier's model, endpoint, and API key automatically. See
[Fallback Tiers](fallback-tiers.md) to configure providers.

## The plan while it works

When the agent executes a DAG pipeline, the **Plan & Tasks** tab (first tab of the
diagnostics panel) shows:

- The plan goal (short header)
- One line per step with an **LED**: gray pending, orange running, green complete,
  red failed
- A progress line like `3 / 7 steps complete`

## Message history

Every conversation is stored in the encrypted vault. Open **History** in the icon
rail to browse and restore past sessions.
