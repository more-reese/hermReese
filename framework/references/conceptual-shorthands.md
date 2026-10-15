# Conceptual Shorthands

Aphorisms describe general truths. Metaphors aid understanding. Heuristics aid deciding. Conceptual aids are constructions for understanding — label them as such, never as documented components.

## Aphorisms

1. **Model fixes aptitude, effort fixes amplitude.** The model determines what the brain can do (reasoning depth, tool-calling quality, vision, code). Effort is the intensity dial — how hard it tries on this specific turn. Aptitude bounds the ceiling; amplitude is where you set the dial within it. A high-aptitude model at low amplitude gets a quick answer that *could* go deeper. A low-aptitude model at high amplitude is trying hard but hitting its ceiling.
2. **One-shot is transactional, multi-shot is interactional.** A one-shot query is a single exchange with no continuation. An interactive session is a multi-turn conversation where context persists. Pick based on whether you need a single answer or a developing dialogue.
3. **The tool call is the bridge from thought to action.** A chatbot reasons and responds. An agent reasons, acts (calls a tool), observes the result, and reasons again. The tool call is what makes it an agent.
4. **Build with, runs in.** A framework constrains what you build. A runtime conditions what runs. Hermes is a runtime — you don't build with it, you configure it and it runs.
5. **Frame sets the shape, time sets the state.** The framework determines what kinds of things can happen. The runtime determines what's happening right now. An agent can adjust the runtime (model, effort, skills) but not the framework (tools, session model, config routing) from inside it.
6. **Think, call, run, repeat.** The conversation loop: model reasons, emits a tool call, Hermes executes it, result feeds back. Each loop is informed by the last — the model decides as it goes, not upfront.

## Metaphors

1. **The consultant and the firm.** Provider is the firm (who hosts and serves the brain). Model is the consultant they send you (the actual brain, with its own aptitudes). Effort is how long you ask them to think before answering. The firm's reputation doesn't do the work — the consultant does. But you can't get the consultant without going through the firm.
2. **The desk and the drawer.** Context window is desk space — how much you can spread out in front of you at once. Memory is the filing cabinet — it persists after you leave the desk. A session is sitting down at the desk: you get your files (memory) and your desk space (context), but when you stand up, the desk clears. The filing cabinet stays.
3. **The surface and the engine.** The CLI, TUI, desktop app, and Telegram are steering wheels. The agent core is the engine. You can drive from any wheel — same engine, same trips, same fuel tank. Switching wheels doesn't change where you're going; it changes how the steering feels in your hands.
4. **The profile is the house.** Config is the thermostat (settings for the whole house). Memory is the bookshelf (what you know, visible in every room). Skills are the toolbench in the garage (loaded when you're doing that kind of work). Sessions are conversations at the kitchen table — when you clear the table, the conversation is gone, but the house remembers who lives there.
5. **Just in case, just in time.** Progressive disclosure has two layers: just in case (the skills index — name + description, always loaded, cheap) and just in time (the full skill body, loaded on match or request, expensive). The just-in-case layer is the catalog you scan; the just-in-time layer is the chapter you open.

*Add new metaphors as they emerge from the learning process. Keep them concise — one image each.*

## Conceptual Aids (not from the docs — constructions for understanding)

1. **Surface vs. interface.** A surface is what the user experiences (Telegram app, terminal, desktop window). An interface is the contract at the boundary (what crosses from one side to the other, in what format, with what rules). A surface implements an interface. Every surface implements the same interface to the agent core: text in, response out. The interface is the protocol; the surface is the presentation.
2. **Facade vs. template method.** `run_agent.py` is the facade — `AIAgent` class with 14 mixins, one public method (`run_conversation`). `conversation_loop.py` is the template method — a fixed 7-step outline (build prompt → resolve provider → call model → dispatch tools → compress → persist → return) with variable steps (which provider, which tools, which skills). The facade is the class (what callers see); the template method is the function (how the loop works). Both serve "one engine, all surfaces."

*Conceptual aids are constructions, not documented components. Label them as such when teaching. Never present a conceptual aid as a documented architectural layer.*

## Heuristics

1. **Match amplitude to task complexity, not to your anxiety.** Reading a doc and explaining a concept = medium effort. Quick factual lookup = low effort. Multi-step debugging or architecture analysis = high effort. Don't burn high effort on simple tasks — it's slower and costs more for no benefit.
2. **Session context is not memory.** If it matters in a session where you're doing something completely different, it belongs in memory. If it only matters in this conversation, it stays in the session. When in doubt: would a brand-new session need to know this? If yes → memory. If no → session.
3. **Config changes next session; slash commands now.** `hermes config set` writes to the profile — takes effect in the next session. `/model` or `/reasoning` overrides for the current session only. Use config for durable defaults, slash commands for one-time adjustments.

*Add new aphorisms and heuristics as they emerge from the learning process. Keep them concise — one sentence each.*
