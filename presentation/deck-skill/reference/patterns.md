# Layout Patterns

Ten type-driven patterns to rotate through across a 15–17 slide deck. Mix freely. **No two adjacent slides should share a pattern.** The whole point is to escape the card-grid monotony that makes most generated decks look the same.

All patterns assume `templates/anthropic.css` is loaded (it defines the class hooks used below).

---

## 1. Drop cap (essay opener)

The single most "this is an essay, not a slide" move. Use on the cover lede.

```html
<p class="dropcap-para">
  <span class="dropcap">T</span>he harness, not the model, is the binding
  constraint on real-world LLM agent reliability. Seven layers, 170+
  open-source projects, one taxonomy.
</p>
```

For CJK: the dropcap works on the first Chinese character. Reduce its right-padding (`.dropcap{padding:4px 16px 0 0}`) since Chinese characters are square.

---

## 2. Hanging numeral (giant marginal number)

The slide's section number lives in the left margin, in giant lightweight serif. Body to the right.

```html
<section class="slide">
  <div class="layout-hang">
    <aside class="hang-num">01</aside>
    <div class="hang-body">
      <p class="kicker">Thesis</p>
      <h3>Better models alone do not produce more reliable agents.</h3>
      <p>Three independent empirical results in early 2026 …</p>
    </div>
  </div>
</section>
```

---

## 3. Hanging-list (book-style numbered list)

The replacement for "stack of accent cards." Numbers sit outside the text block, hairline rules separate items.

```html
<ol class="hanging-list">
  <li>
    <span class="n">01</span>
    <div>
      <h4>Up to <em style="color:var(--accent);font-style:normal;font-weight:700">10×</em> gains from a single edit-tool change</h4>
      <p>Boluk 2026 — one harness-only intervention; the model never moved.</p>
    </div>
  </li>
  <li>
    <span class="n">02</span>
    <div>
      <h4>Second item headline</h4>
      <p>Supporting text.</p>
    </div>
  </li>
</ol>
```

Use `<span class="n roman">` for Roman numerals (i, ii, iii) — good for open-problem lists where the items aren't strictly ranked.

---

## 4. Asymmetric two-column with sidenote

Main column on the left (max 680px), thin sidenote column on the right (320px) for marginalia. Tufte / Newsreader essay pattern.

```html
<div class="layout-sidenote">
  <div class="main-col">
    <p>Main body prose. Two or three paragraphs. Let it breathe.</p>
    <p>Second paragraph continues the argument.</p>
  </div>
  <aside class="side-col">
    <p class="side-note"><span class="side-marker">A</span>A first marginal note — definitions, quotes, sources.</p>
    <p class="side-note"><span class="side-marker">B</span>A second marginal note.</p>
  </aside>
</div>
```

Variant: pair a big stat with prose — `.layout-sidenote` with `grid-template-columns:auto 1fr;gap:96px;align-items:center` and a `.bignum-val` on the left.

---

## 5. Run-in heading (heading + paragraph share a line)

Classic essay pattern. Use to give three sub-points their own visual weight without a card grid.

```html
<p class="run-in"><span class="run-in-head">Security.</span> LLM code is non-auditable and runs autonomously. The sandbox is the only audit trail.</p>
<p class="run-in"><span class="run-in-head">Reproducibility.</span> A baseline snapshot makes evaluation comparable across runs.</p>
<p class="run-in"><span class="run-in-head">Liveness.</span> A bounded region in which the agent can act without prompting a human.</p>
```

Wrap three of these in a `<div class="run-stack" style="max-width:none">` if you want them grouped.

---

## 6. Section divider — label + hairline

For visual punctuation between major arcs of the deck. Replaces the "section title slide with giant card background."

```html
<div class="section-rule">
  <span class="lbl">Part Two — The Seven Layers</span>
  <span class="line"></span>
</div>
```

Or the dinkus (Dario Amodei's section break, U+2042):

```html
<div class="dinkus"></div>
```

---

## 7. Big number / stat with subscript unit

The number is enormous; the unit (%, ×, +) is a small subscript in accent color. Caption is small and serif.

```html
<div class="bignum">
  <div class="bignum-val">84<span class="bignum-unit">%</span></div>
  <p class="bignum-cap">
    reduction in Claude Code permission prompts via a properly engineered sandbox.
    <span class="src">Anthropic · production data, 2026</span>
  </p>
</div>
```

For three small stats inline, use `.statrow` (defined in `anthropic.css`):

```html
<div class="statrow">
  <div class="stat"><div class="val">89<span class="u">%</span></div><p class="lbl">Adoption</p><p>caption</p></div>
  <div class="stat"><div class="val">52<span class="u">%</span></div><p class="lbl">Evaluation gap</p><p>caption</p></div>
  <div class="stat"><div class="val">98<span class="u">%</span></div><p class="lbl">FrugalGPT</p><p>caption</p></div>
</div>
```

---

## 8. Dictionary entry

Best for defining a vocabulary the rest of the deck depends on. Replaces "TOC of cards."

```html
<dl class="dict">
  <div class="entry">
    <div class="letter">i</div>
    <div class="body">
      <dt>Permission models <span class="pos">· how authority is granted</span></dt>
      <dd>Static, contextual, identity-aware delegation across users, tools, and agents.</dd>
    </div>
  </div>
  <div class="entry">
    <div class="letter">ii</div>
    <div class="body">
      <dt>Four hook points <span class="pos">· where checks fire</span></dt>
      <dd>Input · action · post-execution · human-in-the-loop.</dd>
    </div>
  </div>
</dl>
```

The `.letter` is in display sans + accent color. The `.pos` is italic gray, like a part-of-speech marker in a real dictionary.

---

## 9. Full-bleed quote

No card, no border, no decoration. Quote at 48–84px Newsreader-italic on the ivory canvas. Single attribution line below with a hairline rule.

```html
<section class="slide bleed">
  <div class="layout-quote" style="height:100%;padding-left:120px">
    <blockquote class="bigquote">
      <span class="open-quote">&ldquo;</span>Every harness component encodes an
      <em>assumption</em> about what the model cannot do on its own.
    </blockquote>
    <p class="quote-source"><span class="rule"></span>Anthropic &middot; Harness Design 2026</p>
  </div>
</section>
```

The slide takes the `bleed` class to drop normal padding. Add `<div class="deck-footer" style="padding:0 96px">` so the footer doesn't break.

---

## 10. Hero figure with caption

The replacement for in-deck illustrations. Edge-to-near-edge image, small `<figcaption>` underneath.

```html
<figure class="hero-figure">
  <img src="./assets/img/fig-name.png" alt="Descriptive alt text">
  <figcaption>
    <span class="cap-num">Fig 2</span>
    Caption text — what the figure shows, plus one observation about it.
  </figcaption>
</figure>
```

For a small supporting image (e.g. a horizontal flow diagram), use `.strip-figure` (defined in `main.html` local style) at `max-height:200px`.

For an asymmetric "hanging-list on the left, figure on the right" slide, use `.two-col-fig` (1.05fr / 1fr grid).

---

## Slide-to-pattern mapping (suggested)

For a 16-slide paper deck, a healthy rotation:

| Slide | Pattern |
| --- | --- |
| 1 Cover | drop cap |
| 2 Thesis claim | hanging-list |
| 3 Background / context | sidenote |
| 4 Big concept intro | hero figure |
| 5 Taxonomy / categories | hero figure + middot list |
| 6 Component 1 with metric | big stat + run-ins |
| 7 Component 2 | hanging-list + supporting figure |
| 8 Component 3 with metric | big stat + sidenote |
| 9 Component 4 | hero figure |
| 10 Component 5 (multiple metrics) | statrow + quote |
| 11 Component 6 | hero figure |
| 12 Component 7 | dictionary entries |
| 13 Synthesis / cross-cutting | section rule + run-ins |
| 14 Open questions | hanging-list (Roman numerals) |
| 15 Key quote | full-bleed quote |
| 16 Takeaways | hanging-list |

If your topic has fewer or different components, adapt — but never repeat the same pattern on two adjacent slides.
