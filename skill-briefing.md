# html-ppt-skill — Briefing for HTML Authoring Agent

## Repo location (local)
/Users/veto/Documents/git/html-pre/html-ppt-skill

Cloned successfully from https://github.com/lewislulu/html-ppt-skill.

## TL;DR — How to author a deck with this skill

A deck is a **single HTML file** containing one `<div class="deck">` with multiple `<section class="slide" data-title="...">` children. Each slide is one logical page; `assets/runtime.js` toggles `.is-active` between them and binds keyboard navigation (`← →`, `T` cycles themes, `S` opens presenter window, `O` overview). All visual style comes from CSS variables defined in `assets/base.css` and overridden by **one** theme file in `assets/themes/<name>.css` (36 themes available). Authoring is copy-paste: open `templates/single-page/<layout>.html`, copy the `<section class="slide">…</section>` block into your deck, replace the demo content, set `data-title`, add `<div class="notes">` for speaker notes. Do **not** invent layouts or use raw hex colors — always start from a template and use tokens like `var(--text-1)`, `var(--accent)`. Every deck must link `fonts.css`, `base.css`, one theme, `animations.css`, and `runtime.js`.

## Key files (with absolute paths and one-line purpose)

- /Users/veto/Documents/git/html-pre/html-ppt-skill/SKILL.md — agent-facing dispatcher with the full skill spec (verbatim copy below)
- /Users/veto/Documents/git/html-pre/html-ppt-skill/README.md — long-form overview of what ships in the box (36 themes, 31 layouts, 47 animations)
- /Users/veto/Documents/git/html-pre/html-ppt-skill/templates/deck.html — **the minimal 6-slide starter to copy from** (the canonical pattern)
- /Users/veto/Documents/git/html-pre/html-ppt-skill/examples/demo-deck/index.html — complete 8-slide working deck (best end-to-end reference with charts + notes)
- /Users/veto/Documents/git/html-pre/html-ppt-skill/assets/base.css — design tokens + slide system + typography primitives (do NOT edit per deck)
- /Users/veto/Documents/git/html-pre/html-ppt-skill/assets/runtime.js — keyboard runtime (arrows, T, S, O, N, F, A, hash deep-links, BroadcastChannel sync)
- /Users/veto/Documents/git/html-pre/html-ppt-skill/assets/fonts.css — Google Fonts imports (Inter, Noto Sans/Serif SC, JetBrains Mono, Playfair Display, etc.)
- /Users/veto/Documents/git/html-pre/html-ppt-skill/assets/animations/animations.css — 27 CSS entry animation classes (`anim-fade-up`, `anim-rise-in`, `anim-stagger-list`, etc.)
- /Users/veto/Documents/git/html-pre/html-ppt-skill/assets/animations/fx-runtime.js — auto-init for `[data-fx]` canvas effects
- /Users/veto/Documents/git/html-pre/html-ppt-skill/assets/themes/ — 36 theme CSS files; pick ONE for `<link id="theme-link">`
- /Users/veto/Documents/git/html-pre/html-ppt-skill/templates/single-page/ — 31 layout files (cover, toc, bullets, two-column, kpi-grid, code, timeline, big-quote, stat-highlight, cta, thanks, etc.). Copy `<section class="slide">` blocks out of these.
- /Users/veto/Documents/git/html-pre/html-ppt-skill/templates/full-decks/ — 15 self-contained multi-slide template folders with scoped `.tpl-<name>` CSS (e.g. `tech-sharing/`, `pitch-deck/`, `product-launch/`, `presenter-mode-reveal/`)
- /Users/veto/Documents/git/html-pre/html-ppt-skill/references/authoring-guide.md — step-by-step workflow from outline to render
- /Users/veto/Documents/git/html-pre/html-ppt-skill/references/themes.md — all 36 themes with "when to use" guidance
- /Users/veto/Documents/git/html-pre/html-ppt-skill/references/layouts.md — catalog of all 31 layouts
- /Users/veto/Documents/git/html-pre/html-ppt-skill/references/animations.md — 27 CSS + 20 canvas FX catalog
- /Users/veto/Documents/git/html-pre/html-ppt-skill/scripts/new-deck.sh — scaffolds a new deck folder under `examples/<name>/index.html`
- /Users/veto/Documents/git/html-pre/html-ppt-skill/scripts/render.sh — headless Chrome → PNG export

## Slide markup pattern

Canonical deck shell (from `templates/deck.html`, paths shown for a deck saved at `examples/my-talk/index.html`):

```html
<!DOCTYPE html>
<html lang="zh-CN" data-theme="minimal-white">
<head>
<meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<title>html-ppt · Deck</title>
<link rel="stylesheet" href="../../assets/fonts.css">
<link rel="stylesheet" href="../../assets/base.css">
<link rel="stylesheet" id="theme-link" href="../../assets/themes/minimal-white.css">
<link rel="stylesheet" href="../../assets/animations/animations.css">
</head>
<body data-themes="minimal-white,editorial-serif,soft-pastel,arctic-cool,sunset-warm,catppuccin-mocha,tokyo-night,aurora,xiaohongshu-white,neo-brutalism" data-theme-base="../../assets/themes/">
<div class="deck">

  <!-- 1. Cover -->
  <section class="slide" data-title="Cover">
    <p class="kicker">html-ppt · 2026</p>
    <h1 class="h1 anim-fade-up" data-anim="fade-up">用模板,<span class="gradient-text">换主题</span><br>讲任何事情</h1>
    <p class="lede">24 themes · 30 layouts · 25 animations · zero build</p>
    <div class="deck-footer"><span class="dim2">lewis</span><span class="slide-number" data-current="1" data-total="6"></span></div>
    <div class="notes">这是一个最小可用的 deck。你可以复制这个文件作为新 deck 的起点。</div>
  </section>

  <!-- 2. TOC -->
  <section class="slide" data-title="目录">
    <p class="kicker">Agenda</p>
    <h2 class="h2">我们会讲三件事</h2>
    <div class="grid g3 mt-l anim-stagger-list" data-anim-target>
      <div class="card"><h4>01 · Tokens</h4><p class="dim">把颜色/字体/圆角收进 CSS 变量。</p></div>
      <div class="card"><h4>02 · Layouts</h4><p class="dim">30 种可复用单页。</p></div>
      <div class="card"><h4>03 · Runtime</h4><p class="dim">键盘驱动、按 T 换主题。</p></div>
    </div>
  </section>

  <!-- ...more <section class="slide">... blocks copied from templates/single-page/ ... -->

</div>
<script src="../../assets/runtime.js"></script>
</body></html>
```

**Required structural rules:**
- One outer `<div class="deck">`; runtime fails silently if missing.
- One `<section class="slide" data-title="...">` per page.
- The first slide does NOT need `is-active` when the runtime is loaded; `runtime.js` calls `go(0)` on boot and sets it automatically. (Single-page layout files use `body class="single"` + `<section class="slide is-active">` to render standalone for previewing.)
- Per-slide `<div class="notes">…</div>` for speaker notes (hidden visually, surfaced via N drawer and S presenter window).
- Optional `.deck-header` / `.deck-footer` / `.slide-number` chrome inside each slide; the `data-current` / `data-total` on `.slide-number` get auto-updated.
- Animations: put `data-anim="fade-up"` on an element so it re-triggers on slide entry. Use `class="anim-stagger-list"` on a `<ul>` or `.grid` for sequenced child reveals; set `data-anim-target` to hint the runtime.
- For Chart.js/highlight.js, load via CDN in `<head>`; init inside `DOMContentLoaded` and read CSS vars (`getComputedStyle(document.documentElement).getPropertyValue('--accent')`) so charts pick up the active theme.

## Theming hooks

All design tokens live as CSS custom properties on `:root` in `assets/base.css`. Each theme file in `assets/themes/<name>.css` is just an `:root { ... }` override (plus optional decorative additions). The full token list every theme defines:

```
--bg, --bg-soft, --surface, --surface-2,
--border, --border-strong,
--text-1, --text-2, --text-3,
--accent, --accent-2, --accent-3,
--good, --warn, --bad,
--grad, --grad-soft,
--radius, --radius-sm, --radius-lg,
--shadow, --shadow-lg,
--font-sans, --font-serif, --font-mono, --font-display,
--letter-tight, --letter-normal, --ease
```

**To inject a custom palette (e.g. Anthropic brand colors):**

Option A — drop in a new theme file at `/Users/veto/Documents/git/html-pre/html-ppt-skill/assets/themes/anthropic.css`:

```css
/* theme: anthropic */
:root{
  --bg:#FAF9F5;            /* Anthropic cream/off-white */
  --bg-soft:#F0EEE6;
  --surface:#FFFFFF;
  --surface-2:#F0EEE6;
  --border:rgba(40,40,40,.08);
  --border-strong:rgba(40,40,40,.18);
  --text-1:#1F1F1E;
  --text-2:#5C5C5A;
  --text-3:#8E8D87;
  --accent:#D97757;        /* Anthropic clay/coral */
  --accent-2:#CC785C;
  --accent-3:#B8593E;
  --grad:linear-gradient(135deg,#D97757,#CC785C 55%,#B8593E);
  --grad-soft:linear-gradient(135deg,#FAEDE7,#F5DDD2 55%,#EFC8B8);
  --radius:18px;--radius-sm:12px;--radius-lg:26px;
  --shadow:0 10px 30px rgba(18,24,40,.06);
  --shadow-lg:0 24px 60px rgba(18,24,40,.10);
  --font-sans:'Inter','Noto Sans SC',sans-serif;
  --font-serif:'Playfair Display','Noto Serif SC',Georgia,serif;
  --font-mono:'JetBrains Mono',SFMono-Regular,Menlo,monospace;
}
```

Then point `<link id="theme-link" href="../../assets/themes/anthropic.css">`. The whole deck reskins.

Option B (when inlining everything into a single portable HTML) — put a `<style>` block in `<head>` with `:root { --bg:#FAF9F5; --accent:#D97757; ... }` AFTER the inlined `base.css`, and skip the theme link. Same effect.

**Per-slide overrides:** you can set `style="--accent:#xxx"` directly on a `.slide` to recolor just that page. The Anthropic palette commonly used: cream `#FAF9F5`, ink `#1F1F1E`, clay `#D97757`.

## Navigation / runtime

`assets/runtime.js` is loaded once at the end of `<body>`. Zero dependencies. It auto-wires:

- **Arrows / Space / PgUp / PgDn / Home / End** — navigate between `.slide` elements (toggles `.is-active`)
- **F** — fullscreen
- **S** — opens a separate presenter window with 4 draggable cards (CURRENT preview iframe, NEXT preview iframe, SPEAKER SCRIPT, TIMER); audience+presenter sync via `BroadcastChannel`
- **N** — bottom notes drawer (shows current slide's `<div class="notes">`)
- **O** — overview grid (mini-thumb of every slide, click to jump)
- **T** — cycle through themes listed in `<body data-themes="a,b,c">` (requires `data-theme-base` pointing at the themes directory)
- **A** — cycle a demo animation on the current slide
- **R** — reset timer (only inside presenter window)
- **Esc** — close overlays
- **URL hash `#/N`** — deep-link to slide N (1-based)
- **URL `?preview=N`** — preview-only mode (single slide, no chrome) — used internally by the presenter window iframes
- Progress bar at the bottom auto-injected
- Animations: any element with `data-anim="..."` gets its `anim-<name>` class re-applied on each slide entry so the entry effect plays every time you navigate onto the page
- Counters: `<span class="counter" data-to="92">0</span>` animates 0→target on slide entry

The runtime also assumes the theme link has `id="theme-link"` (for T-cycling) and that `data-theme-base` on the `<body>` (or `<html>`) points to the directory containing the theme `.css` files.

## Required asset paths

The skill's intended layout is **NOT a single self-contained file**. The default authoring pattern is:

- Deck file lives at `examples/<deckname>/index.html` (or copy a full-deck template folder like `templates/full-decks/tech-sharing/`)
- It links shared assets via relative paths: `href="../../assets/fonts.css"`, `href="../../assets/base.css"`, `href="../../assets/themes/<theme>.css"`, `href="../../assets/animations/animations.css"`, `src="../../assets/runtime.js"`
- `data-theme-base="../../assets/themes/"` on `<body>` so the T key can swap themes
- For full-decks at `templates/full-decks/<name>/index.html` the paths are `../../../assets/...` (one extra `../`)

**If portability is required (single .html that opens anywhere with no sibling files):**

1. Copy the relevant CSS files inline. Required order in `<head>`:
   - `assets/fonts.css` (or inline the Google Fonts `@import` URLs)
   - `assets/base.css`
   - the chosen theme file (`assets/themes/<name>.css`)
   - `assets/animations/animations.css`
2. Inline `assets/runtime.js` at the bottom of `<body>` in a `<script>` tag.
3. Skip the T-cycle feature OR keep `data-themes` empty — without sibling theme files, T can't swap themes (the runtime tries to load `themeBase + name + '.css'` and will 404). The hard-coded theme baked into the inlined `<style>` still works.
4. The S presenter window iframes use `location.protocol + '//' + location.host + location.pathname + '?preview=N'`. For a `file://` deck this can be flaky in some browsers due to iframe-from-file-with-query-param restrictions. Presenter mode is best served when the deck is opened over `http://localhost`.
5. Use the deck served at `file://...html` and previews still work in Chromium; arrow-key navigation works regardless.

**Recommended approach** for this project: keep the deck at `/Users/veto/Documents/git/html-pre/<deckname>/index.html` (sibling to the `html-ppt-skill/` folder) and use relative paths `../html-ppt-skill/assets/...`. This preserves T-cycling, presenter mode, and the full skill, without forking the skill repo.

## Gotchas

1. **`.notes` is `display:none!important` on the slide itself.** Never put presenter-only text as visible `<p>` / `<span>` on a slide — it MUST go inside `<div class="notes">`. The slide should contain only audience-facing content.
2. **Don't hand-author slides from scratch.** The repo's authoring rule is: open a single-page layout file, copy its `<section class="slide">` block, then edit the content.
3. **Use tokens, never hex colors.** `color: var(--text-1)`, not `color: #111`. Otherwise theme switching breaks.
4. **Layout dimensions are 1920×1080.** `.slide` is `position:absolute; inset:0; padding:72px 96px;` inside a `100vw × 100vh` deck. Design at 16:9. For 小红书 use 1242×1660 by changing `render.sh`.
5. **Single-page layout files use `body class="single"`** to disable the absolute positioning so the slide renders standalone. Strip `class="single"` and `class="is-active"` when copying into a multi-slide deck.
6. **The first slide doesn't need `is-active`** in a multi-slide deck — `runtime.js` sets it during init. (Adding it doesn't hurt either.)
7. **Chart.js / highlight.js / fonts** are CDN-loaded; offline use means caching them. Charts must wait for `DOMContentLoaded` and read CSS vars at init.
8. **`<aside class="notes">`, `.speaker-notes`, and `.notes` are all recognized** by `runtime.js` for the notes drawer.
9. **Theme T-key only works** if `<body data-themes="a,b,c"` AND `data-theme-base="../../assets/themes/"` are present AND the theme `<link>` has `id="theme-link"`.
10. **Stagger lists**: put `class="anim-stagger-list"` on the parent grid/ul; the children get rise-in with progressively delayed animation. Add `data-anim-target` so A-key cycling targets it.
11. **For `data-fx` canvas effects**, you must additionally include `<script src="../../assets/animations/fx-runtime.js"></script>`. Container needs an explicit `height`.
12. **Per the SKILL.md rule**: prefer composing existing layouts. Do not invent new `templates/single-page/*.html` files.
13. **`pre`/`code` blocks** inside cards usually need explicit `style="font-size:13px;background:var(--surface-2);padding:14px;border-radius:var(--radius-sm);overflow:auto"`.
14. **`.gradient-text` class** = three-color gradient text fill using `--grad`. Great for hero words.
15. **For long titles use `<br>`** inside `<h1 class="h1">` — the H1 font-size is 72px, line-height 1.05, so a 2-line title looks intentional. Don't shrink the font.

## Suggested output file path

Write Agent 3's deck at:

**`/Users/veto/Documents/git/html-pre/presentation/index.html`**

This keeps the deck as a sibling to `html-ppt-skill/`, so links resolve as:

```html
<link rel="stylesheet" href="../html-ppt-skill/assets/fonts.css">
<link rel="stylesheet" href="../html-ppt-skill/assets/base.css">
<link rel="stylesheet" id="theme-link" href="../html-ppt-skill/assets/themes/<theme>.css">
<link rel="stylesheet" href="../html-ppt-skill/assets/animations/animations.css">
<script src="../html-ppt-skill/assets/runtime.js"></script>
```

And `<body data-theme-base="../html-ppt-skill/assets/themes/">` for T-cycle.

Create the `presentation/` directory first. If a single portable file is preferred instead, write it to `/Users/veto/Documents/git/html-pre/presentation.html` with everything inlined (see Required asset paths section above).

---

## Verbatim: SKILL.md

```
---
name: html-ppt
description: HTML PPT Studio — author professional static HTML presentations in many styles, layouts, and animations, all driven by templates. Use when the user asks for a presentation, PPT, slides, keynote, deck, slideshow, "幻灯片", "演讲稿", "做一份 PPT", "做一份 slides", a reveal-style HTML deck, a 小红书 图文, or any kind of multi-slide pitch/report/sharing document that should look tasteful and be usable with keyboard navigation. Triggers include keywords like "presentation", "ppt", "slides", "deck", "keynote", "reveal", "slideshow", "幻灯片", "演讲稿", "分享稿", "小红书图文", "talk slides", "pitch deck", "tech sharing", "technical presentation".
---

# html-ppt — HTML PPT Studio

Author professional HTML presentations as static files. One theme file = one
look. One layout file = one page type. One animation class = one entry effect.
All pages share a token-based design system in `assets/base.css`.

## Install

```bash
npx skills add https://github.com/lewislulu/html-ppt-skill
```

One command, no build. Pure static HTML/CSS/JS with only CDN webfonts.

## What the skill gives you

- **36 themes** (`assets/themes/*.css`) — minimal-white, editorial-serif, soft-pastel, sharp-mono, arctic-cool, sunset-warm, catppuccin-latte/mocha, dracula, tokyo-night, nord, solarized-light, gruvbox-dark, rose-pine, neo-brutalism, glassmorphism, bauhaus, swiss-grid, terminal-green, xiaohongshu-white, rainbow-gradient, aurora, blueprint, memphis-pop, cyberpunk-neon, y2k-chrome, retro-tv, japanese-minimal, vaporwave, midcentury, corporate-clean, academic-paper, news-broadcast, pitch-deck-vc, magazine-bold, engineering-whiteprint
- **15 full-deck templates** (`templates/full-decks/<name>/`) — complete multi-slide decks with scoped `.tpl-<name>` CSS. 8 extracted from real-world decks (xhs-white-editorial, graphify-dark-graph, knowledge-arch-blueprint, hermes-cyber-terminal, obsidian-claude-gradient, testing-safety-alert, xhs-pastel-card, dir-key-nav-minimal), 7 scenario scaffolds (pitch-deck, product-launch, tech-sharing, weekly-report, xhs-post 3:4, course-module, **presenter-mode-reveal** — 演讲者模式专用)
- **31 layouts** (`templates/single-page/*.html`) with realistic demo data
- **27 CSS animations** (`assets/animations/animations.css`) via `data-anim`
- **20 canvas FX animations** (`assets/animations/fx/*.js`) via `data-fx` — particle-burst, confetti-cannon, firework, starfield, matrix-rain, knowledge-graph (force-directed), neural-net (pulses), constellation, orbit-ring, galaxy-swirl, word-cascade, letter-explode, chain-react, magnetic-field, data-stream, gradient-blob, sparkle-trail, shockwave, typewriter-multi, counter-explosion
- **Keyboard runtime** (`assets/runtime.js`) — arrows, T (theme), A (anim), F/O, **S (presenter mode: magnetic-card popup with CURRENT / NEXT / SCRIPT / TIMER cards)**, N (notes drawer), R (reset timer in presenter)
- **FX runtime** (`assets/animations/fx-runtime.js`) — auto-inits `[data-fx]` on slide enter, cleans up on leave
- **Showcase decks** for themes / layouts / animations / full-decks gallery
- **Headless Chrome render script** for PNG export

## When to use

Use when the user asks for any kind of slide-based output or wants to turn
text/notes into a presentable deck. Prefer this over building from scratch.

### 🎤 Presenter Mode (演讲者模式 + 逐字稿)

If the user mentions any of: **演讲 / 分享 / 讲稿 / 逐字稿 / speaker notes / presenter view / 演讲者视图 / 提词器**, or says things like "我要去给团队讲 xxx", "要做一场技术分享", "怕讲不流畅", "想要一份带逐字稿的 PPT" — **use the `presenter-mode-reveal` full-deck template** and write 150–300 words of 逐字稿 in each slide's `<aside class="notes">`.

See [references/presenter-mode.md](references/presenter-mode.md) for the full authoring guide including the 3 rules of speaker script writing:
1. **不是讲稿,是提示信号** — 加粗核心词 + 过渡句独立成段
2. **每页 150–300 字** — 2–3 分钟/页的节奏
3. **用口语,不用书面语** — "因此"→"所以","该方案"→"这个方案"

All full-deck templates support the S key presenter mode (it's built into `runtime.js`). **S opens a new popup window with 4 magnetic cards**:
- 🔵 **CURRENT** — pixel-perfect iframe preview of the current slide
- 🟣 **NEXT** — pixel-perfect iframe preview of the next slide
- 🟠 **SPEAKER SCRIPT** — large-font 逐字稿 (scrollable)
- 🟢 **TIMER** — elapsed time + slide counter + prev/next/reset buttons

Each card is **draggable by its header** and **resizable by the bottom-right corner handle**. Card positions/sizes persist to `localStorage` per deck. A "Reset layout" button restores the default arrangement.

**Why the previews are pixel-perfect**: each preview is an `<iframe>` that loads the actual deck HTML with a `?preview=N` query param; `runtime.js` detects this and renders only slide N with no chrome. So the preview uses the **same CSS, theme, fonts, and viewport as the audience view** — colors and layout are guaranteed identical.

**Smooth navigation**: on slide change, the presenter window sends `postMessage({type:'preview-goto', idx:N})` to each iframe. The iframe just toggles `.is-active` between slides — **no reload, no flicker**. The two windows also stay in sync via `BroadcastChannel`.

Only `presenter-mode-reveal` is designed from the ground up around the feature with proper example 逐字稿 on every slide.

Keyboard in presenter window: `← →` navigate (syncs audience) · `R` reset timer · `Esc` close popup.
Keyboard in audience window: `S` open presenter · `T` cycle theme · `← →` navigate (syncs presenter) · `F` fullscreen · `O` overview.

## Before you author anything — ALWAYS ask or recommend

**Do not start writing slides until you understand three things.** Either ask
the user directly, or — if they already handed you rich content — propose a
tasteful default and confirm.

1. **Content & audience.** What's the deck about, how many slides, who's
   watching (engineers / execs / 小红书读者 / 学生 / VC)?
2. **Style / theme.** Which of the 36 themes fits? If unsure, recommend 2-3
   candidates based on tone:
   - Business / investor pitch → `pitch-deck-vc`, `corporate-clean`, `swiss-grid`
   - Tech sharing / engineering → `tokyo-night`, `dracula`, `catppuccin-mocha`,
     `terminal-green`, `blueprint`
   - 小红书图文 → `xiaohongshu-white`, `soft-pastel`, `rainbow-gradient`,
     `magazine-bold`
   - Academic / report → `academic-paper`, `editorial-serif`, `minimal-white`
   - Edgy / cyber / launch → `cyberpunk-neon`, `vaporwave`, `y2k-chrome`,
     `neo-brutalism`
3. **Starting point.** One of the 14 full-deck templates, or scratch? Point
   to the closest `templates/full-decks/<name>/` and ask if it fits. If the
   user's content suggests something obvious (e.g. "我要做产品发布会" →
   `product-launch`), propose it confidently instead of asking blindly.

A good opening message looks like:

> 我可以给你做这份 PPT！先确认三件事:
> 1. 大致内容 / 页数 / 观众是谁?
> 2. 风格偏好? 我建议从这 3 个主题里选一个: `tokyo-night`（技术分享默认好看）、`xiaohongshu-white`（小红书风）、`corporate-clean`（正式汇报）。
> 3. 要不要用我现成的 `tech-sharing` 全 deck 模板打底?

Only after those are clear, scaffold the deck and start writing.

## Quick start

1. **Scaffold a new deck.** From the repo root:
   ```bash
   ./scripts/new-deck.sh my-talk
   open examples/my-talk/index.html
   ```
2. **Pick a theme.** Open the deck and press `T` to cycle. Or hard-code it:
   ```html
   <link rel="stylesheet" id="theme-link" href="../assets/themes/aurora.css">
   ```
   Catalog in [references/themes.md](references/themes.md).
3. **Pick layouts.** Copy `<section class="slide">...</section>` blocks out of
   files in `templates/single-page/` into your deck. Replace the demo data.
   Catalog in [references/layouts.md](references/layouts.md).
4. **Add animations.** Put `data-anim="fade-up"` (or `class="anim-fade-up"`) on
   any element. On `<ul>`/grids, use `anim-stagger-list` for sequenced reveals.
   For canvas FX, use `<div data-fx="knowledge-graph">...</div>` and include
   `<script src="../assets/animations/fx-runtime.js"></script>`.
   Catalog in [references/animations.md](references/animations.md).
5. **Use a full-deck template.** Copy `templates/full-decks/<name>/` into
   `examples/my-talk/` as a starting point. Each folder is self-contained with
   scoped CSS. Catalog in [references/full-decks.md](references/full-decks.md)
   and gallery at `templates/full-decks-index.html`.
6. **Render to PNG.**
   ```bash
   ./scripts/render.sh templates/theme-showcase.html       # one shot
   ./scripts/render.sh examples/my-talk/index.html 12      # 12 slides
   ```

## Authoring rules (important)

- **Always start from a template.** Don't author slides from scratch — copy the
  closest layout from `templates/single-page/` first, then replace content.
- **Use tokens, not literal colors.** Every color, radius, shadow should come
  from CSS variables defined in `assets/base.css` and overridden by a theme.
  Good: `color: var(--text-1)`. Bad: `color: #111`.
- **Don't invent new layout files.** Prefer composing existing ones. Only add
  a new `templates/single-page/*.html` if none of the 30 fit.
- **Respect chrome slots.** `.deck-header`, `.deck-footer`, `.slide-number`
  and the progress bar are provided by `assets/base.css` + `runtime.js`.
- **Keyboard-first.** Always include `<script src="../assets/runtime.js"></script>`
  so the deck supports ← → / T / A / F / S / O / hash deep-links.
- **One `.slide` per logical page.** `runtime.js` makes `.slide.is-active`
  visible; all others are hidden.
- **Supply notes.** Wrap speaker notes in `<div class="notes">…</div>` inside
  each slide. Press S to open the overlay.
- **NEVER put presenter-only text on the slide itself.** Descriptive text like
  "这一页展示了……" or "Speaker: 这里可以补充……" or small explanatory captions
  aimed at the presenter MUST go inside `<div class="notes">`, NOT as visible
  `<p>` / `<span>` elements on the slide. The `.notes` class is `display:none`
  by default — it only appears in the S overlay. Slides should contain ONLY
  audience-facing content (titles, bullet points, data, charts, images).

## Writing guide

See [references/authoring-guide.md](references/authoring-guide.md) for a
step-by-step walkthrough: file structure, naming, how to transform an outline
into a deck, how to choose layouts and themes per audience, how to do a
Chinese + English deck, and how to export.

## Catalogs (load when needed)

- [references/themes.md](references/themes.md) — all 36 themes with when-to-use.
- [references/layouts.md](references/layouts.md) — all 31 layout types.
- [references/animations.md](references/animations.md) — 27 CSS + 20 canvas FX animations.
- [references/full-decks.md](references/full-decks.md) — all 15 full-deck templates.
- [references/presenter-mode.md](references/presenter-mode.md) — **演讲者模式 + 逐字稿编写指南(技术分享/演讲必看)**.
- [references/authoring-guide.md](references/authoring-guide.md) — full workflow.

## File structure

```
html-ppt/
├── SKILL.md                 (this file)
├── references/              (detailed catalogs, load as needed)
├── assets/
│   ├── base.css             (tokens + primitives — do not edit per deck)
│   ├── fonts.css            (webfont imports)
│   ├── runtime.js           (keyboard + presenter + overview + theme cycle)
│   ├── themes/*.css         (36 token overrides, one per theme)
│   └── animations/
│       ├── animations.css   (27 named CSS entry animations)
│       ├── fx-runtime.js    (auto-init [data-fx] on slide enter)
│       └── fx/*.js          (20 canvas FX modules: particles/graph/fireworks…)
├── templates/
│   ├── deck.html                  (minimal 6-slide starter)
│   ├── theme-showcase.html        (36 slides, iframe-isolated per theme)
│   ├── layout-showcase.html       (iframe tour of all 31 layouts)
│   ├── animation-showcase.html    (20 FX + 27 CSS animation slides)
│   ├── full-decks-index.html      (gallery of all 14 full-deck templates)
│   ├── full-decks/<name>/         (14 scoped multi-slide deck templates)
│   └── single-page/*.html         (31 layout files with demo data)
├── scripts/
│   ├── new-deck.sh                (scaffold a deck from deck.html)
│   └── render.sh                  (headless Chrome → PNG)
└── examples/demo-deck/            (complete working deck)
```

## Rendering to PNG

`scripts/render.sh` wraps headless Chrome at
`/Applications/Google Chrome.app/Contents/MacOS/Google Chrome`. For multi-slide
capture, runtime.js exposes `#/N` deep-links, and render.sh iterates 1..N.

```bash
./scripts/render.sh templates/single-page/kpi-grid.html        # single page
./scripts/render.sh examples/demo-deck/index.html 8 out-dir    # 8 slides, custom dir
```

## Keyboard cheat sheet

```
←  →  Space  PgUp  PgDn  Home  End    navigate
F                                       fullscreen
S                                       open presenter window (magnetic cards: current/next/script/timer)
N                                       quick notes drawer (bottom overlay)
R                                       reset timer (in presenter window)
?preview=N                              URL param — force preview-only mode (single slide, no chrome)
O                                       slide overview grid
T                                       cycle themes (reads data-themes attr)
A                                       cycle demo animation on current slide
#/N in URL                              deep-link to slide N
Esc                                     close all overlays
```

## License & author

MIT. Copyright (c) 2026 lewis <sudolewis@gmail.com>.
```

---

## Verbatim: templates/deck.html (the minimal starter)

```html
<!DOCTYPE html>
<html lang="zh-CN" data-theme="minimal-white">
<head>
<meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<title>html-ppt · Deck</title>
<link rel="stylesheet" href="../assets/fonts.css">
<link rel="stylesheet" href="../assets/base.css">
<link rel="stylesheet" id="theme-link" href="../assets/themes/minimal-white.css">
<link rel="stylesheet" href="../assets/animations/animations.css">
</head>
<body data-themes="minimal-white,editorial-serif,soft-pastel,arctic-cool,sunset-warm,catppuccin-mocha,tokyo-night,aurora,xiaohongshu-white,neo-brutalism" data-theme-base="../assets/themes/">
<div class="deck">

  <!-- 1. Cover -->
  <section class="slide" data-title="Cover">
    <p class="kicker">html-ppt · 2026</p>
    <h1 class="h1 anim-fade-up" data-anim="fade-up">用模板,<span class="gradient-text">换主题</span><br>讲任何事情</h1>
    <p class="lede">24 themes · 30 layouts · 25 animations · zero build</p>
    <div class="deck-footer"><span class="dim2">lewis</span><span class="slide-number" data-current="1" data-total="6"></span></div>
    <div class="notes">这是一个最小可用的 deck。你可以复制这个文件作为新 deck 的起点。</div>
  </section>

  <!-- 2. TOC -->
  <section class="slide" data-title="目录">
    <p class="kicker">Agenda</p>
    <h2 class="h2">我们会讲三件事</h2>
    <div class="grid g3 mt-l anim-stagger-list" data-anim-target>
      <div class="card"><h4>01 · Tokens</h4><p class="dim">把颜色/字体/圆角收进 CSS 变量。</p></div>
      <div class="card"><h4>02 · Layouts</h4><p class="dim">30 种可复用单页。</p></div>
      <div class="card"><h4>03 · Runtime</h4><p class="dim">键盘驱动、按 T 换主题。</p></div>
    </div>
  </section>

  <!-- 3. Stat -->
  <section class="slide center tc" data-title="Stat">
    <div>
      <p class="kicker">Result</p>
      <div style="font-size:220px;font-weight:900;line-height:1"><span class="counter gradient-text" data-to="92">0</span><span class="gradient-text">%</span></div>
      <h3>的准备时间被省下</h3>
    </div>
  </section>

  <!-- 4. Two column -->
  <section class="slide" data-title="Tokens">
    <p class="kicker">Under the hood</p>
    <h2 class="h2">换主题 = 换一组变量</h2>
    <div class="grid g2 mt-l">
      <div class="card"><h4>语义变量</h4><p class="dim">写 <code>var(--surface)</code>,不写具体色值。</p></div>
      <div class="card"><h4>一键切换</h4><p class="dim">按 T 循环所有主题——所有 slide 同步更新。</p></div>
    </div>
  </section>

  <!-- 5. CTA -->
  <section class="slide center tc" data-title="CTA">
    <div>
      <p class="kicker">Your turn</p>
      <h1 class="h1 anim-rise-in" data-anim="rise-in">开始做你的 deck</h1>
      <p class="lede" style="margin:16px auto">按 ← → 翻页 · T 切主题 · A 切动效 · F 全屏 · O 概览 · S 备注</p>
    </div>
  </section>

  <!-- 6. Thanks -->
  <section class="slide center tc" data-title="Thanks">
    <h1 class="h1" style="font-size:160px;line-height:1"><span class="gradient-text">Thanks</span></h1>
    <p class="lede">lewis · sudolewis@gmail.com</p>
  </section>
</div>
<script src="../assets/runtime.js"></script>
</body></html>
```

---

## Quick reference: utility classes from base.css

- Typography: `.h1` (72px/800), `.h2` (54px/700), `.h3` (32px/600), `.h4` (22px/600), `.lede` (22px/300 muted), `.kicker` (uppercase accent), `.eyebrow` (uppercase tiny grey), `.dim` (text-2), `.dim2` (text-3), `.mono`, `.serif`, `.gradient-text`
- Layout: `.stack` (vertical rhythm), `.row` / `.row.wrap`, `.grid` + `.g2` / `.g3` / `.g4`, `.center` (flex center + tc), `.fill`
- Spacing: `.mt-s` (8), `.mt-m` (18), `.mt-l` (32), same for `.mb-*`, `.sp-t`, `.sp-b`
- Cards: `.card` (default), `.card-soft`, `.card-outline`, `.card-accent` (top-border in accent), `.card-hover`
- Pills: `.pill`, `.pill-accent`
- Dividers: `.divider`, `.divider-accent`
- Chrome: `.deck-header`, `.deck-footer`, `.slide-number` (uses data-current/data-total), `.progress-bar` (auto)
- Misc: `.tc` text-center, `.tl` left, `.tr` right, `.uppercase`, `.nowrap`, `.hidden`
- Speaker notes: `.notes` (display:none by default — surfaced via N drawer / S window)
