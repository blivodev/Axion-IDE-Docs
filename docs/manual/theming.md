# Theming

Axion ships with **12 pre-built themes**, hot-swappable from
**Settings → Theme & Typography Engine** — no restart needed.

## The themes

| Theme | Style |
|-------|-------|
| **Cherry Dark** (default) | Soft charcoal, restrained blue accent — Cherry Studio inspired |
| Obsidian Dark | Ultra-dark neutral with cyan accents |
| Deep Ocean | Deep blue-teal |
| Nord | Cool arctic blues |
| Dracula | Purple/pink classic |
| One Dark | Atom's One Dark |
| Tokyo Night | Neon night blues |
| Catppuccin Mocha | Pastel mocha |
| GitHub Dark | Familiar GitHub palette |
| High Contrast Dark | Maximum contrast accessibility |
| **Cherry Light** | Light counterpart of Cherry Dark |
| Solarized Light | Classic Solarized daylight |

## How theming works

Every theme defines the same **13 color slots** (backgrounds, borders, accents,
text tiers) plus the font stacks. Swapping a theme swaps one resource dictionary —
the entire UI re-skins instantly, and your selection is applied at startup.

Fonts are configurable too: **Inter** for UI (easy on the eyes) and a monospace
stack (Cascadia Code → JetBrains Mono → Consolas) for code, terminals, and the
Models/AC tabs.

## ELI5

Think of the theme as a bag of labeled paint cans (`AxionBgPanel`,
`AxionCyan`, ...). The whole UI is painted *by name*, never by hard-coded color.
A new theme just brings a different set of cans with the same labels.
