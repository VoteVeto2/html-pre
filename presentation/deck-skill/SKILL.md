---
name: paper-to-deck
description: Turn a PDF (research paper, engineering write-up, long article) into a 15–17 slide HTML presentation. Uses the html-ppt-skill runtime as the slide engine, the Anthropic warm palette, Charter body + system-sans headings, and a typography-forward design (hanging numerals, dropcaps, sidenotes, run-ins, big stats, dictionary entries, hero figures, full-bleed quotes) that escapes card-grid monotony. Invoke whenever the user asks to turn a paper, article, or PDF into HTML slides, a deck, or a presentation. Optionally produces a Chinese mirror with CJK font fallbacks and tightened letter-spacing.
---

# Paper-to-Deck

A workflow for turning a single PDF into a high-quality HTML presentation in this house style.

## When to use

Invoke when the user:
- Provides a PDF / paper / article and asks for slides, a deck, a talk, a presentation.
- Asks to refresh or restyle an existing deck in the same look-and-feel.
- Asks for a Chinese (or other-language) mirror of a finished deck.

Do **not** use for plain Markdown bullets, README writing, or single-image asks.

## Output layout

```
<project>/
├── <source>.pdf
├── summary.md                 # Phase-1 brief
├── html-ppt-skill/            # vendored runtime (cloned, .git removed)
├── presentation/
│   ├── main.html              # the deck — 15–17 slides
│   ├── anthropic.css          # Anthropic Warm theme (Charter + system sans)
│   ├── main-cn.html           # (optional) Chinese mirror
│   └── assets/img/            # extracted figures + page-NN.png references
├── README.md                  # (optional) one-screen project overview
└── onboard.md                 # (optional) editor's guide for collaborators
```

Asset paths in `main.html` resolve via `../html-ppt-skill/assets/...`. Keep `presentation/` and `html-ppt-skill/` as siblings.

## The 3-phase pipeline

### Phase 1 — parallel research (3 agents)

Spawn in a **single message** so they run in parallel.

1. **Figures agent** (general-purpose). Extract PDF figures into `presentation/assets/img/`. Tools: `pdftoppm -png -r 150 <pdf> page` for per-page renders; `pdfimages -png <pdf> embed` for embedded images; Python+Pillow for crops. Write a `MANIFEST.md` mapping each figure to a candidate slide. *Note:* harness blocks subagent file writes — agent must return the manifest text and the orchestrator writes it.

2. **Summary agent** (general-purpose). Read the PDF. Produce `summary.md` with 14–16 slide entries. Each entry: `## Slide N — title`, `Type: title|section|content|quote|comparison|takeaways`, `Headline: <=12 words`, `Body: 3–6 bullets, <=14 words`, `Speaker notes: 1–3 sentences`. Same write-back constraint as the figures agent.

3. **Skill-setup agent** (general-purpose). `git clone https://github.com/lewislulu/html-ppt-skill` into `<project>/html-ppt-skill/`, then `rm -rf html-ppt-skill/.git` so it's vendored cleanly. Read `SKILL.md` and `templates/deck.html`, write a one-page briefing capturing the canonical slide markup and theming hooks.

If poppler isn't installed, install first: `brew install poppler` (mac) or `apt-get install poppler-utils` (linux).

### Phase 2 — audit (optional, 1 agent)

Trigger when fixing an existing deck or before shipping. Audit `main.html` for:
- broken / undefined CSS classes (grep every `class="..."` against `base.css` + `anthropic.css` + local `<style>`)
- hex codes leaking into HTML (`grep -oE '#[0-9A-Fa-f]{6}' main.html | wc -l` should be 0)
- runtime contract violations (`data-current` / `data-total` correct, `<div class="notes">` on every slide)
- **slide overflow** (the most common bug — see `reference/gotchas.md`)

Agent returns a punch list. **Do not fix in-agent.** Synthesize fixes in Phase 3.

### Phase 3 — synthesis (in-conversation, not delegated)

The orchestrator composes `main.html` and (if missing) `anthropic.css` directly. Design judgment lives here — don't delegate.

For each slide:
1. Pick a layout pattern from `reference/patterns.md` that fits the content.
2. **Rotate** patterns across the deck. No two adjacent slides share a pattern. If three slides in a row are "row of cards with a number and a sentence", something is wrong.
3. Insert relevant figures from the figures-agent manifest. Use `hero-figure` (full-width) for diagrams that carry the slide; `strip-figure` (small) for supporting visuals.
4. Speaker notes go in `<div class="notes">` per slide — hidden from audience, surfaced via `N` drawer / `S` presenter window.

## Design rules

- **Palette:** Anthropic warm, locked. See `reference/palette.md`. Book Cloth `#CC785C` is the *only* accent on every slide; the rest is ivory canvas and slate ink. The accent is a punctuation mark, not a paint job.
- **Typography:** Charter (body) + native system sans (headings & UI chrome) + native system mono. No webfont `@import`. See `templates/anthropic.css`.
- **No shadows on cards.** Hairline borders only (`rgba(20,20,19,.08)`). Most pixels should be ivory/slate.
- **Type-driven hierarchy, not box-driven.** Headings differ in *size and weight*, not in chrome.
- **Slide budget:** 15–17 slides. Cover → thesis → definitions → body (one per concept) → cross-cutting synthesis → quote → takeaways.

## Bug-checking before declaring done

```bash
cd presentation/
grep -c '<section class="slide' main.html     # == intended slide count
grep -c '<div class="notes">' main.html       # == intended slide count
grep -oE 'data-total="[0-9]+"' main.html | sort -u  # exactly one value
grep -oE '#[0-9A-Fa-f]{6}' main.html | wc -l  # == 0 (no hex in HTML)
```

Then open in a browser and step through every slide. Look for clipped content at top/bottom (slide-overflow — see `reference/gotchas.md`).

## Chinese mirror (optional)

Trigger when the user asks for a Chinese version of a finished deck.

1. Copy `main.html` → `main-cn.html`.
2. Translate visible text. Keep technical terms in English (MCP, A2A, LLM, ETCLOVG, AGENTS.md). Keep author names in pinyin/English. Translate institution names to Chinese (CMU → 卡内基梅隆 etc.).
3. Add an inline `<style>` block in `<head>` with CJK overrides — see `templates/main-cn-overrides.css`. Three things matter:
   - **Font fallbacks:** prepend `PingFang SC`, `Songti SC`, `Noto Sans/Serif SC` to `--font-serif` and `--font-display` stacks.
   - **Letter-spacing:** Western `.18em` tracking on uppercase labels spreads CJK glyphs apart. Override to `.04em`.
   - **Line-height:** CJK reads better at `1.75` than the default `1.55`.
4. Set `<html lang="zh-CN">`, Chinese `<title>`.
5. If keeping a foreign term untranslated (e.g. "harness"), use a Python script (regex over CJK ranges) to add a space between CJK and Latin per Chinese tech-writing convention.

## Quick start

From the directory where you want the deck to live (with the source PDF present):

```bash
bash <project>/presentation/deck-skill/scripts/new-deck.sh
bash <project>/presentation/deck-skill/scripts/extract-figures.sh <source>.pdf
# Then spawn the 3 research agents per Phase 1 above.
```

## Files in this skill

| File | Purpose |
| --- | --- |
| `SKILL.md` | This file — workflow recipe and invocation guide. |
| `templates/anthropic.css` | The working Anthropic Warm theme. Copy as-is for a new deck; customize per project if needed. |
| `templates/main.html` | A 5-slide boilerplate showing the core patterns. Copy to `presentation/main.html` and extend. |
| `templates/main-cn-overrides.css` | Drop-in `<style>` snippet for the Chinese mirror. |
| `reference/palette.md` | Anthropic palette tokens with usage rules. |
| `reference/patterns.md` | The 10 layout patterns with HTML snippets — the heart of the design system. |
| `reference/gotchas.md` | Known bugs and what causes them. |
| `scripts/new-deck.sh` | Bootstrap a fresh deck folder (clones `html-ppt-skill`, copies templates). |
| `scripts/extract-figures.sh` | Run pdftoppm + pdfimages on a PDF, write to `presentation/assets/img/`. |

## Install as a Claude skill (optional)

To make this invocable from any project:

```bash
mkdir -p ~/.claude/skills/
cp -r <this folder> ~/.claude/skills/paper-to-deck
```

Then Claude can invoke it via the Skill tool whenever the description's trigger conditions match.
