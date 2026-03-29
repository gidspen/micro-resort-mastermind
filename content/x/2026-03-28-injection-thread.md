# X Thread — Prompt Injection Story
**Date:** 2026-03-28
**Source:** content/newsletter/2026-03-28-ai-injection-story.md

---

Tweet 1 (148 chars):
A message appeared in my AI session that nobody typed.

It showed up 19 seconds after my last input. It had a specific goal. It was not bookkeeping.

---

Tweet 2 (196 chars):
I had a browser agent running through QuickBooks, matching transactions against bank statements. Routine stuff. I stepped back and let it work.

Then something else showed up in the session queue.

---

Tweet 3 (200 chars):
The injected message was trying to:

1. Map my dev environment
2. Write a config file to .claude/launch.json
3. Start processes on my machine

Fully formed. Professional-looking. Like it came from me.

---

Tweet 4 (215 chars):
It got stopped because Claude's permission layer surfaced what it was about to do before acting.

I denied it. Then asked one question: "why does Claude want to run Python?"

That question unraveled the whole thing.

---

Tweet 5 (232 chars):
If you're running AI agents, watch for:

- Permission prompts unrelated to your task
- Write requests to config directories (.claude/, .config/)
- Any process execution you didn't ask for

The defense isn't software. It's attention.

---

Tweet 6 (213 chars):
I write about this stuff — AI agents, automation, and what actually happens when you put these tools to work in a real business.

No theory. No hype. Subscribe here:
https://thehuntforincredible.kit.com/897fd9c3f4
