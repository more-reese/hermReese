# Projects

Shipped projects built with or through Hermes Agent. These aren't demos — they're real tools I use, built through Hermes sessions, with the git history showing the agent as collaborator.

## Projects

| Project | What it is | Repo |
|---|---|---|
| **substrate** | Describe a system in plain English; get a versioned graph model with JSON/Markdown/Mermaid/Python output. | [github.com/more-reese/substrate](https://github.com/more-reese/substrate) |
| **vsm-translator** | Desktop app that keeps plain-language process text and BPMN/VSM diagrams in sync, both directions. Built with Electron + Vite. | [github.com/more-reese/vsm-translator](https://github.com/more-reese/vsm-translator) |
| **lenswork** | Multi-pass reasoning pipeline that weighs quality against cost with per-stage model choice. Every claim labeled by evidence type so output can be checked. | [github.com/more-reese/lenswork](https://github.com/more-reese/lenswork) |
| **dreamward** | A comparative atlas of dream traditions — 32 traditions mapped across 8 clusters with graph, matrix, interpret, and comparator views. | [github.com/more-reese/dreamward](https://github.com/more-reese/dreamward) |
| **formology** | The study of form as the atomic unit — a framework investigating what form is, how it gets its meaning from context, and what stays the same when the instance changes. Emerged from re-translating Stafford Beer's VSM. Includes a field survey of 20+ prior-art fields, 5 shared cases, stress tests of 7 hypotheses, and an OWL ontology. | [github.com/more-reese/formology](https://github.com/more-reese/formology) |

## How Hermes was involved

Each project was built through Hermes Agent sessions — not by writing code manually and pushing it, but by working with the agent to design, implement, test, and ship. The Co-Authored-By trailers on commits reflect this: the agent is a collaborator, not a tool.

The publish process for substrate, vsm-translator, and lenswork was itself a Hermes session — a detailed pre-publish review covering:

- **Secrets scanning** — gitleaks on the working tree and staged changes
- **Clean-install verification** — `npm ci` from scratch, dependency install, build run
- **Test execution** — typecheck, build, and runtime checks
- **Personal data audit** — checking for client names, API keys, real project data
- **Screenshot capture** — documenting the UI for the README

This process is documented in a publish-review file that's over 60KB — evidence that shipping through an agent means verifying the agent's work, not trusting it.

## What this shows

These projects demonstrate the "hands-on experience building or shipping AI agent products" qualification from the PM role. They're not toys:

- **substrate** — 8 Python files, ~2,100 lines, a versioning tool with a growing lexicon and provenance tracking
- **vsm-translator** — 42 TypeScript files, ~7,270 lines, a desktop app with bidirectional sync and conflict resolution
- **lenswork** — 52 TypeScript files, ~8,340 lines, a Next.js app with per-stage model choice and evidence labeling
- **dreamward** — a data atlas with an API server, graph/matrix/interpret/comparator views
- **formology** — a research framework with field survey, stress tests, shared cases, and an OWL ontology; evolved through two research passes (v0.3.0 initial + v0.4.0 collaborator review) and four practice-level case studies (register "issue"/"case"/"charge" + purchase order with reader-as-context); the deepest "thinking with Hermes" project to date

Each one was designed, built, and shipped through conversations with Hermes. The through-line: I build with agents because thinking and making are the same act when the tool gets out of the way.
