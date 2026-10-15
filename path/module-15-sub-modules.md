# Module 15: Reading and Explaining Code — Sub-Module Curriculum

**Prerequisite:** Tier I (Beginner) complete. Does not require Tier II or III.  
**Primary Reference:** The Hermes Agent source code at `~/.hermes/hermes-agent/`  
**Estimated Duration:** 1–2 hours across 6 sub-modules  
**Goal:** Teach the engineering concepts, patterns, and design decisions behind Hermes Agent — not how to code, but how to *read* the code well enough to speak intelligently to the engineers who built it and trace how design decisions impact the user experience.

---

## Course Philosophy

Modules 1–14 taught what Hermes *does*. This module teaches how to see what it *is* — by reading the code that makes it work. The student has spent the course building mental models: the interaction loop, the session store, the config split, the skill loader, the tool dispatch. This module connects those mental models to the actual source files and the engineering decisions they embody.

The purpose is not to make the student a programmer. The purpose is to make the student a **reader** — someone who can look at a codebase and understand it well enough to:

1. **Speak intelligently to engineers** — use the right vocabulary, ask the right questions, understand the tradeoffs they made
2. **Trace design decisions to user experience** — see how a choice in the code (frozen snapshot, progressive disclosure, platform-agnostic core) becomes something the user feels (memory not updating mid-session, skills loading on match, one session across surfaces)

---

## Sub-Module Structure

Each sub-module follows the same cycle as the main curriculum: **learn → practice → assess**. The student reads a real source file or excerpt, the instructor explains the engineering concept it embodies, and the student explains it back in their own words.

The sub-modules escalate in technical depth: the first is approachable with no code knowledge, and the last reaches into design patterns the Hermes team chose and why.

---

### Sub-Module 15.1: Reading a File — What Is This Code Doing?

**Estimated time:** ~15 minutes  
**Technical level:** Low — no code knowledge needed

**Concept:** How to approach an unfamiliar source file. Read the imports (what does it depend on?), read the function signatures (what does it expose?), read the body of the most important function (what does it actually do?). You don't read code top-to-bottom — you read it outside-in.

**Reference file:** `run_agent.py` — the AIAgent facade. This is the entry point for the entire agent engine, and it's a thin wrapper that delegates to `agent/conversation_loop.py`.

**Learning objectives:**
- Read a Python file and identify its three layers: imports (dependencies), function definitions (exposed interface), function bodies (implementation)
- Explain what `run_agent.py` does without reading every line — it's a facade that delegates to `agent/conversation_loop.py`
- Identify the pattern: a thin entry point that delegates to internal modules

**After completing this sub-module, the student will know:**
- How to approach an unfamiliar source file without being overwhelmed
- What a "facade" is — a thin wrapper that provides a simple interface to a complex system
- That `run_agent.py` is the facade; `agent/conversation_loop.py` is where the loop lives

**After completing this sub-module, the student will have practiced:**
- Opening `run_agent.py` and identifying the imports, function signatures, and the key delegation (`AIAgent` class → `conversation_loop.py`)
- Explaining in plain language what the file does

---

### Sub-Module 15.2: The Registry Pattern — How Tools Get Discovered

**Estimated time:** ~15 minutes  
**Technical level:** Low–Medium

**Concept:** The registry pattern — a central store where components register themselves at import time, and a discovery function that finds them all. This is how Hermes's tool system works: every `tools/*.py` file calls `registry.register()` at the top level, and `discover_builtin_tools()` finds them all automatically.

**Reference files:** `tools/registry.py` (the registry), `tools/web_tools.py` (a real tool file that registers itself)

**Learning objectives:**
- Explain the registry pattern: components register themselves; a discovery function finds them
- Describe why this pattern matters: no manual import list, adding a tool = creating a file, auto-discovery at startup
- Identify the tradeoff: auto-discovery is convenient but means you can't easily see what's loaded without inspecting the registry

**After completing this sub-module, the student will know:**
- What "import-time registration" means — code that runs when a file is first imported, not when a function is called
- Why Hermes uses this pattern for tools (and why the docs say "no manual import list needed")
- The file dependency chain: `tools/registry.py` → `tools/*.py` (registers) → `model_tools.py` (discovers) → `run_agent.py` (uses)

**After completing this sub-module, the student will have practiced:**
- Opening `tools/registry.py` and finding the `register()` function
- Opening `tools/web_tools.py` and finding the `registry.register()` calls at the bottom
- Tracing the dependency chain from registry to discovery to usage

---

### Sub-Module 15.3: Separation of Concerns — Config vs. Secrets vs. State

**Estimated time:** ~15 minutes  
**Technical level:** Medium

**Concept:** Separation of concerns — the principle that different kinds of data belong in different places with different access patterns. Hermes separates config (settings, `config.yaml`), secrets (credentials, `.env`), and state (sessions, `state.db`). Each has a different storage location, a different access pattern, and a different security boundary.

**Reference files:** `hermes_cli/config.py` (config schema and routing), `hermes_state.py` (state database facade)

**Learning objectives:**
- Explain the three-way separation: config (read at startup, user-editable) vs. secrets (read at startup, never exposed) vs. state (read/written throughout, SQLite + FTS5)
- Describe why the separation matters: security (secrets must stay private), performance (config is read once, state is queried), correctness (each has different invariants)
- Identify the design decision: `hermes config set` auto-routes based on naming convention (UPPER_SNAKE → `.env`, dotted → `config.yaml`) — this is a product decision that makes a security boundary feel effortless

**After completing this sub-module, the student will know:**
- What "separation of concerns" means as an engineering principle
- How Hermes applies it: three file types, three storage locations, three access patterns
- How the design decision (auto-routing by naming convention) impacts the user experience (you never have to think about which file — the command knows)

**After completing this sub-module, the student will have practiced:**
- Opening `hermes_cli/config.py` and finding the config routing logic
- Opening `hermes_state.py` and seeing the SQLite facade
- Explaining the separation in their own words

---

### Sub-Module 15.4: Progressive Disclosure — The Three-Level Loading Pattern

**Estimated time:** ~15 minutes  
**Technical level:** Medium

**Concept:** Progressive disclosure — a design pattern where information is revealed in layers of increasing detail, with each layer loaded only when needed. Hermes uses this for skills: Level 0 (names + descriptions, always in context), Level 1 (full skill body, loaded on match), Level 2 (linked reference files, loaded on deeper demand). The pattern trades completeness for efficiency — the system prompt stays small, and detail loads on demand.

**Reference files:** `agent/prompt_builder.py` (assembles the system prompt — includes the skills index), `agent/skill_commands.py` (handles `skill_view` — loads Level 1 and Level 2)

**Learning objectives:**
- Explain progressive disclosure as a design pattern: reveal information in layers, load each layer only when needed
- Describe the three levels in Hermes: Level 0 (catalog, ~3k tokens, always loaded), Level 1 (full body, loaded on match), Level 2 (linked files, loaded on deeper demand)
- Identify the tradeoff: progressive disclosure keeps the system prompt small but means the model might miss a skill if the Level 0 description doesn't trigger the match — this is why the 60-char description limit is a routing signal, not just a cost measure

**After completing this sub-module, the student will know:**
- What "progressive disclosure" means as an engineering pattern (it's not unique to Hermes — it's used in UIs, APIs, and information architecture)
- How Hermes implements it: the skills index is always in the system prompt; the full body loads via `skill_view`; linked files load via `skill_view` with a `file_path` argument
- How the design decision (60-char description limit, Level 0/1/2 split) impacts the user experience: skills load when you need them, don't clutter context when you don't, but a bad description means the skill never gets discovered

**After completing this sub-module, the student will have practiced:**
- Opening `agent/prompt_builder.py` and finding where the skills index is assembled into the system prompt
- Tracing the three levels: what's in the system prompt (Level 0), what loads on `skill_view(name=...)` (Level 1), what loads on `skill_view(name=..., file_path=...)` (Level 2)

---

### Sub-Module 15.5: Inversion of Control — Who Calls Whom

**Estimated time:** ~20 minutes  
**Technical level:** Medium–High

**Concept:** Inversion of control — the principle that a framework (or runtime) calls your code, rather than your code calling the framework. In Hermes, the AIAgent calls tools, loads skills, and manages the conversation loop. The tools and skills don't call the agent — the agent calls them. The entry points (CLI, gateway, ACP) call the AIAgent, not the other way around. This inversion is what makes the architecture "platform-agnostic" — the agent doesn't know which surface it's serving.

**Reference files:** `agent/conversation_loop.py` (the loop that calls tools and manages turns), `model_tools.py` (the dispatch that routes tool calls to handlers)

**Learning objectives:**
- Explain inversion of control: the runtime calls your code, not the other way around
- Describe how Hermes applies it: the conversation loop calls tools (via `model_tools.handle_function_call()`), loads skills (via `skill_view`), and manages turns — the tools and skills don't drive the process, the loop does
- Identify the design decision: the platform-agnostic core. The AIAgent doesn't know whether it's serving the CLI, the gateway, or ACP. Platform differences live in the entry points. This is inversion of control applied to surfaces — the entry point adapts to the agent, not the agent to the entry point
- Trace the user experience impact: because the core is agnostic, a session started in the CLI can be resumed from Telegram. The agent doesn't care which surface you're using — it processes the same conversation either way

**After completing this sub-module, the student will know:**
- What "inversion of control" means and how to spot it (the runtime calls you; you don't call the runtime)
- How Hermes applies it to tools (the loop calls `handle_function_call`), skills (the loop calls `skill_view`), and surfaces (the entry point calls `run_conversation`)
- How the "platform-agnostic core" design decision (from Module 11) is an application of inversion of control — and how it enables cross-surface session persistence

**After completing this sub-module, the student will have practiced:**
- Opening `agent/conversation_loop.py` and tracing where the loop calls tools (the `handle_function_call` dispatch point)
- Identifying the inversion: the loop is in control; tools, skills, and surfaces are all called *by* the loop, not the other way around
- Explaining how this enables the "one session, many surfaces" user experience

---

### Sub-Module 15.6: Design Decisions and Their Tradeoffs — The Frozen Snapshot

**Estimated time:** ~20 minutes  
**Technical level:** High

**Concept:** Every design decision has a tradeoff — something gained and something lost. This sub-module examines three specific design decisions in Hermes, what they gain, what they cost, and how the cost manifests as user experience. The goal is to teach the student to think like an engineer: not "what does this code do?" but "what did this decision gain, and what did it give up?"

**Reference files:** `agent/prompt_builder.py` (frozen snapshot — memory loaded once, never re-read), `agent/prompt_caching.py` (Anthropic prompt caching — the reason for the freeze), `agent/context_compressor.py` (compression — the consequence of context windows)

**Three design decisions to examine:**

**Decision 1: The Frozen Snapshot (memory loaded once, never re-read mid-session)**
- **What it gains:** Prompt cache stability. The system prompt stays byte-identical for the life of a conversation, so the provider's prefix cache never breaks. This saves tokens and latency on every turn after the first.
- **What it costs:** Memory writes during a session don't appear until the next session. If you tell me to remember something at 2pm, it's on disk immediately but invisible to the running session. The user experience: "I told it to remember, and it forgot" — which the docs explicitly call out as the most common support issue.
- **The tradeoff:** Cache stability vs. real-time memory visibility. Hermes chose cache stability because the alternative (re-reading memory every turn) would break the cache and cost more tokens than the memory is worth.

**Decision 2: Progressive Disclosure (skills load in three levels)**
- **What it gains:** A small system prompt. ~3k tokens for the entire skill catalog vs. potentially tens of thousands if all skills loaded fully. The baseline stays cheap.
- **What it costs:** The model might not discover a skill if the Level 0 description doesn't trigger the match. A skill with a vague description is loaded less often. The user experience: "why didn't it use the skill I installed?" — because the description didn't match the task.
- **The tradeoff:** Baseline cost vs. discovery reliability. Hermes chose a small baseline and a 60-char description limit — forcing skill authors to be precise about what the skill is for.

**Decision 3: Platform-Agnostic Core (one AIAgent for all surfaces)**
- **What it gains:** Cross-surface session persistence. A session started in the CLI can be resumed from Telegram. The agent doesn't know or care which surface you're using. One engine, one session store, one set of tools.
- **What it costs:** Platform-specific features are harder to add. If Telegram has a capability the CLI doesn't (voice messages, inline keyboards), the agent can't use it without the entry point handling it. The user experience: some features are surface-specific (voice mode on Telegram, shell mode in the CLI) and can't be ported across surfaces.
- **The tradeoff:** Cross-surface compatibility vs. platform-specific optimization. Hermes chose compatibility — one engine for all surfaces — and accepts that platform-specific features live in the entry point, not the agent.

**Learning objectives:**
- Explain what a design tradeoff is: something gained and something lost
- Trace three specific Hermes decisions to their user-experience consequences
- Identify the pattern: every engineering decision is a tradeoff, and the user experience is where the cost shows up

**After completing this sub-module, the student will know:**
- That "the frozen snapshot" is a prompt caching decision with a UX cost (memory not visible mid-session)
- That "progressive disclosure" is a token-cost decision with a UX cost (skills might not be discovered)
- That "platform-agnostic core" is a compatibility decision with a UX cost (platform-specific features live in the entry point)
- The meta-pattern: engineering decisions are tradeoffs, and the user experience is where the tradeoff's cost becomes visible

**After completing this sub-module, the student will have practiced:**
- Reading `agent/prompt_builder.py` and identifying where the frozen snapshot is implemented
- Reading `agent/prompt_caching.py` and understanding why the freeze exists (Anthropic prompt caching)
- Explaining the three tradeoffs in their own words — what each decision gains, what it costs, and how the cost shows up as user experience

---

## Assessment

**Knowledge check:** The student is given a short Hermes source file (or a trimmed excerpt) they haven't seen during the sub-modules. They read it and answer three questions:

1. What is this code doing? (Structural explanation, not line-by-line)
2. What engineering concept or pattern is it an example of? (From the sub-modules: facade, registry, separation of concerns, progressive disclosure, inversion of control, tradeoff)
3. How does this design decision impact the user experience? (What does the user feel because of this choice?)

**Skills check:** The student picks a Hermes concept they've learned during the course (the frozen snapshot, progressive disclosure, platform-agnostic core, the registry pattern) and traces it from concept to source file to user experience. The instructor verifies the trace is accurate by reading the same files.

---

## The Through-Line

Sub-modules 15.1 through 15.6 escalate from "how to read a file" to "how to think about design decisions." The through-line is:

1. **15.1** — How to read a file (outside-in: imports → signatures → body)
2. **15.2** — What pattern is this? (registry: components register, a function discovers)
3. **15.3** — Why is the data separated? (separation of concerns: config, secrets, state)
4. **15.4** — Why doesn't everything load at once? (progressive disclosure: load on demand)
5. **15.5** — Who's in control? (inversion of control: the runtime calls you)
6. **15.6** — What did this decision cost? (tradeoffs: every gain has a cost, and the cost shows up as UX)

By the end, the student can: read a source file, identify the pattern it embodies, explain the design decision behind it, and trace how that decision impacts what the user feels. That's the skill set for speaking intelligently to engineers — not "how do I write this code?" but "why did you choose this, and what does it cost?"

---

*Sub-module curriculum for Module 15 of the Hermes Agent Learning Path. Designed for a student with elementary code-reading ability who wants to understand engineering concepts, patterns, and design decisions — not how to code.*
