# Anthropic Warm Palette

Locked. Don't introduce colors outside this table. Every color flows through a CSS variable in `templates/anthropic.css`.

| Token | Hex | Name | Use |
| --- | --- | --- | --- |
| `--bg` | `#FAFAF7` | Ivory Light | Primary slide background |
| `--bg-soft` | `#F4F1EA` | Ivory Medium | Tinted slide background (`.slide.tinted` for section openers) |
| `--surface` | `#FFFFFF` | White | Card faces (rare — most cards are borderless now) |
| `--surface-2` | `#F4ECD9` | Manilla-tinted | Soft accent surfaces |
| `--border` | `rgba(20,20,19,.08)` | Hairline | All borders — should be nearly invisible |
| `--border-strong` | `rgba(20,20,19,.18)` | Strong hairline | Section dividers, the rule under the cover H1 |
| `--text-1` | `#141413` | Slate Dark | Primary text |
| `--text-2` | `#3A3A38` | Slate Medium | Secondary text, body lede |
| `--text-3` | `#7A7A75` | Slate Light / Cloud | Meta text, captions, sidenotes |
| `--accent` | `#CC785C` | **Book Cloth** | **Primary accent — terracotta. The signature color.** |
| `--accent-2` | `#D4A27F` | Kraft | Secondary accent (rare) |
| `--accent-3` | `#EBDBBC` | Manilla | Tertiary accent / soft fill |
| `--focus` | `#61AAF2` | Focus blue | `:focus-visible` outline only. Not for links, not for hover. |
| `--good` / `--warn` / `--bad` | `#7A8F5C` / `#D4A27F` / `#B8593E` | sage / kraft / dark book cloth | Status colors, used almost never in decks |

## Rules of restraint

- **Book Cloth carries the energy.** Use on: kickers (small uppercase eyebrow), one italic accent per heading, the hanging numeral, big-stat unit, hairline dividers under H1.
- **Anthropic's accent is rare** in their real production sites — it appears on kicker eyebrows, the "Try Claude" CTA, one underline accent in the hero. That's it. The vast majority of pixels are ivory or slate.
- **Kraft and Manilla are background tints**, not card fills. A whole section background can be Kraft-tinted; cards inside should be ivory.
- **Focus blue is a spice, not a staple.** Don't sprinkle it on hover states.
- **Hairline borders only.** Cards should look like they were ironed onto the page, not lifted off it.
- **No shadows.** If you find yourself adding `box-shadow`, type-driven hierarchy is failing — fix that instead.

## Anti-patterns

- Gradient-filling heading text. (It's a Webflow-template move; Anthropic never does this.)
- Three or more accent moments on one slide.
- Card with a colored top stripe AND a colored border AND a shadow.
- Using Focus blue for hover or link color. It's reserved for keyboard focus.
- Hardcoding hex codes in `main.html`. Always route through the theme.
