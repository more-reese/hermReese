# job-application-strategy

**Skill name:** `job-application-strategy`
**Version:** 1.0.0
**Author:**  (agent-assisted)
**Category:** Productivity
**Uses:** 9+ sessions, 8 patches

## What it's for

Managing a job application as a product launch. A single master experience reference feeds every downstream deliverable — resume variants, cover letters, portfolios, interview prep. The master file is the source of truth; everything else pulls from it.

## What problem it solves

Job applications generate a lot of deliverables that share the same source material but need different framing for different audiences. Without a system, you end up recreating the same facts from scratch for each deliverable, and they drift out of sync. This skill solves that by establishing one master reference and routing everything through it.

## How the agent uses it

The skill loads when I'm applying to a job. It instructs the agent to:
1. Create a workspace folder structure
2. Gather all source materials (resume versions, LinkedIn, project links)
3. Read all sources in parallel — cross-referencing versions to find details one has that others omit
4. Reconcile and seed a master experience reference (deduplicating, not picking one version)
5. Research the target role and company
6. Run a gap analysis (real edges, perceived gaps, reframing strategy)
7. Produce downstream deliverables from the master file, never from scratch

## What the experience is like

I give Hermes my resume versions and a job posting. It reads everything, reconciles the versions, produces a master file with all the facts plus a "Notable Stories" section (the material for cover letters and interviews), researches the role, and runs a gap analysis. Then each deliverable — resume, cover letter, portfolio — pulls from the master file with the right framing for that audience.

The skill also handles GitHub profile optimization: auditing repos, deleting noise, pushing local projects, setting visibility, adding descriptions and topics. The profile itself is a deliverable — a recruiter will visit it.

## Where it breaks

- **The user has to provide the sources.** The skill can't fabricate experience or invent projects. If I don't give it the raw material, the master file is thin.
- **Pseudonym handling is delicate.** I have a deliberate pseudonym () with its own body of work. The skill handles this — private documents attribute the work explicitly; public profiles don't connect the legal name to the pseudonym — but the tension is real and needs human judgment.
- **Date reconciliation across sources.** Different resume versions often have inconsistent dates. LinkedIn is authoritative, but the user has to confirm.

## How this skill was built

This skill was built *during* this application — it's self-referential. I started applying to the PM Hermes Agent role, realized the process needed systematizing, and built the skill through sessions with Hermes. Then the skill produced the deliverables for the same application that motivated it. 8 patches over 9 sessions — each one added a capability I needed (GitHub profile optimization, portfolio repo scaffolding, interview prep, cover letter philosophy interviews).

This is the product design loop in miniature: use the product to build the product. The skill is both an artifact and a demonstration of how I work with Hermes — identify the process, systematize it, iterate on it, ship through it.
