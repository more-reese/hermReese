# Model comparison evals

Same task, different models. Same input, same criteria, different results. Shows that model choice is a product decision — it affects UX, cost, reliability, and trust.

---

## Why this matters

Hermes is provider-agnostic — I can swap models mid-workflow. This is a product feature, not just a technical one. The model determines:

- **Quality of output** — does it produce accurate, useful results?
- **Speed** — how long does the user wait?
- **Cost** — how many tokens, at what price?
- **Reliability** — does it follow the tool-use discipline, or hallucinate?
- **Trust** — does the user feel comfortable giving it more after this interaction?

Choosing a model is choosing a user experience. The comparison evals make this visible.

## Planned comparisons

_To be populated with real comparison runs. Each comparison should use the same task and acceptance criteria across at least two models, with results side by side._

### Comparison 1: Pre-publish review across models

**Task:** Run the pre-publish review (Eval 1 from [task-completion.md](task-completion.md)) across GLM-5.2 and at least one other model.

**Acceptance criteria:** Same as Eval 1 — secrets scan, clean install, typecheck, build, boot, data audit, .gitignore check.

**What to measure:** 
- Did it complete all criteria?
- How long did it take?
- How many tool calls did it make?
- Did it flag the same issues, or different ones?
- Did it hallucinate any results?

### Comparison 2: Skill authoring across models

**Task:** Build a new skill from a plain-language description across two models.

**Acceptance criteria:**
- Skill file passes YAML frontmatter validation
- Routing table covers the stated use cases
- No fabricated steps (each step references a real tool or capability)
- Skill loads and is usable in a subsequent session

**What to measure:**
- Did the skill work when loaded?
- How well did it route — did it load for the right tasks?
- How much patching was needed before it was usable?

---

## What this shows

The "set acceptance criteria that account for task completion, reliability, speed and cost" requirement. Model comparison isn't about benchmarks — it's about which model gives the best *user experience* for a given task. A model that's faster but hallucinates more is worse for trust-critical tasks. A model that's slower but more reliable is better for tasks with real consequences.

The product insight: model choice should be task-aware, not just user-configured. A pre-publish review (trust-critical, high-consequence) should use the most reliable model; a brainstorming session (low-stakes, exploratory) can use a faster, cheaper model. Hermes's per-stage model choice (as implemented in lenswork) is the right pattern — different stages, different models, different tradeoffs.
