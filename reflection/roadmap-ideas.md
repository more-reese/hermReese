# Roadmap ideas

If I owned the Hermes Agent roadmap, here's what I'd prioritize. Each idea connects to a specific friction point or success pattern from my own usage — not hypotheticals.

---

## 1. Surface parity: make every surface first-class

**What:** Every surface (desktop, CLI, TUI, Telegram, Discord, web dashboard) should handle the same range of outputs gracefully. Long outputs, file attachments, rich formatting, interactive elements — all should work everywhere, with surface-appropriate rendering.

**Why it matters:** The Telegram gateway is how I work when I'm not at my desk. Right now it's a second-class surface — long outputs truncate, diffs are impractical, interactive browser sessions don't work. The conversation is the product; the surface shouldn't determine the quality. (Friction log entries 1, 2.)

**What "done" looks like:** A long output on Telegram gets summarized with a link to the full content (or attached as a document). A diff gets rendered as a formatted message or a file. The surface adapts the output, not the other way around.

**Tradeoff:** This is a lot of surface-specific work. The alternative is a single "output adapter" layer that normalizes outputs per surface — less work, but less polished.

## 2. Compression that preserves the working edge

**What:** Context compression should be recency-weighted — preserve the most recently discussed details at higher fidelity and compress older context more aggressively. The current approach is ratio-based (compress to 20% of context window), which treats all context as equally compressible.

**Why it matters:** In a long session, the most important context is what we're working on *right now* — the last few exchanges, the current open question, the nuance we just established. Compressing that at the same ratio as the opening preamble loses the working edge. (Friction log entry 3.)

**What "done" looks like:** After compression, the agent can pick up the current thread with the same nuance it had before. The last N exchanges are preserved at full fidelity; older context is compressed more aggressively. The user doesn't notice the compression happened.

**Tradeoff:** Recency-weighted compression is more complex to implement and may preserve less total context. The ratio-based approach is simpler and more predictable.

## 3. Trust metrics: make the tenth task visible

**What:** Define and surface metrics that show whether users are trusting Hermes with more of their work over time — not just activation (first task) or retention (repeat use), but task escalation: are users giving the agent harder, more consequential tasks as they use it more?

**Why it matters:** The tenth task is where the product lives or dies. If I'm using Hermes for the same simple tasks on session 50 as I was on session 1, the product isn't earning trust — it's plateauing. (See [metrics.md](metrics.md).)

**What "done" looks like:** A dashboard or report that shows, per user: task complexity trend, tool diversity (am I using more tools over time?), session length trend, and skill creation rate. Not vanity metrics — trust metrics.

**Tradeoff:** "Task complexity" is hard to define and measure. It's easier to measure what tools were used than how hard the task was. But the hard metric is the one that matters.

## 4. Skill ergonomics: faster cold starts

**What:** Skills should load lazily — the routing table first, then the specific section when the agent knows which one it needs. Currently, loading a large skill (like pattern-language at ~8KB) adds noticeable latency to the first response.

**Why it matters:** Skills are the productization layer — they're how raw capabilities become useful experiences. If loading a skill adds friction, users avoid using skills, and the product's key differentiator goes unused. (Friction log entry 4.)

**What "done" looks like:** The first response after skill activation is as fast as a response without the skill. The routing table loads instantly; the section loads when referenced.

**Tradeoff:** Lazy loading is more complex and may cause mid-session latency when a new section is needed. Eager loading is simpler but slower on cold start.

## 5. State file ergonomics: don't make users parse internals

**What:** Hermes's internal state files (`.usage.json`, `.curator_ledger.jsonl`, `executions.db`) should be accessible through first-class commands, not manual parsing. `hermes skills stats`, `hermes sessions list`, `hermes cron history` — commands that handle the parsing internally.

**Why it matters:** When I want to know "what skills have I built and how often do I use them," I should run a command, not parse a JSON file with null guards. The data is there; the ergonomics aren't. (Friction log entry 5.)

**What "done" looks like:** Every internal state file has a corresponding CLI command that produces human-readable output. No one should need to `cat` or `jq` a state file to understand their own usage.

**Tradeoff:** Building CLI commands for every state file is maintenance surface. But the alternative — users parsing internal files — is worse.

---

## What this shows

Each idea connects to a real moment of using Hermes — a friction point, a success pattern, a gap I felt. This is product management grounded in lived experience, not market research. The roadmap isn't "what I think Hermes should do"; it's "what I've noticed Hermes needs, from using it every day."

The through-line: the product opportunity is at the edges — surface parity, compression fidelity, skill ergonomics, state file ergonomics, trust measurement. The core loop (conversation → tools → output) works. The edges are where trust with the tenth task is won or lost.
