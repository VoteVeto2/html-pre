# Agent Harness Engineering — HTML Presentation

A 16-slide HTML deck of the survey paper *Agent Harness Engineering* (Li et al., 2026), themed in Anthropic's warm palette and built with the [html-ppt-skill](https://github.com/lewislulu/html-ppt-skill).

## View the deck

Open `presentation/index.html` in any modern browser:

```sh
open presentation/index.html
```

**Keyboard:** `←` / `→` or `Space` to navigate, `N` for speaker notes, `S` for presenter view, `T` to cycle themes, `F` for fullscreen.

## What's here

```
.
├── [LR]Agent-Harness-Engineering.pdf   source paper
├── summary.md                          slide-by-slide content brief
├── skill-briefing.md                   how the html-ppt-skill works
├── html-ppt-skill/                     cloned skill (templates, CSS, runtime, themes)
└── presentation/
    ├── index.html                      the deck — 16 slides
    └── anthropic.css                   the Anthropic Warm theme
```

## How it was built

A 3-agent pipeline:

1. **Summarize** — read the PDF, extract the thesis (the ETCLOVG taxonomy and the binding-constraint argument), write `summary.md` structured as one section per slide.
2. **Set up** — clone `html-ppt-skill`, document its templates and theming hooks in `skill-briefing.md`.
3. **Cook** — compose `presentation/index.html` from the summary and skill templates; write `anthropic.css` covering every variable `base.css` references. Zero hex codes are hardcoded in the HTML — all colors flow through the theme.

See [`onboard.md`](onboard.md) for the practical guide to editing slides, swapping colors, or rebuilding from a new PDF.

## Credits

- Survey paper: Junjie Li, Xi Xiao, Yunbei Zhang, Chen Liu et al. — *Agent Harness Engineering: A Survey* (TMLR submission, 2026).
- Skill: [lewislulu/html-ppt-skill](https://github.com/lewislulu/html-ppt-skill).
- Palette: Anthropic brand colors — Slate, Cloud, Ivory, Book Cloth, Kraft, Manilla, Focus.
