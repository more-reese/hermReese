# Config

How my Hermes is set up. Sanitized — no keys, tokens, or secrets.

## Model and provider

- **Model:** GLM-5.2 (z-ai)
- **Provider:** inference API (default)
- **Base URL:** (provider inference endpoint)
- **API mode:** Chat completions

I use my default inference endpoint. The provider is provider-agnostic in Hermes — I can swap models mid-workflow if a task calls for a different model's strengths.

## Runtime

- **Platform:** macOS
- **Terminal backend:** local (not containerized)
- **Timeout:** 180s default
- **Agent max turns:** 500
- **Reasoning effort:** medium
- **Compression:** enabled (context compression kicks in at 50% of context window)

## Skills

I have skills across 12 categories. The ones I've built or contributed to are in [artifacts/skills/](../artifacts/skills/). The full set:

| Category | Skills |
|---|---|
| Apple | apple-notes, apple-reminders, findmy, imessage |
| Autonomous AI agents | claude-code, codex, computer-use, hermes-agent, opencode |
| Creative | architecture-diagram, ascii-video, baoyu-infographic, claude-design, design-md, humanizer, manim-video, p5js, popular-web-designs, songwriting-and-ai-music |
| DevOps | sdlc-review |
| Email | email-inbox-triage, himalaya |
| Media | gif-search, songsee, youtube-content |
| Note-taking | obsidian |
| Productivity | airtable, box, document-to-action-items, docx, google-workspace, job-application-strategy, maps, meeting-action-items, notion, pdf, powerpoint, product-price-monitor, telegram-share, teams-meeting-pipeline, weekly-review-planning, xlsx |
| Research | arxiv, competitor-news-monitor, grounded-citations, llm-wiki, pattern-language, webprotege |
| Social media | xurl |
| Software development | codebase-inspection, dogfood, github, hermes-agent-skill-authoring, inspecting-hermes-desktop-dom, mcp-server, node-inspect-debugger, python-debugpy, requesting-code-review, simplify-code, spike, systematic-debugging, test-driven-development |
| Web | blocked-page-recovery |

## Persistent memory

Hermes has two memory stores: `MEMORY.md` (my notes — environment, conventions, lessons) and `USER.md` (who I am — preferences, background, how to work with me). Both persist across sessions and load into every new session's context. See [memory.md](memory.md) for what's actually in them.

## Cron

Hermes supports scheduled jobs via cron. I have a heartbeat ticker running — the infrastructure is set up and working, though I haven't built out recurring scheduled tasks yet. The `executions.db` SQLite database tracks run history.

## What this shows

The config is the "use it daily" evidence. It's not a test drive — it's a working setup with a real model, real skills, real memory, and real cron infrastructure. The skills I've built myself ([artifacts/skills/](../artifacts/skills/)) are the ones that shape how I work; the rest are installed capabilities I use when the task calls for them.
