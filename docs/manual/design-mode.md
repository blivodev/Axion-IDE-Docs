# Design Mode (Visual UI Builder)

**Design Mode** is a WYSIWYG builder inside Axion. You drop widgets onto a canvas, edit
their settings, and export the result as **Avalonia XAML**, **HTML/CSS**, or **React** -
all from the same design.

## Opening it

Click the mode button in the top bar until it reads **DESIGN** (it cycles
ASSISTANT → DEVELOPER → DESIGN). The mode is remembered per workspace.

## The three panes

| Pane | What it does |
|------|--------------|
| **Widgets** (left) | The palette. Search it, or browse by category, then click a widget to add it. |
| **Design tree + Generated code** (centre) | The tree shows what is in your design; below it, the generated code updates live. |
| **Properties** (right) | Edit the selected widget's settings - its name, text, size, spacing, and so on. |

## Adding and arranging widgets

1. Click a widget in the palette (e.g. **Button**).
2. It lands **inside** the selected widget when that widget can hold children (like a
   Card or Stack Panel); otherwise it is added **next to** it.
3. Select a widget in the tree to edit it, or click **Delete Widget** to remove it.

The root widget can never be deleted - a design always needs a top box.

## The widget library

**56 widgets** ship across seven categories:

| Category | Examples |
|----------|----------|
| **Layout** | Stack Panel, Grid, Border, Card, Scroll Viewer, Expander, Split View, Wrap Panel |
| **Text** | Text, Heading, Paragraph, Label, Code Snippet, Markdown Preview, Link |
| **Inputs** | Button, Text Input, Password Field, Text Area, Check Box, Radio Group, Toggle Switch, Slider, Numeric Stepper, Search Box, Dropdown, Combo Box, Auto Complete, Tag Input, Date/Time/Colour/File Picker, Rating |
| **Display** | Image, Icon, Avatar, Chip, Progress Bar, Loading Spinner, Tooltip, Popover, Modal Dialog, Drawer, Toast, Alert Banner, Carousel, Map Embed |
| **Data** | List View, Tree View, Data Grid, Table, Timeline, Kanban Board, Calendar, Pagination, Breadcrumb |
| **Charts** | Stat Card, Line Chart, Bar Chart, Pie Chart, Sparkline |
| **Chrome** | Tabs, Accordion, Toolbar, Command Bar, Status Bar, Separator, Spacer |

## Exporting

Pick the target in the **Generated code** dropdown:

| Target | Output |
|--------|--------|
| **Avalonia** | A `UserControl` with real controls and `x:Name`s. |
| **Html** | A complete, self-contained page with mapped tags and inline styles. |
| **React** | A component function with mapped elements, props, and keys. |

Then either:

- **Copy Code** - puts the generated code on your clipboard, or
- **Open Code in Editor** - writes it to `.axion/designs/generated/` and opens it as a
  real editor tab, handing the design off to **Developer mode**.

## Saving and sharing

| Action | File |
|--------|------|
| **Save Design** | `.axdesign` in the workspace (`.axion/designs`) |
| **Save Widget** | `.axwidget` in the workspace (`.axion/widgets`) |

Both are plain JSON, so they can be read, diffed, versioned, and shared. A global
library folder (in your local app data) is also searched, so reusable widgets are
available in every project.

!!! tip "One tree, many targets"
    The design tree is the **source of truth**. The XAML, HTML, and React outputs are
    just different ways of writing the same tree down - so you never maintain three
    copies of the same UI.

## Custom widgets (Widget SDK)

You can add your own building blocks to the palette without a new version of Axion.
Write a small JSON package describing the widget, and it appears alongside the built-ins.

### The package format

```json
{
  "type": "RatingStars",
  "displayName": "Rating Stars",
  "category": "Custom",
  "description": "A row of stars to score something.",
  "author": "Your Name",
  "version": "1.0.0",
  "avaloniaControl": "StackPanel",
  "htmlTag": "div",
  "reactComponent": "Rating",
  "properties": [
    { "name": "Max", "type": "number", "defaultValue": "5" },
    { "name": "Value", "type": "number", "defaultValue": "3" }
  ]
}
```

| Field | Meaning |
|-------|---------|
| `type` | The internal name used in the design tree. Letters, digits, and underscores, starting with a letter. |
| `displayName` | The label shown in the palette. |
| `category` | Which palette group it joins (defaults to `Custom`). |
| `avaloniaControl` / `htmlTag` / `reactComponent` | How each renderer writes it out. Set at least one. |
| `properties` | The settings it understands. Types: `string`, `number`, `boolean`, `enum`. |

### Installing one

1. Open **Design Mode** and press **Widget SDK** in the action bar.
2. Press **Load Package…** and pick your `.axwidget` (or `.json`) file.
3. Axion validates it and shows the result. If it is valid, press **Install**.
4. The widget now appears in the palette - drop it on the canvas like any other.

**Rescan Folder** picks up every package in the workspace's `.axion/widgets` folder, so a
project can ship its own widgets.

### Validation

Axion checks a package before installing it, and explains any problem in plain English:

- missing `type` or `displayName`,
- a `type` that is not a safe name,
- a property with an unknown type,
- an `enum` property with no allowed values,
- two properties with the same name,
- a package that maps to no renderer at all.

A missing *individual* renderer mapping is only a **warning** - the renderers fall back to
a placeholder box, a `<div>`, or a `<div>` respectively.

!!! tip "Reinstalling replaces"
    Installing an updated version of the same `type` replaces the old one rather than
    adding a duplicate.