# telegram-share

**Skill name:** `telegram-share`
**Version:** 1.0.0
**Author:** Hermes Agent (built during a  session)
**Category:** Productivity
**Related skills:** architecture-diagram

## What it's for

Sending files, images, and text to a Telegram chat via the Bot API, using only curl. No SDK, no extra dependencies. Powers my mobile workflow — lets Hermes push outputs to me when a long-running task finishes.

## What problem it solves

When I'm away from my desk, I still want to receive outputs from Hermes — a generated diagram, a research summary, a file Hermes produced. The Telegram gateway lets me send messages *to* Hermes from my phone, but I also need Hermes to send things *back* to me proactively. This skill handles the "push" direction: Hermes sends me files and images through Telegram when they're ready.

## How the agent uses it

The skill loads when Hermes needs to send me something via Telegram. It provides:
- Bot token and chat ID setup (stored as environment variables)
- `sendPhoto` — for images (diagrams, screenshots, rendered HTML)
- `sendDocument` — for any file type
- `sendMessage` — for text
- HTML-to-PNG rendering via headless Chrome (for architecture diagrams and other HTML artifacts)

## What the experience is like

I'm walking. I send Hermes a task from my phone: "Render the system architecture diagram and send it to me." Hermes generates the HTML, renders it to PNG via headless Chrome, sends it via `sendPhoto` with a caption, and I get the image in Telegram. The whole pipeline — generate, render, send — happens without me being at my desk.

## Where it breaks

- **Chat ID has to be right.** If the chat ID is wrong or I haven't started a conversation with the bot, `sendPhoto` fails with "chat not found."
- **File size limits.** Telegram has limits on file size; large outputs need to be split or sent as documents.
- **Image rendering quirks.** Headless Chrome's `--window-size` needs to match the SVG viewBox dimensions to avoid clipping. The `CVDisplayLinkCreateWithCGDisplay` warnings on macOS are harmless but look alarming.

## What this shows

This skill is small but illustrates the product principle: the agent's capability shouldn't degrade when the surface changes. The same agent that runs in my terminal, reads my files, and uses my skills can push outputs to my phone through a different surface — because the conversation is the product, and Telegram is just where it happens.
