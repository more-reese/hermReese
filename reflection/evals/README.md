# Evaluations

Does the agent actually complete tasks? Not "does it produce plausible-looking output" — does it *do the thing*. This directory runs real evaluations: tasks with acceptance criteria, measured pass/fail, across models where relevant.

## What this shows

The "design evaluations for agent reliability and real-world task completion" requirement, made operational. I'm not describing how I *would* evaluate agents — I'm running the evaluations and showing the results.

## Evaluation principles

1. **Acceptance criteria are explicit.** "Do a good job" isn't a criterion. "Produce a file that passes `npm run build`, has no secrets, and runs without errors" is.
2. **Failures are kept, not hidden.** A failed eval is more useful than a passed one — it shows where the agent breaks.
3. **Evidence is verifiable.** Every pass claim is backed by a command output or file check. Every fail claim is backed by the same.
4. **Evals are rerun.** A single eval is a snapshot. The interesting question is whether the agent gets better or worse over time.

## Contents

- **[task-completion.md](task-completion.md)** — Real tasks with acceptance criteria and pass/fail results.
- **[model-comparison.md](model-comparison.md)** — Same task across different models. Same input, same criteria, different results.
