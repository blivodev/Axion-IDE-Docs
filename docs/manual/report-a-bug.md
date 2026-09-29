# Report a Bug

Axion makes it easy to tell the developers when something goes wrong - and it does most
of the paperwork for you.

## From the Help menu

**Help → Report a Bug…** opens the report dialog. Fill in:

- **Title** - a short summary (leave it blank and Axion borrows the first line of the
  error for you).
- **What happened?** - what you were doing, what you expected, what happened instead.
- **Error details (optional)** - paste a stack trace or error message if you have one.

The **environment is attached automatically**: Axion version, operating system, .NET
runtime, and the time of capture. You never have to look these up.

Then choose where to file it:

| Button | What it does |
|--------|--------------|
| **Open on GitHub** | Opens a pre-filled issue on the GitHub repository. |
| **Open on Gitea** | Opens a pre-filled issue on the Gitea mirror. |
| **Copy report** | Copies the whole report as Markdown, for pasting anywhere. |

Both tracker buttons open your browser with the **title and body already typed in** -
you only have to press **Submit**.

## When an error is thrown

If Axion hits an unexpected error, the same dialog **opens by itself** with the
exception type, message, and stack trace already filled in, plus a banner explaining
that the details were captured automatically.

This covers errors from:

- the **UI thread** (for example, a broken button handler),
- **background threads**,
- and **fire-and-forget tasks** that nobody was waiting on.

The app stays open so you can read the report and decide whether to send it - it no
longer disappears silently.

!!! tip "Nothing is sent without you"
    Axion never uploads anything on its own. The dialog only *prepares* a report; you
    review it and press Submit in your browser.

## Issue trackers

| Tracker | URL |
|---------|-----|
| GitHub | <https://github.com/blivodev/Axion-IDE/issues> |
| Gitea | <https://gitea.sektor9.dev/blivodev/Axion-IDE/issues> |

The **Help** menu also has **Open Issue Tracker (GitHub)** and **Open Issue Tracker
(Gitea)** to jump straight to the issue lists.
