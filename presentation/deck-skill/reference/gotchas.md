# Gotchas

Bugs that bit this house style at least once, with the fix.

## Slide overflow (the most common one)

`base.css` puts `.slide` at `display:flex; flex-direction:column; justify-content:center; overflow:hidden`. When content is taller than the viewport, the slide is centered AND clipped — so content escapes both top and bottom, not just the bottom. A clipped letter at the top and a footer overlap at the bottom is the smoking gun.

**Fix priorities, in order:**
1. Remove an optional element (figure, extra paragraph).
2. Reduce a figure's `max-height`.
3. Tighten dict / hanging-list padding from 18px → 12px per item.
4. Reduce slide padding from 88px to 72px.
5. Last resort: change `.slide` to `justify-content:flex-start` and pin the top.

Slides most at risk: layer pages with `layer-mark + h2 + dict + figure` (slide 12 of the Agent-Harness deck originally hit this).

## `.center` on a `.slide` breaks flex direction

`base.css`'s `.center` is `display:flex;align-items:center;justify-content:center;text-align:center` — no `flex-direction:column`. When you put it on a `.slide` (which IS `flex-direction:column`), `.center` overrides without re-asserting column. Children stack horizontally instead of vertically.

**Fix:** don't put `.center` on the `.slide` itself. Wrap content in a child div with the centering rules.

## Stacked animations on one element

The cover h1 originally had both `class="anim-fade-up"` AND was a direct child of `<div class="anim-stagger-list">`. Two animations targeted the same element, fighting for opacity initial state. Brief flash of invisible h1 on slide enter.

**Fix:** pick one. Either remove `anim-fade-up` and let the stagger-list parent handle it, or move the h1 outside the stagger wrapper.

## `.g1` is not defined in `base.css`

`base.css` defines `.g2`, `.g3`, `.g4` but no `.g1`. Using `class="grid g1"` silently gives you `display:grid` with `gap` but no `grid-template-columns` — the items end up in a single column by default-flow accident, which usually looks right but is fragile.

**Fix:** `anthropic.css` adds `.g1{grid-template-columns:1fr}` explicitly. If you start from a different theme, add it yourself.

## Hex codes leaking into HTML

The theme system stops working if you hardcode `#CC785C` (or any other hex) in `main.html`. The `T`-key theme cycler can't swap colors that don't go through CSS variables.

**Fix:** route every color through `var(--accent)`, `var(--text-2)`, etc. Use `rgba(204,120,92,.32)` only when you genuinely need an alpha tint that's not in the token set — and even then, prefer adding a new variable.

**Check:** `grep -oE '#[0-9A-Fa-f]{6}' main.html | wc -l` must be 0.

## CJK glyphs drift apart on tracked labels

Western typography uses `letter-spacing: .18em` on uppercase eyebrows. Apply the same value to Chinese text and you get 「插 曲 · 词 源」 with gaping holes between glyphs.

**Fix:** in the Chinese mirror, override every tracked-label class to `letter-spacing: .04em`:

```css
.kicker,.eyebrow,.deck-header,.deck-footer,.section-rule .lbl,
.label-caps,.bignum-cap .src,.quote-source,.statrow .stat .lbl,
.fb-figure figcaption .cap-num,.middot-list,.layer-mark .name{
  letter-spacing:.04em;
}
```

## Geometric Unicode symbols (⌖ ⌬ ↔) render as boxes

Inter doesn't ship glyphs for many obscure Unicode geometric shapes. On some systems they fall back to a missing-glyph box.

**Fix:** use plain digits (01 / 02 / 03), or SVG icons.

## Subagents can't write report files

Claude Code's harness blocks Write from subagents for arbitrary report files (the rule is "subagents return findings as text, not write files"). Agents will report success even when the write was blocked.

**Fix:** instruct each agent to write its output as text in the final response. The orchestrator (you) does the `Write`. Affects `summary.md`, `skill-briefing.md`, `MANIFEST.md` typically.

The figures agent CAN write the image files themselves (those are the deliverable, not a report). Only the report files are blocked.

## `pdftoppm not found` after installing poppler

`brew install poppler` puts binaries in `/opt/homebrew/bin/` (Apple Silicon) or `/usr/local/bin/` (Intel). The Read tool may have cached its PATH at session start and not see them.

**Fix:** in agent prompts that need PDF reading, pass the absolute path: `/opt/homebrew/bin/pdftoppm ...`. Or extract content via Python `pypdf` / `pdfplumber` instead.

## Page renders inflate the repo

`pdftoppm -png -r 150` produces ~500 KB per page. A 44-page paper = ~22 MB. Use the 14 named figures for the deck; gitignore the page renders.

```gitignore
presentation/assets/img/page-*.png
```

## Vendored skill repo becomes a nested git

After `git clone https://github.com/lewislulu/html-ppt-skill`, the inner `.git/` makes git treat it as a sub-repo or submodule. Pushing to your own remote will error or silently exclude its files.

**Fix:** `rm -rf html-ppt-skill/.git` immediately after clone. The MIT license is preserved (LICENSE file stays inside), and your repo just has plain files.

## Cover h1 italic on the wrong word for the Chinese mirror

If `<em>` wraps the second line of a translated H1, the italic accent lands on a Chinese word — but the *imported foreign term* (e.g. `harness` in the Chinese deck) is the one that should be emphasized. Move the `<em>` onto the foreign word.

```html
<!-- English: italic accent on "Engineering" -->
<h1 class="cover-h1">Agent Harness<br><em>Engineering</em></h1>

<!-- Chinese: italic accent on "harness" (the imported term) -->
<h1 class="cover-h1">Agent <em>harness</em><br>工程</h1>
```
