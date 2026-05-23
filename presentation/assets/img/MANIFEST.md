# Figure Manifest — Agent Harness Engineering

All assets live in `/Users/veto/Documents/git/html-pre/presentation/assets/img/`.

14 clean named figures extracted plus 44 full-page renders (body pages 1-44) at 150 DPI.
Three of the figures (three-phases, ETCLOVG taxonomy, task-feedback lifecycle) were pulled directly from the PDF's embedded image stream — these are the crispest assets in the set.

## Recommended for slides

| Slide | Figure file | What it shows | Source page |
| --- | --- | --- | --- |
| 1 (Cover) | fig-etclovg-taxonomy.png | ETCLOVG seven-layer architecture as a visual anchor for the cover | p. 6 |
| 4 (Three Engineering Phases) | fig-three-phases.png | Three-column comparison — Prompt vs Context vs Harness engineering, with icons for each subsystem | p. 1 |
| 5 (ETCLOVG intro) | fig-etclovg-taxonomy.png | The colored seven-layer ETCLOVG architecture diagram (E, T, C, L on row 2; O on top; V, G as footer bands) | p. 6 |
| 5 alt (deeper view) | fig-etclovg-detail.png | Full hierarchical outline of all seven ETCLOVG layers with their subcategories | p. 8 |
| 5 alt (history) | fig-harness-timeline.png | Timeline of representative harness systems 2022-2026, color-tagged by ETCLOVG layer | p. 7 |
| 6 (Layer E — Sandboxes) | fig-sandbox-categories.png | Seven sandbox categories tree: managed, computer-use, code, framework-integrated, browser, OS-level, abstractions | p. 11 |
| 7 (Layer T — Tools) | fig-tool-interface-tree.png | Four tool-interface subcategories: protocol standards, description/discovery, training/integration, scalability | p. 16 |
| 8 (Layer C — Context/Memory) | fig-context-memory-tree.png | Five context/memory subcategories: active window, session state, long-term memory, long-horizon techniques, drift/limits | p. 19 |
| 9 (Layer L — Lifecycle) | fig-lifecycle-orchestration-tree.png | Three lifecycle patterns: single-agent inner loop, multi-agent orchestration, full lifecycle pipeline issue-to-PR | p. 25 |
| 10 (Layer O — Observability) | fig-observability-tree.png | Five observability subcategories: tracing/monitoring, agent-specific ops, cost tracking, reliability engineering, unified observability | p. 28 |
| 11 (Layer V — Verification) | fig-task-feedback-lifecycle.png | Five-stage circular task-to-feedback lifecycle (grounding → readiness → execution → judgement → regression feedback) | p. 33 |
| 11 alt (Verification tree) | fig-verification-tree.png | Five verification subcategories tree corresponding to the lifecycle stages | p. 32 |
| 12 (Layer G — Governance) | fig-governance-tree.png | Six governance subcategories: permission models, lifecycle hooks, component hardening, declarative constitutions, audit infrastructure, agent security landscape | p. 39 |
| 12 alt (Hook points) | fig-hook-points.png | Linear diagram of the four hook points H1-H4 along one tool-use cycle (Input → LLM → Tool → Response) | p. 41 |
| 13 (Cross-Layer Synthesis) | fig-etclovg-detail.png | Complete ETCLOVG outline reused to anchor the cross-layer discussion | p. 8 |
| 16 (Takeaways) | fig-corpus-protocol.png | Corpus construction protocol showing the systematic methodology behind the survey's 170+ project corpus | p. 9 |

Slides 2 (Binding Constraint), 3 (Practitioner-Research Gap), 14 (Open Problems), and 15 (Key Quote) have no dedicated paper figure — they are text-heavy / argumentative slides. Recommend rendering them with typography and pull-quotes only.

## All clean named figures (file → quick description)

| File | Size | Source | Notes |
| --- | --- | --- | --- |
| fig-three-phases.png | 377 KB | embedded image, p. 1 | Crisp three-column comparison, original source quality |
| fig-etclovg-taxonomy.png | 345 KB | embedded image, p. 6 | Crisp colored layered architecture, original source quality |
| fig-harness-timeline.png | 209 KB | cropped from p. 7 render | Full 2022-2026 timeline with ~50 representative systems |
| fig-etclovg-detail.png | 196 KB | cropped from p. 8 | Hierarchical outline of every ETCLOVG layer and subcategory |
| fig-corpus-protocol.png | 285 KB | embedded image, p. 9 | Methodology diagram: search sources → construction protocol |
| fig-sandbox-categories.png | 142 KB | cropped from p. 11 | Seven sandbox categories with named systems per row |
| fig-tool-interface-tree.png | 118 KB | cropped from p. 16 | Four tool-interface subcategories tree |
| fig-context-memory-tree.png | 109 KB | cropped from p. 19 | Five context/memory subcategories tree |
| fig-lifecycle-orchestration-tree.png | 135 KB | cropped from p. 25 | Three orchestration-pattern subcategories tree |
| fig-observability-tree.png | 156 KB | cropped from p. 28 | Five observability subcategories tree |
| fig-verification-tree.png | 156 KB | cropped from p. 32 | Five verification subcategories tree |
| fig-task-feedback-lifecycle.png | 213 KB | embedded image, p. 33 | Crisp five-stage circular validation/evaluation diagram |
| fig-governance-tree.png | 174 KB | cropped from p. 39 | Six governance subcategories tree |
| fig-hook-points.png | 74 KB | cropped from p. 41 | Linear H1-H4 hook-point flow along one tool-use cycle |

## Figures considered but skipped

| Item | Why skipped |
| --- | --- |
| Table 1 (tool standards by integration boundary) | Pure text table, low visual interest; the tool tree (Figure 7) covers the same ground |
| Table 2 (representative orchestration systems) | Pure text table, large; the lifecycle tree (Figure 9) is more presentation-friendly |
| Table 3 (governance mechanisms vs risk taxonomy) | Pure text table; the governance tree (Figure 13) covers the same ground |
| Table 4 (governance feature coverage matrix) | Sparse text table — useful for the paper but not a strong visual for slides |

## All page renders

- `page-01.png` through `page-44.png` — full body pages at 150 DPI, ~400-530 KB each
- Reference/appendix pages (45-71) were rendered then discarded to keep the directory lean
- Use page renders as fallback if any named figure crop is unsatisfactory, or to lift additional unlabeled diagrams not catalogued above

## Notes for the synthesis agent

- The three "embedded image" figures (three-phases, ETCLOVG taxonomy, task-feedback lifecycle) came out of `pdfimages` directly — they are the highest fidelity assets and will not pixelate at any reasonable slide size. Prefer these over the cropped versions of their source pages.
- All "tree" figures (sandbox, tool, context, lifecycle, observability, verification, governance) follow the same visual grammar — a left spine label, colored category boxes in the middle, and citation lists on the right. They will look like a coherent visual family if used in sequence on slides 6 through 12.
- The Figure 1 three-phase diagram on slide 4 is the deck's single best "explainer" graphic — it makes the prompt→context→harness progression immediately legible. The ETCLOVG taxonomy on slide 5 is the second-best.
- Hook-points diagram (fig-hook-points.png) is very small/wide — use it inline at modest size on slide 12, not as a hero image.
- Page renders include header band "Under review as submission to TMLR" and page numbers. If a slide quotes a page directly, that header is visible; crop it out if it visually distracts.
