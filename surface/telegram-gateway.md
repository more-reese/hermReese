# Telegram gateway

I connected a Telegram bot to Hermes so I can work from my phone. When I'm walking, in the car, or away from my desk, I can still send Hermes a task and it executes with full tool access — not just chat, but real work: file reads, web searches, terminal commands, skill execution.

## How it works

1. **A Telegram bot** (created via @BotFather) receives messages I send from my phone.
2. **Hermes's gateway** routes the message to the agent with full tool access.
3. **The agent executes** — reads files, runs commands, searches the web, uses skills — and responds back through Telegram.
4. **I get the result** as a message on my phone.

The bot token and chat ID are stored as environment variables (`TELEGRAM_BOT_TOKEN`, `TELEGRAM_CHAT_ID`). I also built a [telegram-share skill](../artifacts/skills/telegram-share.md) that lets Hermes send me files and images proactively — not just responding to my messages, but pushing outputs to me when a long-running task finishes.

## What I can do from my phone

- Ask questions and get answers (chat)
- Send a task and get it executed (file operations, web research, code execution)
- Receive files Hermes generates (via the telegram-share skill)
- Receive screenshots and images (rendered to PNG and sent via sendPhoto)
- Continue conversations across sessions (Hermes keeps session context)

## What I can't do (yet)

- **See long outputs comfortably.** Telegram messages have length limits; complex terminal output gets truncated.
- **Review code diffs.** I can ask Hermes to make changes, but reviewing diffs on mobile is impractical — I save that for desktop.
- **Interactive browser sessions.** The browser tool needs a real viewport; mobile Telegram can't host one.
- **Work with files that aren't already on my machine.** Hermes can access my local filesystem, but I can't drag-and-drop from my phone.

## What I'd improve

- **Richer message formatting.** Telegram supports markdown, but Hermes's output is optimized for the desktop app. A mobile-formatted output mode would help.
- **Proactive notifications.** The telegram-share skill can push files, but I'd want more control over when Hermes initiates — e.g., "notify me when the build finishes" as a first-class feature.
- **Session continuity indicators.** On mobile I lose track of which session I'm in. A session label or context indicator in the Telegram chat would help me know what Hermes remembers.

## What this shows

The Telegram gateway is the "multi-platform" requirement made personal. It's not a feature I read about — it's how I actually work when I'm not at my desk. The fact that Hermes's gateway gives me full tool access from a phone, not just chat, is the product insight: the agent's capability doesn't degrade when the surface changes. The conversation is the product; the surface is just where it happens.
