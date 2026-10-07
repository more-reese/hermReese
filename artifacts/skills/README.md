# Skills

Custom skills I've built for Hermes Agent. A skill is a reusable chunk of competence — a workflow, a set of conventions, a way of working that the agent loads when it's relevant. These are where agent capabilities become product experiences: each skill takes a raw capability (API access, text processing, pattern recognition) and shapes it into something that does a useful thing in a way that fits how I work.

## What this shows

Each skill is a case study in product design for agents:

- **What problem does it solve?** (Not what it does — what it's *for*.)
- **How does the agent know when to use it?** (The trigger, the routing logic.)
- **What's the user experience?** (What do I type, what do I get back?)
- **Where does it break?** (Skills fail. The interesting question is how.)

## Skills

### [pattern-language](skills/pattern-language.md)

A shared operating language for pro-forms — meaning resolved by context, with productive morphology. Built through months of iterative sessions with Hermes. The most complex skill I've built: it encodes a way of thinking about form, not just a workflow. Four axes, five conformations tested across domains (business, research, creative, software, cybernetics). Currently at v0.3.1 with open questions about formal proofs and algorithm/heuristic distinctions.

### [job-application-strategy](skills/job-application-strategy.md)

Structured guidance for preparing a job application or interview. Built during this very application — the skill I used to produce the resume, cover letter, and this repo. Manages an application as a product launch: a single master experience reference feeds every downstream deliverable. Includes GitHub profile optimization, portfolio repo scaffolding, and interview prep.

### [telegram-share](skills/telegram-share.md)

Send files and messages via Telegram Bot API using curl. Powers my mobile workflow — lets Hermes push outputs to me when a long-running task finishes, not just respond to my messages. Also handles rendering HTML to PNG via headless Chrome before sending as an image.

## How these are maintained

Skills evolve. They get patched when I learn something new, reused across sessions, and sometimes deprecated. The git history on each skill shows the iteration — the skill's version history is the product design history. The `pattern-language` skill alone has been through 8+ patches and 20+ uses; the `job-application-strategy` skill was created and patched 8 times during this application process.
