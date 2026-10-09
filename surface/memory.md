# Memory

Hermes has persistent memory that loads into every new session. Two stores: one for who I am (`USER.md`), one for my notes (`MEMORY.md`). Both survive across sessions — the agent that remembers what I meant last time is the one I trust with more.

## How it works

- **USER.md** — Who I am: preferences, background, how to work with me. Hermes reads this at session start and adapts.
- **MEMORY.md** — My notes: environment facts, conventions, lessons learned, project state. Also loaded at session start.
- Both files have a hard character budget. When they fill, I consolidate or replace stale entries rather than skipping the save.
- Memory is injected into every turn — it's not task-specific. If it only matters for one kind of work, it goes in a skill, not memory.

## What's in mine (sanitized excerpts)

### From USER.md

> Prefers concise, minimal-step instructions and plain-language explanations — avoid unnecessary detail when a short answer suffices.
>
> Non-technical: prefers plain-language explanations over command-line instructions, wants to understand tradeoffs before acting, and explicitly does not want to be pushed beyond their current skill level. Frame technical setup as staged progression — stay at current stage until a real need pushes forward.
>
> Works in crypto/web3. Has consulting experience — built a revenue operating system for a marketing agency. Also built: substrate, vsm-translator, dreamward. Iterative worker who prefers small chunks.

### From MEMORY.md

> PATTERN LANGUAGE PROJECT: Formology v0.3.1 — shared operating language of pro-forms with productive morphology. Five conformations tested across business, research, creative, software, and cybernetic morphology. NEXT: draft standalone formal proof; decide if algorithm/heuristic is a separate axis or a prefix reading.
>
> User sometimes interacts from mobile via Telegram without computer access.

## What this shows

Memory is the difference between a tool and an agent. The tool does what I say; the agent does what I mean — because it remembers what I meant last time. The fact that Hermes loads this context into every session, without me re-explaining, is the thing that makes it a collaborator rather than a chatbot.

The memory also has a character budget — it can't grow indefinitely. This is a product constraint that shapes behavior: I have to decide what's worth remembering, and the agent has to manage the budget. The consolidation behavior (replace stale entries, don't skip the save) is itself a product design choice — it keeps memory relevant without overflowing context.
