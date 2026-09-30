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

Every theme defines the same **26 colour slots** plus the font stacks. Swapping a theme swaps
one resource dictionary — the entire UI re-skins instantly, and your selection is applied at
startup.

The slots fall into four groups:

| Group | Slots | What they cover |
|-------|-------|-----------------|
| **Surfaces** | `Surface0`–`Surface3` | A four-step elevation scale: app background, panel, raised/input, hover/selected. Each theme derives its steps from its own background, so the scale stays consistent per theme — and light themes step *darker* for elevation, which is the correct direction on a light background. |
| **Accents** | `AxionCyan`, `AxionNeonGreen`, `AxionNeonRed`, `AxionNeonPurple`, `AxionNeonOrange` | The primary accent plus status colours. Deliberately muted rather than neon — a saturated cyan/purple/green trio is the signature of an AI-generated dashboard. |
| **Semantic** | `OnAccent`, `SuccessTint`, `WarningTint`, `ErrorTint`, `InfoTint` | Text that sits *on* a coloured button, and the tinted backgrounds behind success / warning / error / info banners. |
| **Navigation** | `NavHover`, `NavPressed`, `NavActive`, `NavIcon` | The left navigation strip's hover, pressed, active, and icon colours. |

There are also text tiers (`TextPrimary`, `TextSecondary`, `TextMuted`) and border slots
(`Border`, `BorderHover`).

**No colour is hard-coded anywhere in the UI.** Every view and control paints by name, so
switching theme re-skins everything — panels, cards, inputs, banners, and the navigation
strip alike.

### Typography

The UI uses the **operating system's own interface font** — `Segoe UI Variable Text` on
Windows 11, falling back to `Segoe UI`, then `system-ui`. Axion deliberately does not bundle
a custom UI font, so it looks like a native desktop program rather than a web page.

Code, terminals, and the Models/AC tabs use a monospace stack: **Cascadia Code → JetBrains
Mono → Consolas**.

## ELI5

Think of the theme as a bag of labeled paint cans (`AxionSurface1`, `AxionCyan`, ...). The
whole UI is painted *by name*, never by hard-coded colour. A new theme just brings a
different set of cans with the same labels.

That is why switching theme changes everything at once: nothing in the app knows what colour
it is, it only knows which can to reach for.
