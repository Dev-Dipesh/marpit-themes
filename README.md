# marpit-themes

Custom theme CSS for [Marp for VS Code](https://marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode).

Hosted here so the raw URLs can be referenced from User `settings.json` and the themes become available globally across all VSCode windows (the extension does not support absolute local paths).

## Themes

| Name | Use for |
| --- | --- |
| `clean` | Minimalist white, serif headers — articles, reading-style decks |
| `dark` | Dark slate, cyan/amber accents — demos, screenshares |
| `consulting` | Off-white + red accent — Bain-leaning client decks with reusable business layouts |
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
- `consulting` — `title`, `divider`, `takeaway`, `section`, `metric`, `split-h`, `cta`
- `mckinsey` — `title`, `divider`, `takeaway`
- `tech` — `title`, `terminal`
- `pitch` — `cover`, `light`, `quote`
- `indigo` — `title` (light), `cover`, `cover-bleed`, `cover-geometric`, `cover-split`, `divider`, `takeaway`, `section`, `metric`, `split-h`

## Layout helpers

All themes ship the same grid helpers (require `markdown.marp.html: "all"`):

- `.cols` / `.cols-2` — two equal columns
- `.cols-3` — three equal columns

Indigo and consulting themes add:

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

## Consulting layout helpers

The `consulting` theme includes additional client-deck layouts so decks need minimal inline CSS. These require `markdown.marp.html: "all"`.

- `.glance-grid` + `.glance-card` — compact 4-column summary grid. Use `.glance-card.alt` for black accent cards.
- `.metric-row` + `.metric` — 4-column numeric KPI row with `.num` and `.label`.
- `.sequence-grid` + `.sequence-card` — two-card sequence or phase layout. Use `.step-num` for large numbers and `.sequence-card.alt` for black accent.
- `.split-emphasis` + `.dark-box` + `.support-panel` — asymmetric contrast layout with one dark anchor panel and one white detail panel.
- `.gate-matrix` — two-column dependency/risk matrix with `.head` and `.area` cells.
- `.role-card-grid` + `.role-card` — two compact role/responsibility cards. Use `.role-card-title` for the card heading and `.role-card.alt` for black accent.
- `.case-evidence` + `.case-claim` + `.evidence-grid` + `.evidence-list` + `.relevance-band` — case-study evidence slide with a bottom relevance band.
- `.verification-layout` + `.check-panel` + `.check-row` + `.check-mark` — checklist plus contrast panel layout.
- `.cta-panel` + `.cta-metrics` + `.cta-metric` + `.cta-next` — strong final decision / call-to-action slide content, usually with `<!-- _class: cta -->`.
- `.callout` — red left-rule callout.
- `.diagram` — centered diagram container sized for large architecture images.
- `.small`, `.tight` — utility classes for dense text slides.
- `.corner-mark` — absolutely positioned decorative or brand image for title slides.

Example CTA slide:

```markdown
<!-- _class: cta -->

# Approve the 12-Week First Engagement

<div class="cta-panel">
<p>Decision requested: proceed with the revised SOW response.</p>
</div>

<div class="cta-metrics">
<div class="cta-metric"><strong>12 weeks</strong><span>Kickoff to readout</span></div>
<div class="cta-metric"><strong>INR 26L</strong><span>Professional fee</span></div>
<div class="cta-metric"><strong>1 built pilot</strong><span>End-to-end evidence</span></div>
<div class="cta-metric"><strong>1 guided pilot</strong><span>Client-led build path</span></div>
</div>
```

Example split-emphasis slide:

```html
<div class="split-emphasis">
<div class="dark-box">

## Primary Offer

One workstream is delivered end-to-end.

</div>
<div class="support-panel">

## Supporting Work

- Architecture and design docs
- Implementation plan
- Risk profile

</div>
</div>
```

To override the consulting accent color for a client deck, set the CSS variable once near the top of the deck:

```html
<style>
section {
  --consulting-red: #C00000;
}
</style>
```

## Per-slide image override (indigo `cover-split`)

The `cover-split` variant exposes two CSS variables so you can swap the right-column image without editing the theme:

```markdown
<!-- _class: cover-split -->

<style scoped>
section {
  --split-image: url('https://example.com/your-image.jpg');
  --split-image-x: -120px;   /* horizontal offset to center the subject */
}
</style>

# Slide title

Subtitle text on the left
```

Tune `--split-image-x` until the subject of your image lands centered in the right column (negative pulls left, positive pulls right).

## Native Marp directives for ad-hoc layouts

For one-off slides that don't need a theme class, use Marp's built-in syntax:

- `![bg right](url)` — image fills right half
- `![bg left](url)` — image fills left half
- `![bg right 40%](url)` — image fills right 40%
- `<!-- _backgroundColor: #001B94 -->` — solid background color per slide
- `<style scoped>` — arbitrary per-slide CSS (great for two-color splits, custom backgrounds, etc.)

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
