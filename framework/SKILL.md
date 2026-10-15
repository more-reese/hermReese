---
name: hermes-learning-path
description: "Learn Hermes Agent from first principles with assessment."
version: 1.0.0
author: moreReese + Hermes Agent
license: MIT
platforms: [macos, linux, windows]
metadata:
  hermes:
    tags: [learning, hermes, curriculum, assessment, onboarding]
    category: productivity
---

# Hermes Learning Path

A structured curriculum for learning Hermes Agent from first principles, with dual assessment (knowledge + practical skills) and progress tracking.

**Use Hermes to learn Hermes.** Work with Hermes to show you how it works, not to tell you.

## When to Use

Use when learning Hermes Agent from the official learning path docs — working through the beginner→intermediate→advanced curriculum, doing practice exercises, or running a knowledge + skills assessment for any module. Also loads when checking learning progress.

## How this works

Each module follows the same cycle:

1. **Learn** — Read the doc together. I explain it in plain language. You ask questions. We make sure you understand the *why*, not just the *what*.
2. **Practice** — You actually do the thing in Hermes. Not a quiz — real practice. Set up a real config, create a real skill, schedule a real cron job.
3. **Assess** — Two parts:
   - **Knowledge check**: You explain the concept back to me in your own words. I verify you understand it from first principles — not just "what does this command do" but "why does it work this way."
   - **Skills check**: You complete a practical exercise and I verify the output actually worked. Real tool output, not self-reporting.
4. **Record** — Results go to a progress file (see templates/progress.md) and to memory so the next session picks up where you left off.

## Curriculum overview

Three tiers, each building on the last. Don't skip ahead — each tier assumes the one before it.

### Beginner (~1 hour)

| # | Module | Doc | Learn | Practice | Assess |
|---|--------|-----|-------|----------|--------|
| 1 | Installation | [Installation](https://hermes-agent.nousresearch.com/docs/getting-started/installation) | What Hermes is, how it installs, what it needs | Run `hermes doctor` — verify it works | Explain what Hermes is in your own words; show doctor passing |
| 2 | Quickstart | [Quickstart](https://hermes-agent.nousresearch.com/docs/getting-started/quickstart) | The interaction model — you talk, it uses tools, it responds | Run `hermes chat -q` with a real query; have an interactive session | Explain the interaction loop; show a completed query |
| 3 | CLI Usage | [CLI Usage](https://hermes-agent.nousresearch.com/docs/user-guide/cli) | Commands, flags, session navigation | Use `hermes --help`, list sessions, resume one | Explain what 3+ CLI commands do; demonstrate resuming a session |
| 4 | Configuration | [Configuration](https://hermes-agent.nousresearch.com/docs/user-guide/configuration) | config.yaml vs .env, what lives where, how settings work | View your config, change a setting with `hermes config set` | Explain the config/secrets split; show a real config change |

### Intermediate (~2-3 hours)

| # | Module | Doc | Learn | Practice | Assess |
|---|--------|-----|-------|----------|--------|
| 5 | Sessions | [Sessions](https://hermes-agent.nousresearch.com/docs/user-guide/sessions) | Session lifecycle, context persistence, how to manage | Start a session, do work, exit, resume it | Explain how sessions persist context; demonstrate resume |
| 6 | Messaging | [Messaging](https://hermes-agent.nousresearch.com/docs/user-guide/messaging/) | The gateway model — how Hermes connects to platforms | Verify your Telegram connection works end-to-end | Explain the gateway model; show a working messaging round-trip |
| 7 | Tools | [Tools](https://hermes-agent.nousresearch.com/docs/user-guide/features/tools) | What tools are, how the agent calls them, what's available | Use 3+ different tools in a single session | Explain what a tool call is from first principles; show tool output |
| 8 | Skills | [Skills](https://hermes-agent.nousresearch.com/docs/user-guide/features/skills) | What skills are, how they load contextually, how to create one | Load a skill with `skill_view`, examine its structure | Explain the contextual loading model; show a loaded skill's content |
| 9 | Memory | [Memory](https://hermes-agent.nousresearch.com/docs/user-guide/features/memory) | What persists across sessions, what doesn't, why | Add a memory entry, verify it appears in a new session | Explain the memory/skill/session boundary; show a persisted entry |
| 10 | Cron | [Cron](https://hermes-agent.nousresearch.com/docs/user-guide/features/cron) | Scheduled jobs, when to use them vs other approaches | Create a real cron job, verify it runs | Explain cron vs session vs delegation; show a created and run job |

### Advanced (~4-6 hours)

| # | Module | Doc | Learn | Practice | Assess |
|---|--------|-----|-------|----------|--------|
| 11 | Architecture | [Architecture](https://hermes-agent.nousresearch.com/docs/developer-guide/architecture) | Internal structure, request flow, how pieces connect | Trace a tool call through the system mentally | Explain the request flow from prompt to tool execution |
| 12 | Adding Tools | [Adding Tools](https://hermes-agent.nousresearch.com/docs/developer-guide/adding-tools) | The tool registration pattern, tool schemas | Read the adding-tools doc, understand the pattern | Explain how a tool gets registered and called |
| 13 | Creating Skills | [Creating Skills](https://hermes-agent.nousresearch.com/docs/developer-guide/creating-skills) | SKILL.md format, frontmatter, structure, linked files | Create a simple skill from scratch | Show a created skill with proper frontmatter and structure |
| 14 | Contributing | [Contributing](https://hermes-agent.nousresearch.com/docs/developer-guide/contributing) | How to contribute to Hermes Agent itself | Read contributing guidelines, understand the process | Explain the contribution workflow |

### Bonus: Reading Code (~1-2 hours)

A bonus module on reading, understanding, and explaining code using the Hermes source as the primary reference. See `references/module-15-sub-modules.md` for the full sub-module curriculum.

## Assessment protocol

### Knowledge check (understanding)

After learning a module, I ask you to explain it back to me in your own words. I'm checking for:

- **First-principles understanding** — not "what command does X" but "why does X work this way"
- **Accurate mental model** — does your explanation match how Hermes actually works?
- **Boundary awareness** — can you explain what this feature does AND doesn't do?

Score: **pass** / **partial** / **retry**. On retry, we go back to Learn with the specific gap.

### Skills check (practical ability)

You complete the practice exercise and I verify the output with a real tool call — not self-reported.

Score: **pass** / **partial** / **retry**. On retry, we practice again.

A module is **complete** when both checks pass (partial counts as pass with a note).

## Progress tracking

### In a progress file

`progress.md` (see `templates/progress.md`) is the durable trace. Each completed module gets:

- Module name, tier, status
- Knowledge score, skills score
- Date completed
- One-line note (what you said about it in your own words)

The git history of that file is the longitudinal record — every assessment is a commit.

### In memory

A single entry stores your current position: tier + next module. Every new session reads it and knows where to pick up.

## Conceptual Shorthands

Aphorisms describe general truths. Metaphors aid understanding. Heuristics aid deciding.

See `references/conceptual-shorthands.md` for the full collection. Add new ones as they emerge from the learning process.

## Pitfalls

- **Don't invent architectural layers.** When describing Hermes architecture, stick to what the docs and source code show. If you synthesize a concept to aid understanding, label it as a conceptual aid — never present it as a documented component.
- **Don't over-iterate on shorthand refinement.** When the user says a shorthand isn't resonant, lock in what works and move on. Don't spend more than one round refining a single phrase.

## Rules

- Don't skip tiers. Each builds on the last.
- Don't skip the knowledge check. Understanding the *why* is the point.
- Don't skip verification on the skills check. I check real output, not self-reporting.
- If you get "partial" on either check, it still counts — but the note captures what's incomplete.
- The curriculum is a guide, not a prison. If a module sparks a tangent, follow it — but come back.
- If something in the curriculum is wrong or outdated, fix this skill with `skill_manage`.
