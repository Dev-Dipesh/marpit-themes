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
| `indigo` | IndiGo Airlines brand — navy/white with auto-branded wordmark, for IndiGo client decks |

## Usage

In User `settings.json`:

```json
"markdown.marp.themes": [
  "https://raw.githubusercontent.com/Dev-Dipesh/marpit-themes/main/clean.css",
  "https://raw.githubusercontent.com/Dev-Dipesh/marpit-themes/main/dark.css",
  "https://raw.githubusercontent.com/Dev-Dipesh/marpit-themes/main/consulting.css",
  "https://raw.githubusercontent.com/Dev-Dipesh/marpit-themes/main/mckinsey.css",
  "https://raw.githubusercontent.com/Dev-Dipesh/marpit-themes/main/tech.css",
  "https://raw.githubusercontent.com/Dev-Dipesh/marpit-themes/main/pitch.css",
  "https://raw.githubusercontent.com/Dev-Dipesh/marpit-themes/main/indigo.css"
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

Apply with `<!-- _class: <name> -->` on a slide:

- `clean`, `dark` — `title`
- `consulting`, `mckinsey` — `title`, `divider`, `takeaway`
- `tech` — `title`, `terminal`
- `pitch` — `cover`, `light`, `quote`
- `indigo` — `title` (light), `cover`, `cover-bleed`, `cover-geometric`, `cover-split`, `divider`, `takeaway`, `section`, `metric`, `split-h`

## Layout helpers

All themes ship the same grid helpers (require `markdown.marp.html: "all"`):

- `.cols` / `.cols-2` — two equal columns
- `.cols-3` — three equal columns

Indigo theme adds two more:

- `.cards` — 3-column card grid (image on top, title + body below). Each card uses `<div class="card">` containing an image + `<div class="body">` with `### Title` and body text.
- `.matrix` — 2x2 decision matrix. Each quadrant is `<div class="q">` (or `<div class="q alt">` for the alternate accent).

```html
<div class="cols">
<div>

## Left

</div>
<div>

## Right

</div>
</div>
```

For non-equal splits, inline the grid template: `<div class="cols" style="grid-template-columns: 2fr 1fr;">`.

## Image sizing (Marp native syntax)

Inside `![]` brackets:

- `![w:400](url)` — 400px wide
- `![w:50%](url)` — 50% of container width
- `![bg cover](url)` — full-slide background
- `![bg right 40%](url)` — right-side background occupying 40% of slide width

## Assets

The `assets/` directory holds image assets referenced by themes (currently the IndiGo theme).  Themes reference these via the same `raw.githubusercontent.com` URL pattern so they work without local files.

## Editing notes

- Themes are cached by the Marp extension. After pushing CSS changes, run **Marp: Clear Marp themes cache** in the VSCode command palette (or reload the window).
- For theme development, edit locally then push — the User `settings.json` URLs always point at `main`.
