# Agent Harness Engineering: A Survey

**Source:** [LR]Agent-Harness-Engineering.pdf
**One-line summary:** Real-world LLM agent reliability is bound less by model capability than by the engineered execution harness around it, which this survey organizes into a seven-layer ETCLOVG taxonomy backed by 170+ open-source projects.
**Tone for deck:** practical, opinionated, engineering-focused, systems-minded

---

## Slide 1 — Title
**Type:** title
**Headline:** Agent Harness Engineering: A Survey
**Body:**
- Junjie Li, Xi Xiao, Yunbei Zhang, Chen Liu et al.
- CMU, Yale, JHU, Tulane, OSU, Virginia Tech, Amazon
- Submitted to TMLR, 2026
- The harness, not the model, is the binding constraint
**Speaker notes:** This survey argues that the infrastructure layer wrapping an LLM is now the dominant variable in agent reliability. It synthesizes practitioner knowledge from OpenAI, Anthropic, and LangChain with academic research and maps 170+ open-source projects to a new taxonomy.

---

## Slide 2 — The Binding Constraint
**Type:** content
**Headline:** Better models alone do not produce more reliable agents
**Body:**
- Boluk 2026: harness-only edit-tool change gave up to 10x gains
- Trivedy 2026: +13.7 points on Terminal-Bench by changing infra only
- Meta-Harness 2026: 76.4% on Terminal-Bench-2 via automated harness search
- Each beats the typical 2-4 point model-driven gain
- Variable held constant: the model. What changed: the harness.
**Speaker notes:** These three recent empirical results in early 2026 are the wedge for the whole survey. Same model, different scaffolding around it, dramatically different reliability. This is what the authors call the binding-constraint thesis.

---

## Slide 3 — The Practitioner-Research Gap
**Type:** content
**Headline:** Practitioners know harnesses matter; research lacks the vocabulary
**Body:**
- OpenAI: "harness engineering" produced 1M lines without manual code
- Anthropic: simple inspectable agents, tools for agents not humans
- Martin Fowler site: harnesses as "cybernetic governors for AI agents"
- Researchers still study memory, tools, planning, safety in isolation
- Missing: the system that integrates them into reliable operation
**Speaker notes:** Practitioners know that infrastructure matters but lack formal terms to describe why. The survey aims to bridge this gap so improvements can be made systematically rather than as folklore.

---

## Slide 4 — Three Engineering Phases
**Type:** comparison
**Headline:** Prompt to Context to Harness Engineering
**Body:**
- Prompt engineering (2022-2024): optimize one text input to one call
- Context engineering (2025): manage information streams across turns
- Harness engineering (2026): design constraints, feedback loops, controls
- Each phase subsumes the previous; they overlap rather than replace
- Marginal engineering effort keeps shifting outward
**Speaker notes:** This evolution explains why the field is here today. As models got better at long-horizon work, the bottleneck shifted outward from text input, to information state, to the entire control system around the model.

---

## Slide 5 — Introducing ETCLOVG
**Type:** section
**Headline:** Seven layers, one harness
**Body:**
- E: Execution environment and sandbox
- T: Tool interface and protocol
- C: Context and memory management
- L: Lifecycle and orchestration
- O: Observability and operations
- V: Verification and evaluation
- G: Governance and security
**Speaker notes:** ETCLOVG extends prior six-component frameworks by promoting Observability and Governance to first-class layers. The authors argue both have distinct tooling ecosystems and team ownership in production, so they deserve their own architectural treatment.

---

## Slide 6 — Execution Environment (E)
**Type:** content
**Headline:** Sandboxes are cage, license, and reset button
**Body:**
- Security: LLM code is non-auditable and runs autonomously
- Reproducibility: reset to baseline for evaluation and training
- Liveness: bounded region where agent can act without prompts
- Anthropic cut Claude Code permission prompts by 84% via sandbox
- Seven categories: managed, computer-use, code, framework, browser, OS-level, abstractions
**Speaker notes:** Sandboxing serves three jobs at once and the combination is what elevates it to a first-class concern. Liveness is the new one: without a sandbox, every risky action needs a human prompt, which destroys long-horizon execution.

---

## Slide 7 — Tool Interface (T)
**Type:** content
**Headline:** Fewer but better tools beat bloated menus
**Body:**
- MCP standardizes agent-to-capability; A2A standardizes agent-to-agent
- Function calling and OpenAPI remain foundational
- AGENTS.md encodes tool usage in version control
- Oversized tool menus degrade reliability and inflate prompts
- Discovery must be adaptive, not static global lists
**Speaker notes:** This layer sits at the fault line between coverage and decision quality. The principle from production: if a human engineer cannot say which tool applies in a situation, the model cannot either.

---

## Slide 8 — Context and Memory (C)
**Type:** content
**Headline:** Give the model exactly the right tokens, nothing more
**Body:**
- Attention is quadratic; long context is architecturally expensive
- U-shaped curve: middle context drops accuracy by 30+ percent
- Context rot: 18 frontier models degrade well before window is full
- Three tiers: active window, session state, persistent memory
- KV-cache hit rate: "the single most important metric" (Manus team)
**Speaker notes:** Bigger windows do not fix the memory problem. Liu 2024 showed information placement matters as much as presence, and Hong 2025 showed degradation begins long before windows fill. Effective context engineering is about progressive disclosure, compaction, and cache-aware design.

---

## Slide 9 — Lifecycle and Orchestration (L)
**Type:** content
**Headline:** From single loop to issue-to-pull-request pipeline
**Body:**
- Single-agent loop: ReAct-style observe-think-act
- Multi-agent: hierarchical, team, workflow, fan-out, graph composition
- Full lifecycle: task runner spans planning, code, test, review, merge
- Execution models: stateless replay, stateful, hybrid
- State here is operational, distinct from memory and from observability
**Speaker notes:** This layer combines execution flow with the operational state the flow reads and writes. Reliability over long tasks depends on remembering what happened, deciding what is next, recovering from errors, and stopping when done.

---

## Slide 10 — Observability (O)
**Type:** content
**Headline:** Traces, costs, failures as first-class concerns
**Body:**
- OpenTelemetry semantic conventions for generative AI
- Langfuse, Opik, Phoenix, MLflow for trace trees and dashboards
- AgentSight uses eBPF to monitor outside the agent process
- FrugalGPT: cost cuts of up to 98% via cascade routing
- 89 percent use observability, only 52 percent run offline evals
**Speaker notes:** Observability earned its own layer because it has a dedicated tooling stack, instrumentation standards, and dedicated practitioners. The bigger story is the observability-evaluation gap: teams can see what agents did but cannot systematically judge it.

---

## Slide 11 — Verification (V)
**Type:** content
**Headline:** A task-to-feedback lifecycle, not a leaderboard score
**Body:**
- Stage 1: ground tasks in environments with success criteria
- Stage 2: validate sandbox, tools, context, evaluator readiness
- Stage 3: controlled execution with rich trace capture
- Stage 4: multi-level judgement and failure attribution
- Stage 5: convert outcomes into regression and deployment feedback
**Speaker notes:** Evaluation is reframed as a five-stage quality-control loop. Infrastructure noise can masquerade as model failure: Anthropic showed config alone shifts benchmark scores by 6 points. Reported scores are properties of the model-harness pair, not the model alone.

---

## Slide 12 — Governance and Security (G)
**Type:** content
**Headline:** Permission, hooks, hardening, constitutions, audit
**Body:**
- Permission models: static, contextual, identity-aware delegation
- Four hook points: input, action, post-execution, human-in-the-loop
- Component hardening: instruction hierarchy, Llama Guard, MCP signing
- Declarative constitutions: training-time vs YAML deployment policy
- Audit: structured logs, anomaly detection per-action or per-trajectory
**Speaker notes:** Governance was promoted to a first-class layer because it has its own tooling, languages, and ownership in production. The defense-in-depth pattern fails if layers are not coordinated. No surveyed agent fully implements all defense categories today.

---

## Slide 13 — Cross-Layer Synthesis
**Type:** comparison
**Headline:** Three system-level effects, not isolated layers
**Body:**
- Cost-Quality-Speed Trilemma: stronger checks slow and cost more
- Capability-Control Tradeoff: more authority widens the blast radius
- Harness Coupling: local changes regress the whole control loop
- Frameworks are becoming platforms: tenancy, billing, fault recovery
- Score variance cannot be attributed to the model alone
**Speaker notes:** Once the seven layers are composed, their interactions create constraints no single layer can solve. Harness changes should be tested as system changes. The ecosystem is shifting from "build an agent" to "operate a fleet of agents."

---

## Slide 14 — Open Problems
**Type:** content
**Headline:** Five questions for the next phase
**Body:**
- Harden and scale execution environments under real threat models
- Maintain reliable state across long-horizon, multi-session work
- Diagnose failures from traces, not just final scores
- Standardize handoffs across agents, tools, sandboxes, humans
- Keep harnesses useful as models improve; simplify, do not bloat
**Speaker notes:** Anthropic reports they removed scaffolding when upgrading from Opus 4.5 to 4.6 and cost dropped from 200 to 125 dollars with equal quality. Every harness component encodes an assumption about what the model cannot do; those assumptions go stale.

---

## Slide 15 — Key Quote
**Type:** quote
**Headline:** "Every harness component encodes an assumption about what the model cannot do on its own"
**Body:**
- Anthropic, Harness Design for Long-Running Apps, 2026
- Removing context resets cut cost 37 percent with no quality drop
- Harness design should not be assumed to move monotonically up
- Adaptive simplification is the durable goal
**Speaker notes:** This is the paper's most memorable framing. Harnesses should re-estimate their interventions as models change. Meta-Harness and Natural-Language Agent Harnesses point toward harnesses that optimize and simplify themselves.

---

## Slide 16 — Takeaways
**Type:** takeaways
**Headline:** Treat the harness as an independent engineering surface
**Body:**
- Infrastructure quality, not model size, sets the reliability ceiling
- Use ETCLOVG to talk about, partition, and improve harness layers
- Observability and Governance deserve dedicated ownership and tooling
- Evaluate the model-harness pair; trace is the primary evidence
- Simplify as models improve; do not assume more scaffolding is better
**Speaker notes:** The survey closes by acknowledging its bias toward English-language, GitHub-visible, coding-agent projects. The natural next step is turning ETCLOVG from descriptive taxonomy into a normative framework that guides harness design rather than only classifying it.
