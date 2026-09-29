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

## Asking you questions (question cards)

When the agent needs a decision from you, it can ask right in the chat. Its reply
ends with a question card:

- **Numbered options** — each with a short description; the agent marks the one it
  **recommends**
- **Free-text box** — type your own answer instead
- **Skip** — dismiss the question

Click an option (or send typed text) and the conversation continues immediately; the
card collapses to `Answered: …` or `Question skipped.`

## The Axion Agent

The default agent driving all of this is **Axion Agent** — see
[Axion Agent](axion-agent.md) for its full capability set, default MCP toolkit, and
how to uninstall it.

## The composer toolbar

The row of icons under the prompt box is laid out in three groups:

| Position | Controls |
|----------|----------|
| **Left** | **Attach** (files/media/symbols) and **Skills & Agents** (toggle which skills and agents are injected into the prompt). |
| **Centre** | **Auto Continue**, **Auto Router**, and **Fallback** - each opens a flyout of presets plus a link to its full configuration view. |
| **Right** | **Context / Compact**, **Optimize prompt**, and **Send** (or the amber **Queue** button while the agent is busy). |

## Context / Compact

The **Context / Compact** icon on the right does two jobs:

- **Hover** it to see context usage at a glance.
- **Click** it to open a popup with:
  - a usage bar and the breakdown (system prompt, attached context, conversation
    history),
  - **Compact & compress this session now** - runs the active compactor over your
    pinned files and open tabs immediately, and folds older conversation turns into a
    single summary note. The popup reports exactly how many tokens were saved.
  - **Open Context & Budget…** - jumps to the full Context view.

!!! tip "Compact vs. usage"
    **Context usage** just *shows* you the numbers. **Compact** actually *changes* the
    session right away, making the next prompt smaller.

## New Session

The **New Session** icon sits in the chat header, immediately to the left of the active
DAG label. Click it to clear the conversation and start fresh.

## Message history