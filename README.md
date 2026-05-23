# marpit-themes

Custom theme CSS for [Marp for VS Code](https://marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode).

Hosted here so the raw URLs can be referenced from User `settings.json` and the themes become available globally across all VSCode windows (the extension does not support absolute local paths).

## Themes

| Name | Use for |
| --- | --- |
| `clean` | Minimalist white, serif headers — articles, reading-style decks |
| `dark` | Dark slate, cyan/amber accents — demos, screenshares |
| `consulting` | Off-white + red accent — Bain-leaning client decks |
| `mckinsey` | Charcoal/blue/gold — executive consulting style |
| `tech` | Monospace headers, code-forward — architecture/engineering |
| `pitch` | Bold large-type — covers, section transitions, single-message slides |

## Usage

In User `settings.json`:

```json
"markdown.marp.themes": [
  "https://raw.githubusercontent.com/Dev-Dipesh/marpit-themes/main/clean.css",
  "https://raw.githubusercontent.com/Dev-Dipesh/marpit-themes/main/dark.css",
  "https://raw.githubusercontent.com/Dev-Dipesh/marpit-themes/main/consulting.css",
  "https://raw.githubusercontent.com/Dev-Dipesh/marpit-themes/main/mckinsey.css",
  "https://raw.githubusercontent.com/Dev-Dipesh/marpit-themes/main/tech.css",
  "https://raw.githubusercontent.com/Dev-Dipesh/marpit-themes/main/pitch.css"
]
```

In a deck:

```yaml
---
marp: true
theme: mckinsey
paginate: true
---
```

## Slide-class variants

Several themes define per-slide variants — apply with `<!-- _class: <name> -->`:

- `clean`, `dark` — `title`
- `consulting`, `mckinsey` — `title`, `divider`, `takeaway`
- `tech` — `title`, `terminal`
- `pitch` — `cover`, `light`, `quote`
