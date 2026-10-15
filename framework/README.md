# Framework — Use Hermes to Learn Hermes

This directory contains the reusable learning framework. It's a Hermes skill (`SKILL.md`) that anyone can install into their own Hermes instance to learn Hermes from first principles.

## What's here

```
framework/
├── SKILL.md                          ← The installable skill (install this)
├── references/
│   ├── curriculum.md                 ← Default Hermes curriculum (Modules 1–15)
│   ├── assessment-protocol.md        ← Dual assessment: knowledge + skills
│   ├── conceptual-shorthands.md      ← Aphorisms, metaphors, heuristics
│   └── module-15-sub-modules.md      ← Bonus module: reading code
└── templates/
    ├── progress.md                   ← Template for personal progress tracking
    └── reflections.md                ← Template for per-tier reflections
```

## How to use it

1. **Clone this repo** and copy `framework/SKILL.md` and `framework/references/` into your `~/.hermes/skills/productivity/hermes-learning-path/` directory
2. **Start a Hermes session** and say "let's start the learning path"
3. The skill loads, the curriculum begins, and Hermes guides you through each module

The skill carries:
- The 14-module curriculum (3 tiers: Beginner, Intermediate, Advanced)
- The assessment protocol (dual knowledge + skills checks)
- Conceptual shorthands (aphorisms, metaphors, heuristics that develop as you learn)
- The bonus Module 15 (reading and explaining code)

## The principle

**Work with Hermes to show you how it works, not to tell you.**

The learning path is self-referential by design: the agent that runs the curriculum is the same agent the curriculum teaches you about. You learn what a tool is by watching the tool use itself. You learn what a skill is by using a skill that teaches you about skills. You learn what memory is by having the agent remember your progress across sessions.

## Customizing

The curriculum is a reference file (`references/curriculum.md`) — you can edit it to add, remove, or modify modules without touching the skill itself. The skill loads the curriculum on demand (Level 2 progressive disclosure), so changes to the reference file take effect on the next skill load.
