# hermReese

**Use Hermes to learn Hermes.** Work with Hermes to show you how it works, not to tell you.

This repo is both a **reusable learning framework** and a **personal learning path** — the evidence of one person's journey through it.

## What's here

| Directory | What it is | Who it's for |
|-----------|-----------|--------------|
| [`framework/`](framework/) | The reusable framework — a Hermes skill, default curriculum, assessment protocol, and conceptual shorthands | Anyone who wants to learn Hermes with Hermes |
| [`path/`](path/) | A personal learning path — progress records, artifacts, and reflections from completing the curriculum | Reference for what the framework produces |
| [`surface/`](surface/) | How the author actually works with Hermes day to day | The author |
| [`artifacts/`](artifacts/) | What the interactions produce — skills, projects, writing | The author |
| [`reflection/`](reflection/) | What the author is figuring out about product, including Hermes itself | The author |

## The philosophy

An agent is a cognitive prosthetic. It cultivates a new channel — translating thought into material value aligned to user intent. The prosthetic increases the fidelity of that process: more of what I mean becomes what I get, and the gap between thinking and output narrows with use.

Trust is earned through memory, adaptation, and transparency. The agent that remembers what I meant last time, adapts to how I work, and shows its work is the one I trust with more. The one that hallucinates confidently, forgets context, or hides its reasoning gets used less — and the less it's used, the less it can learn. Trust and use are coupled.

The ideal agent disappears. You think through it. The interface becomes the work itself — not a screen between you and the work, but a surface where thinking and making are the same act.

## The framework

The `framework/` directory contains a Hermes skill (`SKILL.md`) that anyone can install into their own Hermes instance. Clone the repo, install the skill, and Hermes guides you through a structured curriculum with dual assessment (knowledge + practical skills).

```bash
# Clone the framework
git clone https://github.com/more-reese/hermReese.git
cd hermReese/framework

# Install the skill into your Hermes instance
# (or copy SKILL.md + references/ into your ~/.hermes/skills/ directory)
```

The framework ships with a default Hermes curriculum (14 modules across 3 tiers + a bonus module on reading code). You can follow it as-is or customize it for your own learning goals.

## The principle

**Work with Hermes to show you how it works, not to tell you.**

The learning path is built on a simple idea: you learn a tool by using it to understand itself. Hermes reads its own docs, explains them in plain language, gives you hands-on practice, and assesses both your understanding and your practical skills. The agent that runs the curriculum is the same agent the curriculum teaches you about — it's self-referential by design.

Each module follows a cycle: **learn → practice → assess → record**. The agent reads the doc, explains it, you practice, the agent verifies your output with real tool calls, and your results are recorded for the next session to pick up.

## The path

The `path/` directory is a completed example of what the framework produces — one person's progress through the default curriculum, including their key insights, diagrams they built, and reflections on what they learned. It's evidence that the framework works, and a reference for what your own path might look like.

---

Maintained by a daily Hermes Agent user. The git history is the iteration history.
