# Hermes Agent Learning Path — Course Curriculum

**Course Code:** HMA-101  
**Format:** Guided, self-paced with dual assessment (knowledge + practical skills)  
**Prerequisites:** None  
**Estimated Duration:** 7–10 hours across three tiers  
**Assessment:** Pass / Partial / Retry for each module (both knowledge and skills checks must pass)  

---

## Course Description

Hermes Agent is an open-source AI agent framework that uses tool calling to interact with your system — reading files, running shell commands, searching the web, and driving browsers. This course teaches Hermes from first principles: what it is, how it works internally, and how to extend it. Students learn through a structured cycle of reading, hands-on practice, and dual assessment that verifies both understanding and practical ability.

The course follows three tiers — Beginner, Intermediate, and Advanced — each building on the last. Students do not skip tiers. Each module follows a consistent cycle: **learn → practice → assess → record**.

---

## Course Structure

| Tier | Modules | Goal | Est. Time |
|------|---------|------|-----------|
| Beginner | 1–4 | Get up and running, have basic conversations, use built-in tools | ~1 hour |
| Intermediate | 5–10 | Set up messaging bots, use advanced features like memory, cron jobs, and skills | ~2–3 hours |
| Advanced | 11–14 | Build custom tools, create skills, understand internals, contribute to the project | ~4–6 hours |

---

## Assessment Protocol

Each module includes two assessments:

**Knowledge Check (understanding)**
The student explains the concept back in their own words. The instructor checks for:
- First-principles understanding — not "what command does X" but "why does X work this way"
- Accurate mental model — does the explanation match how Hermes actually works?
- Boundary awareness — can the student explain what the feature does AND doesn't do?

Score: **pass** / **partial** / **retry**

**Skills Check (practical ability)**
The student completes a hands-on exercise. The instructor verifies the output with a real tool call — not self-reported.

Score: **pass** / **partial** / **retry**

A module is **complete** when both checks pass (partial counts as pass with a note).

---

## Tier I: Beginner (~1 hour)

**Goal:** Get up and running, have basic conversations, use built-in tools.  
**Assumes:** Nothing.

---

### Module 1: Installation

**Doc:** [Installation](https://hermes-agent.nousresearch.com/docs/getting-started/installation)

**Description:**  
Students learn what Hermes Agent is — an AI agent framework that uses tool calling to interact with computer systems — and how it installs on their machine. Covers the shell installer, what it bootstraps (Python, dependencies, browser tools), what it needs (Python 3.14, a model provider), and where everything lives on the filesystem.

**Learning Objectives:**
- Define what Hermes Agent is and what problem it solves
- Explain the difference between an agent and a chatbot (action vs. text)
- Describe how the installer works and what it bootstraps
- Identify the key filesystem locations (`~/.hermes/`, `config.yaml`, `.env`, `state.db`)

**After completing this module, the student will know:**
- What Hermes Agent is and why dependency isolation (pinned Python) matters
- The core distinction: a chatbot produces text, an agent produces effects
- Where Hermes lives on the filesystem and what each path contains

**After completing this module, the student will have practiced:**
- Running `hermes doctor` to verify a healthy installation
- Running `hermes --version` to confirm the install

---

### Module 2: Quickstart

**Doc:** [Quickstart](https://hermes-agent.nousresearch.com/docs/getting-started/quickstart)

**Description:**  
Students learn the interaction loop — the ReAct pattern that powers every Hermes conversation: input → [reason → act → observe → reason] → output. Covers one-shot queries (`hermes chat -q`), interactive sessions, what a tool call looks like in practice, and tool chaining (where each tool result informs the next decision).

**Learning Objectives:**
- Describe the interaction loop from first principles (ReAct pattern)
- Distinguish one-shot queries from interactive sessions
- Explain what tool chaining is and how each result informs the next decision
- Identify what success looks like (banner, response, tool usage, multi-turn)

**After completing this module, the student will know:**
- The ReAct loop: input → [reason → act → observe → reason] → output
- That one-shot is transactional, multi-shot is interactional
- That tool chaining means each result informs the next decision — the model doesn't plan all calls upfront

**After completing this module, the student will have practiced:**
- Running a one-shot query (`hermes chat -q`)
- Starting an interactive session and having a tool-using conversation

---

### Module 3: CLI Usage

**Doc:** [CLI Usage](https://hermes-agent.nousresearch.com/docs/user-guide/cli)

**Description:**  
Students learn the command-line interface — the command structure, key commands, session navigation, and the two terminal interfaces (classic CLI and modern TUI). Covers `--continue` vs `--resume`, slash commands, shell mode (`!` prefix), and keybindings.

**Learning Objectives:**
- Navigate the CLI command structure (`hermes <command> [flags]`)
- Distinguish `--continue` (most recent session) from `--resume <id>` (specific session)
- Use slash commands inside a session (`/help`, `/model`, `/tools`, `/bg`, `/btw`)
- Use shell mode (`!` prefix) to run commands without invoking the model
- Identify the two terminal interfaces (classic CLI vs TUI) and when to use each

**After completing this module, the student will know:**
- The difference between `--continue` and `--resume` and when to use each
- That `!` prefix runs shell commands at zero token cost AND keeps context clean
- How slash commands work and which ones are most useful day-to-day

**After completing this module, the student will have practiced:**
- Exploring the command tree with `hermes --help`
- Starting, exiting, and resuming a session
- Using shell mode (`!git status`, `!ls -la`)

---

### Module 4: Configuration

**Doc:** [Configuration](https://hermes-agent.nousresearch.com/docs/user-guide/configuration)

**Description:**  
Students learn the config/secrets split — the security boundary between settings (`config.yaml`) and secrets (`.env`). Covers how `hermes config set` routes values automatically, the configuration precedence order, and why you never hand-edit `config.yaml`.

**Learning Objectives:**
- Explain the config/secrets split and why it's a security boundary
- Describe how `hermes config set` routes values (UPPER_SNAKE → `.env`, dotted → `config.yaml`)
- State the configuration precedence order: CLI args > config.yaml > .env > defaults
- Explain why hand-editing `config.yaml` is dangerous (YAML is whitespace-sensitive)

**After completing this module, the student will know:**
- That the config/secrets split is security — secrets in config.yaml would leak when shared or committed
- That `hermes config set` auto-routes based on naming convention
- The four-level precedence order and how CLI flags override persistent settings

**After completing this module, the student will have practiced:**
- Viewing their current config
- Changing a setting with `hermes config set` and verifying it took effect

---

## Tier II: Intermediate (~2–3 hours)

**Goal:** Set up messaging bots, use advanced features like memory, cron jobs, and skills.  
**Assumes:** Beginner tier complete.

---

### Module 5: Sessions

**Doc:** [Sessions](https://hermes-agent.nousresearch.com/docs/user-guide/sessions)

**Description:**  
Students learn the session lifecycle — how conversations persist, how to resume them, and the critical distinction between session context and persistent memory. Covers the SQLite session store (`state.db`), session sources (cli, telegram, cron, etc.), cross-platform handoff, and context compression.

**Learning Objectives:**
- Describe the session lifecycle: start → work → exit → resume
- Distinguish what persists within a session (conversation history) from what persists across sessions (memory, skills, config)
- Explain how all surfaces (CLI, TUI, desktop, Telegram) share one `state.db` per profile
- Describe what context compression does and how session lineage works
- Explain per-terminal `--continue` behavior

**After completing this module, the student will know:**
- That session context is not memory — `/new` starts fresh, but memory and skills persist
- That all sessions in a profile share one SQLite database
- How compression creates lineage (`"my project" → "my project #2"`)
- That persistence is intentional — memory is written by a deliberate act, not auto-extracted

**After completing this module, the student will have practiced:**
- Starting a session, having a multi-turn conversation, exiting, and resuming it
- Verifying that context persisted on resume

---

### Module 6: Messaging

**Doc:** [Messaging](https://hermes-agent.nousresearch.com/docs/user-guide/messaging/)

**Description:**  
Students learn the gateway model — how one Hermes instance serves multiple messaging platforms (Telegram, Discord, Slack, etc.). Covers what's shared across surfaces (tools, memory, skills) vs what's per-platform, the security boundary (who can talk to your bot), and cross-platform handoff.

**Learning Objectives:**
- Explain the gateway model: one agent core, many platform connections
- Describe what's shared across surfaces and what's isolated per-platform
- Explain the security boundary (authorized users, allowlists)
- Describe how `/handoff` transfers a live session between surfaces

**After completing this module, the student will know:**
- How one agent serves multiple platforms through the gateway
- What the gateway shares (tools, memory, skills) vs what it isolates (sessions, routing)
- How to transfer a live conversation from CLI to Telegram and back

**After completing this module, the student will have practiced:**
- Verifying an existing Telegram connection works end-to-end
- Understanding what tools are available through the Telegram gateway

---

### Module 7: Tools

**Doc:** [Tools](https://hermes-agent.nousresearch.com/docs/user-guide/features/tools)

**Description:**  
Students learn what tools are — callable functions with schemas that the agent can invoke — and how tool calling is the core mechanism that makes Hermes an agent, not just a chatbot. Covers how the model decides which tool to call, what tools are available built-in, and how tools chain.

**Learning Objectives:**
- Define what a tool is: a callable function with a schema
- Explain how the model decides which tool to call (it reasons about the schema)
- List categories of built-in tools (file I/O, search, shell, browser, etc.)
- Explain tool chaining and how each result informs the next decision

**After completing this module, the student will know:**
- That tool calling is the bridge from thought to action — what makes it an agent
- How the model reasons about tool schemas to pick the right one
- That tool chaining is dynamic — each result informs the next call, not planned upfront

**After completing this module, the student will have practiced:**
- Using 3+ different tools in a single session
- Observing how the agent picks tools and chains them

---

### Module 8: Skills

**Doc:** [Skills](https://hermes-agent.nousresearch.com/docs/user-guide/features/skills)

**Description:**  
Students learn what skills are — reusable procedure packages that load contextually when relevant — and how they differ from tools. Covers the SKILL.md format (frontmatter + body + linked files), the contextual loading mechanism, and the difference between skills (procedures/knowledge) and tools (functions).

**Learning Objectives:**
- Define what a skill is and how it differs from a tool
- Explain the contextual loading model (triggered by relevance, not always-on)
- Describe the SKILL.md format (YAML frontmatter + markdown body + linked files)
- Explain why contextual loading matters (cost/benefit of loading only when relevant)

**After completing this module, the student will know:**
- That skills are procedures/workflows that load when the topic matches
- That tools are functions the agent calls; skills are knowledge the agent loads
- Why contextual loading is more efficient than loading everything always

**After completing this module, the student will have practiced:**
- Loading a skill with `skill_view(name='...')` and examining its structure
- Identifying the frontmatter, body, and linked files

---

### Module 9: Memory

**Doc:** [Memory](https://hermes-agent.nousresearch.com/docs/user-guide/features/memory)

**Description:**  
Students learn persistent memory — what it stores (who you are, preferences, environment), what it doesn't (task-specific state, transient info), and the memory/skill/session boundary. Covers how memory gets injected into every new session's system prompt and how it differs from session context.

**Learning Objectives:**
- Define what persistent memory is and what it stores
- Explain what memory is NOT for (transient state, task progress, logs)
- Describe the memory/skill/session boundary: what persists where, and why
- Explain how memory gets injected into every new session

**After completing this module, the student will know:**
- That memory is profile-scoped, deliberately written, and injected into every session
- That persistence is intentional, not implicit — nothing is auto-extracted
- The boundary: memory (every session) vs skills (contextual) vs session (this conversation only)

**After completing this module, the student will have practiced:**
- Adding a memory entry about a preference or fact
- Verifying it appears in a new session's context

---

### Module 10: Cron

**Doc:** [Cron](https://hermes-agent.nousresearch.com/docs/user-guide/features/cron)

**Description:**  
Students learn the cron system — durable scheduled jobs that run without the user being present. Covers schedule types (duration, every phrase, 5-field cron, ISO timestamp), when to use cron vs delegation vs a session, and per-job configuration knobs.

**Learning Objectives:**
- Define what cron is: durable scheduled jobs that survive restarts
- Describe the schedule types (duration, every phrase, cron syntax, ISO timestamp)
- Distinguish cron from delegation and sessions — when to use each
- Identify per-job knobs (skills, model/provider override, workdir)

**After completing this module, the student will know:**
- That cron is durable — it survives restarts and runs without the user present
- When to use cron (recurring, autonomous) vs delegation (parallel subtasks) vs session (interactive)
- That cron jobs run in fresh sessions with no chat context — prompts must be self-contained

**After completing this module, the student will have practiced:**
- Creating a simple cron job
- Verifying it runs successfully

---

## Tier III: Advanced (~4–6 hours)

**Goal:** Build custom tools, create skills, understand internals, contribute to the project.  
**Assumes:** Intermediate tier complete.

---

### Module 11: Architecture

**Doc:** [Architecture](https://hermes-agent.nousresearch.com/docs/developer-guide/architecture)

**Description:**  
Students learn the internal structure of Hermes — the agent core, gateway, surfaces, and tools. Covers the full request flow from user message to tool execution to response, how surfaces share the same core, and where the extensibility points are.

**Learning Objectives:**
- Describe the internal structure (agent core, gateway, surfaces, tools)
- Trace the request flow: user message → model → tool call → execution → response → user
- Explain how surfaces (CLI, desktop, messaging) share the same core
- Identify the extensibility points (skills, plugins, MCP, tools)

**After completing this module, the student will know:**
- The full request flow from prompt to tool execution
- Where the model fits, where the gateway fits, where skills load
- How the same core powers every surface

**After completing this module, the student will have practiced:**
- Tracing a tool call through the system mentally, step by step

---

### Module 12: Adding Tools

**Doc:** [Adding Tools](https://hermes-agent.nousresearch.com/docs/developer-guide/adding-tools)

**Description:**  
Students learn the tool registration pattern — how tools get defined, discovered, and called. Covers tool schemas (name, description, parameters), the difference between built-in tools and plugin tools, and how the agent discovers available tools at runtime.

**Learning Objectives:**
- Describe the tool registration pattern
- Explain tool schemas (name, description, parameters)
- Describe how the agent discovers and calls tools at runtime
- Distinguish built-in tools from plugin tools

**After completing this module, the student will know:**
- How a tool gets registered and called
- The schema format and how the model uses it to decide which tool to call
- The difference between built-in and plugin tools

**After completing this module, the student will have practiced:**
- Reading the adding-tools documentation and understanding the pattern

---

### Module 13: Creating Skills

**Doc:** [Creating Skills](https://hermes-agent.nousresearch.com/docs/developer-guide/creating-skills)

**Description:**  
Students learn to create skills from scratch — the SKILL.md format, YAML frontmatter, linked reference files, and the contextual loading mechanism. Covers best practices: lessons not logs, imperative rules, concise descriptions, and proper structure.

**Learning Objectives:**
- Describe the SKILL.md format: YAML frontmatter + markdown body + linked files
- Explain the frontmatter fields (name, description, version, tags, metadata)
- Describe linked files (references/, templates/, scripts/) and when to use them
- Explain the contextual loading mechanism and how relevance is determined
- Identify best practices (lessons not logs, one rule per lesson, concise descriptions)

**After completing this module, the student will know:**
- Why frontmatter matters (routing, discovery, description truncation rules)
- Why linked files matter (loading additional context on demand)
- How the loading mechanism decides when to load a skill

**After completing this module, the student will have practiced:**
- Creating a simple skill from scratch with proper frontmatter and structure
- Optionally adding a linked reference file

---

### Module 14: Contributing

**Doc:** [Contributing](https://hermes-agent.nousresearch.com/docs/developer-guide/contributing)

**Description:**  
Students learn how to contribute to Hermes Agent itself — the development workflow (fork, branch, PR), testing requirements, and code standards. Covers the full process from idea to merged pull request.

**Learning Objectives:**
- Describe the contribution workflow (fork, branch, PR)
- Identify testing requirements and code standards
- Explain the steps from idea to merged pull request

**After completing this module, the student will know:**
- The full contribution workflow
- How to set up a development environment
- What standards contributions must meet

**After completing this module, the student will have practiced:**
- Reading the contributing guidelines and understanding the process

---

## Bonus Module: Reading Code

**Goal:** Read, understand, and explain what code does — not write it.  
**Assumes:** Elementary understanding of code (can read basic Python, knows what a function/variable/import is).  
**Primary Reference:** The Hermes Agent source code at `~/.hermes/hermes-agent/`  
**Prerequisite:** Tier I (Beginner) complete. Does not require Tier II or III — this module can be taken after Module 4.

---

### Module 15: Reading and Explaining Code

**Reference:** `~/.hermes/hermes-agent/` (the installed Hermes source)

**Description:**  
Students learn to read code the way an architect reads blueprints — not to build, but to understand. What is this code doing? How does it interact with and contribute to the entire system? What pattern is it an example of? The module uses the Hermes Agent source code as the primary reference, walking through real files the student has been using all course: the CLI entry point, the session store, the tool dispatcher, the skill loader. Students don't write code — they explain it.

The goal is not literacy in Python the programming language. The goal is literacy in systems: what does this file do, why does it exist, what pattern does it instantiate, and how does it connect to the other moving parts the student has already learned about in Modules 1–14?

**Learning Objectives:**
- Read a source file and explain in plain language what it does (not line-by-line, but structurally)
- Identify the role a file or function plays in the larger system (where does it sit in the request flow from Module 11?)
- Recognize common patterns in the codebase: the tool registration pattern (Module 12), the skill loading pattern (Module 8), the config/secrets split (Module 4), the session storage pattern (Module 5)
- Distinguish between "what this code does" and "what pattern it's an example of" — the concrete vs. the abstract
- Map code structure to the concepts already learned: trace how `hermes --continue` actually finds a session, how `hermes config set` routes a value, how `skill_view` loads a SKILL.md file

**After completing this module, the student will know:**
- How to approach an unfamiliar source file: read the imports (what does it depend on?), read the function signatures (what does it expose?), read the body of the most important function (what does it actually do?)
- How to connect code to the mental models from the course: the interaction loop, the session store, the config/secrets split, the skill loading mechanism, the tool dispatch system
- That you can understand a system by reading its code without being able to write code for that system — the same way you can understand how a car engine works without being able to build one
- Which patterns from the course appear in the codebase and where: the ReAct loop lives in the agent core, the session store lives in `state.db` accessed through the sessions module, the skill loading lives in the skills directory scanned at startup, the config routing lives in the config module

**After completing this module, the student will have practiced:**
- Reading a specific Hermes source file (e.g., the CLI entry point or the session store module) and explaining what it does in plain language
- Identifying which course concept the file implements (e.g., "this is the session store — it reads and writes `state.db`, which is the SQLite database from Module 5")
- Tracing one real code path: pick a command the student has used (`hermes --continue`, `hermes config set`, `skill_view`) and follow it from the CLI entry point through to where it actually does the thing
- Explaining the pattern a file instantiates: "This is the tool registration pattern from Module 12 — here's where tools get defined, here's where they get discovered, here's where they get called"

**Assessment:**

**Knowledge check:**
The student is given a short Hermes source file (or a trimmed excerpt) they haven't seen during the module. They read it and answer three questions in their own words:
1. What is this code doing? (Structural explanation, not line-by-line)
2. How does it interact with and contribute to the entire system? (Where does it sit in the architecture from Module 11?)
3. What pattern is it an example of? (Connect it to a concept from the course)

**Skills check:**
The student picks a Hermes command they've used during the course (e.g., `hermes --continue`, `hermes config set`, `skill_view`) and traces it through the source code — from the CLI entry point to where it actually does the work. The instructor verifies the trace is accurate by reading the same files.

**Why this module exists:**

Modules 1–14 teach what Hermes does. This module teaches how to see what it is — by reading the code that makes it work. The student has spent the course building mental models: the interaction loop, the session store, the config split, the skill loader. This module connects those mental models to the actual source files that implement them.

The purpose is not to make the student a programmer. The purpose is to make the student a reader — someone who can look at a codebase and understand it well enough to explain it, make product decisions about it, and ask better questions about how it works. That's the same skill set the course has been building all along, applied to the code itself instead of the docs.

---

## Grading Scale

| Score | Meaning |
|-------|---------|
| **Pass** | Student can explain the concept clearly and complete the exercise independently. |
| **Partial** | Student gets the core idea but misses details, or completes the exercise with help. Still counts as complete — the note captures what's incomplete. |
| **Retry** | Important gaps in understanding or inability to complete the exercise. We go back to Learn with the specific gap. |

A module is **complete** when both the knowledge check and skills check pass (partial counts). A tier is complete when all its modules are complete. The course is complete when all three tiers are complete.

---

## Progress Tracking

Progress is tracked in two places:

- **hermReese** (`surface/learning-path/progress.md`) — the durable, public trace. Each completed module records: module name, tier, status, knowledge score, skills score, date, and a one-line note in the student's own words. The git history is the longitudinal record.
- **Memory** — a single entry stores the student's current position (tier + next module). Every new session reads it and knows where to pick up.

---

*Derived from the [official Hermes Agent learning path](https://hermes-agent.nousresearch.com/docs/getting-started/learning-path).*
