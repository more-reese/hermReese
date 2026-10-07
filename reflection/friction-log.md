# Friction log

Real friction points I've hit using Hermes Agent. Each entry is a specific moment — not a general complaint. What I was doing, what happened, what it felt like, what I'd fix.

---

## 1. Stale write protection blocks legitimate edits

**Date:** 2026-10-07
**Task:** Rewriting the README for this repo after restructuring.
**What happened:** Hermes's write_file tool refused to overwrite README.md because it detected the file had been "read" in a different execution context (the first session's interpreter). It required a fresh read_file call before allowing the overwrite — even though I'd already read the file earlier in the same session.
**What it felt like:** Like the tool was protecting me from myself, but the protection fired on a false positive. I had to work around it by writing via terminal (`cat > file << EOF`) instead of the proper tool.
**What I'd fix:** The stale-write protection should be session-scoped, not execution-context-scoped. If I read the file in this session, I should be able to write to it. The protection is right to exist — it prevents stale overwrites — but the boundary is too conservative.

## 2. Long outputs truncate on mobile

**Date:** Ongoing
**Task:** Receiving Hermes outputs via Telegram.
**What happened:** When Hermes produces a long output (terminal output, file contents, search results), Telegram truncates it. I get the first part and lose the rest, or it gets split awkwardly across messages.
**What it felt like:** Like the mobile surface is a second-class citizen. The desktop app handles long outputs gracefully; the Telegram gateway doesn't.
**What I'd fix:** A mobile-formatted output mode — summarize long outputs, attach full content as a document (via the telegram-send skill), or chunk outputs intelligently based on the surface.

## 3. Context compression can lose important details

**Date:** 2026-10-07
**Task:** A long session working on the pattern-language skill.
**What happened:** Mid-session, context compression kicked in (threshold 50%, target ratio 20%). The compressed context dropped some of the nuanced distinctions I'd been building — specific conformations, edge cases, the precise wording of an open question. The agent continued working but with a slightly flattened version of what we'd discussed.
**What it felt like:** Like the agent forgot the nuance but remembered the gist. Good enough to continue, not good enough to pick up exactly where we left off.
**What I'd fix:** Compression should preserve the most recently discussed details at higher fidelity and compress older context more aggressively. The current approach is ratio-based; a recency-weighted approach would preserve the working edge better.

## 4. Skill loading adds latency to the first response

**Date:** Ongoing
**Task:** Starting a session that uses a complex skill (pattern-language, job-application-strategy).
**What happened:** When a skill loads, the first response is slower — the agent has to read the skill content, parse the YAML frontmatter, and route to the right section before it can act. For large skills (pattern-language is ~8KB), this adds noticeable latency.
**What it felt like:** Like a cold start. Once the skill is loaded, the session is fast. But the first interaction feels slow.
**What I'd fix:** Skill pre-loading or lazy section loading — load the routing table first, then load the specific section when the agent knows which one it needs. Don't load the full skill body until the section is needed.

## 5. The .usage.json file has nested nulls that break shell parsing

**Date:** 2026-10-04
**Task:** Checking which skills I've built and how often I use them.
**What happened:** I asked Hermes what skills I'd built. It tried to read `~/.hermes/skills/.usage.json` with `cat | python3` — but the file has nested null values that break `jq` and inline Python formatting. The command crashed. I had to use `execute_code` with proper null guards (`or 0`) instead of shell pipes.
**What it felt like:** Like the tooling around Hermes's own state files isn't quite production-grade. The data is there; the ergonomics aren't.
**What I'd fix:** Either clean up the null values in `.usage.json` (use 0 instead of null for missing counts) or provide a first-class `hermes skills stats` command that handles the parsing internally. Don't make users parse internal state files manually.

---

## What this shows

These aren't hypothetical friction points — they're real moments I hit while using Hermes, documented through a Hermes session. The friction log is the "understand where it succeeds and breaks down" requirement, made honest. Each entry has a specific fix I'd propose — not because I know better, but because I've felt the gap and thought about what would close it.

The pattern I see across these: Hermes is strong at the core loop (conversation → tools → output) and weaker at the edges (surface parity, state file ergonomics, compression fidelity, cold-start latency). The product opportunity is at the edges — that's where trust with the tenth task is won or lost.
