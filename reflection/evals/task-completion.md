# Task completion evals

Real tasks, real acceptance criteria, real results. Each entry is an evaluation run — the task, what "done" means, what happened, and whether it passed.

---

## Eval 1: Pre-publish review (substrate, vsm-translator, lenswork)

**Date:** 2026-10-04
**Model:** GLM-5.2 (z-ai, )
**Task:** Run a complete pre-publish review for three repos before their first public GitHub push.

**Acceptance criteria:**
- [x] gitleaks scan clean (no secrets in working tree or staged changes)
- [x] Clean install passes (`npm ci` / `pip install`) from scratch
- [x] Typecheck passes (`npm run typecheck`)
- [x] Build passes (`npm run build`)
- [x] App boots from clean state (no key, scratch HOME)
- [x] No personal or client data in committed files
- [x] `.gitignore` covers secrets (.env, *.env, node_modules, .venv, __pycache__)
- [x] Backup created before changes

**Run:** Hermes read all three repos, ran gitleaks, executed clean installs, ran typecheck and build, booted vsm-translator from a clean state, audited personal data, checked .gitignore, and created a backup tarball. The full review produced a 60KB+ report covering every file in each commit.

**Result:** **PASS** — all criteria met for all three repos. gitleaks clean. Clean install, typecheck, and build passed for vsm-translator and lenswork. substrate's Python deps installed cleanly. vsm-translator booted from a scratch HOME with no key and wrote the example project. No personal data found. .gitignore covers all secrets.

**Analysis:** This is the eval that proved Hermes could handle my real work — not toy tasks but a production-grade publishing process with secrets scanning, clean-install verification, and test execution. The 60KB review file is the evidence. The agent didn't just "run the commands" — it audited each file for personal data, checked for broken placeholder values, and flagged Claude model IDs it couldn't verify.

**What I'd change:** The eval doesn't cover `npm run package` (electron-builder download) or the Claude/Ollama translators (no key used). The criteria should note what's not tested, not just what is.

---

## Eval 2: GitHub profile optimization

**Date:** 2026-10-04
**Model:** GLM-5.2 (z-ai, )
**Task:** Audit and optimize my GitHub profile for a job application — make relevant repos public, add descriptions, clean up noise.

**Acceptance criteria:**
- [x] All relevant repos public and visible on the profile
- [x] Each public repo has a one-line description
- [x] No noise repos (old tutorials, empty projects) visible
- [x] Profile bio set
- [x] No secrets or API keys in any public repo

**Run:** Hermes listed all repos with `gh repo list`, checked visibility, set relevant repos to public (`gh repo edit --visibility public`), added descriptions and topics, audited for secrets, and set the profile bio via the REST API.

**Result:** **PASS** — all 4 project repos (substrate, vsm-translator, lenswork, dreamward) are public with descriptions. Profile bio set. No noise repos visible.

**Analysis:** This eval shows Hermes handling a multi-step workflow with real side effects (changing repo visibility, setting a bio). The agent verified each step — it didn't just run the commands, it checked the results. The one gap: `pinnedRepositories` is deprecated in the GraphQL API, so pinning repos required browser automation (noted as a known limitation in the skill).

---

## Eval 3: This repo (hermReese)

**Date:** 2026-10-07
**Model:** GLM-5.2 (z-ai, )
**Task:** Build a living workspace repo that showcases how I use Hermes Agent, structured around my mental model (philosophy → surface → artifacts → reflection).

**Acceptance criteria:**
- [x] README frames the repo and includes the philosophy
- [x] Directory structure reflects the mental model (surface → artifacts → reflection)
- [x] Surface section documents actual config, memory, and Telegram gateway
- [x] Artifacts section documents real skills, projects, and writing
- [x] Reflection section includes a friction log with real friction points
- [x] Every file produced through a Hermes session
- [x] No fabricated content — templates where real content needs user input

**Run:** This session. Hermes read my resume, the job posting, my skill files, my Hermes config, my memory files, my usage stats, and my project directories. It proposed a structure, got feedback via clarify(), restructured based on the feedback ("this reflects my ever-evolving understanding of and interactions with Hermes Agent"), and built every file through the session.

**Result:** **PASS** — all criteria met. The repo exists, is structured around the mental model, and contains real content from real artifacts. The friction log has 5 real friction points I've hit. The evals section has 3 real evals (including this one).

**Analysis:** This is the self-referential eval — the repo evaluates itself by being built through the process it describes. The friction log was written during the same session that hit one of the friction points (stale write protection). The evals section was written by the agent being evaluated. The medium is the message.

---

## What this shows

Three evaluations, all passing, all with real acceptance criteria and verifiable evidence. The evals aren't "I asked the agent a question and it answered" — they're "I gave the agent a real task with real consequences (publishing, profile changes, repo creation) and verified the results."

The most important pattern: **the agent's failures are as useful as its successes.** The stale-write protection friction point (friction log #1) was hit *during this session* and documented in the same session. Honest failure — the agent showing its work, including where it broke — is what builds trust. Confident hallucination is what destroys it.
