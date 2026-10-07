# Metrics

How I'd measure whether Hermes is becoming more useful. Not vanity metrics — the ones that show the agent is earning trust with more of someone's work.

---

## The thesis

Activation (first useful task) is necessary but not sufficient. The metric that matters is **trust growth**: are users giving the agent harder, more consequential tasks as they use it more? A user who's been on Hermes for 50 sessions and is still using it for the same simple tasks as session 1 hasn't been won. A user who's on session 10 and already trusting it with their real work has.

The tenth task is where the product lives or dies. The metrics should reflect that.

## The metrics

### 1. Activation: first useful task

**Definition:** The time from install to the first session where the user completes a task they consider useful — not just "I chatted with it" but "it did something I needed."

**How to measure:** Self-reported (post-session survey: "Did Hermes do what you needed?") or inferred (first session where a tool is successfully invoked and the user continues to a second session).

**What it tells you:** Whether the onboarding gets people to value. If activation is low, the install-to-first-useful-task journey has friction.

**Target:** >60% of new users reach first useful task within the first session. If they don't get value in the first session, the trust ramp never starts.

### 2. Repeat use: the habit forming

**Definition:** Whether the user comes back. Daily/weekly active usage, session frequency, time between sessions.

**How to measure:** Session count per user per week. The trend matters more than the absolute number — is it going up (habit forming) or down (churn risk)?

**What it tells you:** Whether Hermes earned a spot in the user's workflow. One session is a trial; weekly use is a habit.

**Target:** >40% of activated users return within a week. >20% return within 30 days. The drop-off between activation and repeat use is where most products lose people.

### 3. Task escalation: the trust ramp

**Definition:** Whether users are giving Hermes harder, more consequential tasks over time. This is the metric that matters most.

**How to measure:** Proxy metrics:
- **Tool diversity:** Is the user invoking more tools over time? (First session: chat. Tenth session: file reads, web searches, terminal commands, skill execution.)
- **Session length trend:** Are sessions getting longer? (Longer sessions = more complex tasks = more trust.)
- **Skill creation rate:** Is the user building skills? (Building a skill means trusting the agent with a reusable workflow — high trust.)
- **Task type distribution:** Are the tasks getting more complex? (Simple Q&A → file operations → multi-step workflows → building and shipping.)

**What it tells you:** Whether the trust ramp is working. If tool diversity and session length are flat over time, users are plateauing — using Hermes as a chatbot, not a collaborator.

**Target:** Tool diversity increases week-over-week for the first month. Skill creation correlates with retention — users who build skills stay.

### 4. Task completion: does it actually do the thing?

**Definition:** Whether Hermes successfully completes the tasks users give it — not "produces plausible output" but "does the thing."

**How to measure:** Self-reported (post-session: "Did Hermes complete the task?") or inferred (session ends without the user re-asking or correcting). For skills: does the skill's procedure complete successfully?

**What it tells you:** Whether the core loop works. If completion is low, trust can't grow — users won't escalate to harder tasks if the easy ones fail.

**Target:** >85% task completion for sessions where the user reports a clear task. Failure is fine; silent failure is not. (See [friction-log.md](friction-log.md) — honest failure builds trust; confident hallucination destroys it.)

### 5. Trust growth: the composite

**Definition:** A composite metric combining task escalation, skill creation, session length, and retention. The question: is the user's relationship with Hermes deepening?

**How to measure:** A trust score — not a single number, but a profile: "this user started 3 weeks ago, has built 2 skills, uses 5 tools per session on average (up from 1), and has a 90% task completion rate." The trend matters more than the absolute.

**What it tells you:** Whether the product is earning trust with more of someone's work. This is the metric that determines whether Hermes becomes a collaborator or stays a tool.

**Target:** Trust score increases month-over-month. Users who build skills and escalate task complexity are the retained users — the ones who stuck with it.

---

## What I'd prioritize

If I had to pick one metric to build first: **task escalation (the trust ramp).** It's the hardest to measure but the most predictive of retention. Users who escalate to harder tasks stay. Users who plateau leave.

The infrastructure for this metric already exists in Hermes — the `.usage.json` file tracks skill use counts, the session store has session lengths, the tool-use history is logged. The work is surfacing it: a `hermes stats` command that shows the user their own trust ramp. "You've used Hermes for 30 sessions. Your tool diversity has grown from 1 to 7. You've built 3 skills. Your sessions are getting longer. You're trusting Hermes with more."

That's the metric that shows the product working — not to the team, but to the user. And the user seeing their own trust grow is what keeps them coming back.
