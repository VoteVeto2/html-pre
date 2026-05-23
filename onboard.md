# Onboarding — Agent Harness Engineering Deck

If you've just been handed this folder, here's everything you need to edit or extend the presentation.

## 30-second tour

The deck is `presentation/index.html`. Open it in a browser, navigate with arrow keys. Done.

Everything else either fed the deck (the PDF, `summary.md`, `skill-briefing.md`) or supports it at runtime (`html-ppt-skill/`, `anthropic.css`).

## File map

| Path | What it is | Edit when… |
| --- | --- | --- |
| `[LR]Agent-Harness-Engineering.pdf` | Source paper | Never — input only |
| `summary.md` | Slide-by-slide content brief | You're changing what the slides *say* and want the brief to stay in sync |
| `skill-briefing.md` | Reference doc for the skill | Never — read it if confused |
| `html-ppt-skill/` | Skill repo (templates, base CSS, runtime JS, animations, fonts, 36 themes) | Never — keep pristine |
| `presentation/index.html` | The deck | You're rearranging slides, adding a slide, or tweaking copy |
| `presentation/anthropic.css` | The theme | You're changing colors, fonts, radii, shadows |

## How a slide works

The deck is one HTML file. Each slide is a `<section class="slide" data-title="...">` inside a `<div class="deck">`. `runtime.js` toggles the `.is-active` class so one slide shows at a time.

Canonical structure:

```html
<section class="slide" data-title="Slide Name">
  <div class="bg-grad bg-soft"></div>
  <div class="content">
    <span class="kicker">Section · 03</span>
    <h2 class="display">Big headline goes here</h2>
    <ul class="bullets">
      <li>Bullet one</li>
      <li>Bullet two</li>
    </ul>
    <div class="notes">Speaker notes — hidden on screen, surfaced via N drawer.</div>
  </div>
  <div class="deck-footer">…page chrome…</div>
</section>
```

To **add a slide**: copy any `<section class="slide">…</section>` block, swap the content, drop it in order, then update `data-total="16"` on every `.slide-number` if the count changed.

To **use a different layout**: browse `html-ppt-skill/templates/single-page/` — each file is a working example (cover, toc, bullets, two-column, kpi-grid, big-quote, comparison, process-steps, timeline, code, chart-bar, mindmap, …). Copy its slide block, strip `body.single` and `is-active`, drop in.

## The palette (Anthropic Warm)

Every color is a CSS variable in `presentation/anthropic.css`. Change a color globally by editing one line.

| Token | Hex | Name | Use |
| --- | --- | --- | --- |
| `--bg` | `#FAFAF7` | Ivory Light | Page background |
| `--surface` | `#F0F0EB` | Ivory Medium | Card surfaces |
| `--bg-soft` | `#E5E4DF` | Ivory Dark | Slide background tint |
| `--text-1` | `#191919` | Slate Dark | Primary text |
| `--text-2` | `#262625` | Slate Medium | Secondary text |
| `--text-3` | `#40403E` | Slate Light | Muted text |
| `--accent` | `#CC785C` | **Book Cloth** | **Primary accent — terracotta** |
| `--accent-2` | `#D4A27F` | Kraft | Secondary accent |
| `--accent-3` | `#EBDBBC` | Manilla | Tertiary accent / soft fill |
| `--border` | `#BFBFBA` | Cloud Light | Dividers |
| `--focus` | `#61AAF2` | Focus | Link hover and `:focus-visible` only |

Rule of thumb: **Book Cloth carries the energy.** Kraft and Manilla support it. Slate is the ink. Focus blue is a spice — don't sprinkle it everywhere.

## Common edits

- **Change the deck's title / footer text** — search `index.html` for `Agent Harness Engineering` and replace.
- **Swap colors** — edit `presentation/anthropic.css`. Nothing else needs to change.
- **Add or remove a slide** — copy a `<section class="slide">` block; update `data-total` on every footer.
- **Change a slide's content** — edit it directly in `index.html`. The matching entry in `summary.md` is for reference only — once you start editing the HTML, that's canonical.
- **Tweak typography** — edit the `--font-sans` / `--font-serif` / `--font-mono` / `--font-display` tokens in `anthropic.css`.
- **Rebuild from a new PDF** — drop the new PDF in this folder and re-run the 3-agent pipeline (see [`README.md`](README.md)).

## Runtime keybindings

| Key | Action |
| --- | --- |
| `←` `→` `Space` | Navigate |
| `Home` `End` | First / last slide |
| `N` | Speaker notes drawer |
| `S` | Presenter view (separate window) |
| `T` | Cycle themes (only `anthropic` installed here) |
| `F` | Fullscreen |

## Gotchas

- The deck loads CSS and JS via `../html-ppt-skill/assets/...`. **Don't move `presentation/` without keeping `html-ppt-skill/` as its sibling**, or asset paths will 404.
- All colors live in `anthropic.css`. **Don't hardcode hex codes in `index.html`** — the theme system stops working and `T`-cycle breaks.
- `summary.md` is a frozen snapshot of the brief that fed Agent 3. Edits to the deck don't sync back. Treat `index.html` as the source of truth once tweaking starts.
- The deck targets a 16:9 viewport. For projector use, hit `F` for fullscreen first.
