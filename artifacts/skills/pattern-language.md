# pattern-language

**Skill name:** `pattern-language`
**Version:** 0.3.1
**Author:** Agent-assisted
**Category:** Research
**Uses:** 8+ sessions

## What it's for

Formology — a shared operating language built on form as the atomic unit. A way of thinking about how meaning resolves across contexts, with a productive morphology (suffix encodes grammatical function, prefix encodes resolution state). Not a tool that does one thing — a way of seeing that applies across domains.

## What problem it solves

I needed a language for talking about patterns that recur across completely different domains — business processes, software architecture, creative writing, cybernetics — without flattening the differences. Formology gives me the vocabulary: form (the invariant), conformation (form resolved by context), proformation (form before resolution), deformation (form releasing context). Same form, different conformations, domain determines the resolution.

## How the agent uses it

The skill loads when I'm developing, refining, or applying the pattern language. It contains:
- The core principles (form as atomic unit, productive morphology, the cycle pro→con→de)
- The four axes (suffix, prefix, focus, context)
- The 2x2 spatio-temporal matrix as a conformation of the prefix
- Five tested conformations across domains (business, research, creative, software, cybernetic morphology)
- Open questions and version history

The agent reads this and participates in the thinking — proposing conformations, testing them against the criteria, flagging where the language breaks.

## What the experience is like

I describe a domain I'm working in. The agent proposes how the form resolves there — what the invariant is, what the morphology looks like, how the prefix axis maps. We test it against the three-condition membership rule (structural slot, substitution, anaphoric interpretation). If it passes, it's a conformation. If it fails, we learn where the language doesn't reach yet.

It's not a lookup — it's a conversation. The skill gives the agent the vocabulary; the session produces the insight.

## Where it breaks

- **Over-fitting to VSM.** The 2x2 matrix is a conformation, not the form — but it's the most developed one, so it's easy to mistake it for the structure itself.
- **Premature formalization.** The language is heuristic, not algorithmic — it orients within an open space of possibilities; it doesn't compute a final answer.
- **Domain coverage.** Five conformations tested; vsm-translator, published articles, and the Composite Wordplay Score remain untested.

## What I'm working on next

- Drafting a standalone C0-style formal proof for Formology (axioms + membership rule + domain topology + test suite)
- Testing remaining artifacts (vsm-translator, published articles) against the foundational proof
- Deciding whether the algorithm/heuristic distinction is a separate axis or a reading of the prefix

## The deeper point

This skill is the clearest example of what I mean by "agent as cognitive prosthetic." The language evolved through sessions with Hermes — not because Hermes invented it, but because the conversation was the surface where the thinking became making. The skill encodes what we figured out together. It's not a tool I built; it's a way of seeing we developed.
