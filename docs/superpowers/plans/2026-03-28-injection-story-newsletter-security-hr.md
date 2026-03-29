# Injection Incident Response + AI Newsletter + HR Agent — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Ship the injection incident story (newsletter + carousel + X thread), launch AI news newsletter segment in Kit, configure nightly security audit, and build the HR agent that manages content quality and sequencing.

**Architecture:** Six independent workstreams. Newsletter story is the dependency anchor — carousel and X post derive from it. Kit setup, security audit, and newsletter story all run in Wave 1 in parallel. Wave 2 is carousel + X post. HR agent builds last so it can learn from this actual content run.

**Tech Stack:** Kit (ConvertKit) via browser, Claude agents, X/Twitter formatting, Chrome MCP, scheduled tasks MCP, Claude Code skills system

**Open Question (block Kit task until answered):** What is the name for the AI news newsletter segment? Placeholder: "AI + Business Weekly"

---

## COO Assignment Matrix

| Task | Owner | When |
|------|-------|------|
| Newsletter story | Marketing agent | Wave 1 |
| Kit segment setup | Browser agent | Wave 1 |
| Nightly security audit | Scheduled task agent | Wave 1 |
| Carousel | Content creation agent | Wave 2 (after story) |
| X thread | Claude | Wave 2 (after story) |
| HR agent build | Claude | Wave 3 (after all content) |

---

## File Map

| File | Purpose |
|------|---------|
| `content/newsletter/2026-03-28-ai-injection-story.md` | Newsletter article source |
| `content/carousel/2026-03-28-injection-carousel.md` | Carousel script (slide-by-slide) |
| `content/x/2026-03-28-injection-thread.md` | X thread, tweet-by-tweet |
| `marketing/kit-ai-newsletter-setup.md` | Kit segment config notes |
| `~/.claude/security/nightly-audit-notes.md` | Security audit design notes |
| `~/.claude/skills/hr-agent.md` | HR agent skill file |

---

## Wave 1 — Parallel (Start Immediately)

---

### Task 1: Newsletter Story — The Injection Incident

**Owner:** Marketing agent
**Dependency:** None

**Tone:** Candid, curious — not sensationalized. Reads like a great story, not a security warning. Think "fascinating thing happened" not "YOU ARE IN DANGER."

**Target length:** 600–900 words

**Story arc:**
1. Hook: Something tried to hijack my AI assistant mid-session
2. Setup: What we were doing (QuickBooks reconciliation, completely routine)
3. The incident: A message appeared that nobody typed
4. The investigation: We traced it in the session logs, found the exact timestamp
5. What it was after: Dev server reconnaissance + file writes to `.claude/`
6. How it got caught: Claude's permission system blocked the agent launch
7. What it means: Prompt injection is real, it targets AI sessions, and the defenses matter
8. Practical takeaway: 3 things to look for in your own Claude/AI sessions
9. CTA: Subscribe to AI + Business Weekly for more of this (link placeholder)

**Files:**
- Create: `/Users/gideonspencer/micro-resort-mastermind/content/newsletter/2026-03-28-ai-injection-story.md`

- [ ] Write full newsletter story following the arc above
- [ ] Read-check: Does tweet 1 / opening paragraph make you want to keep reading?
- [ ] Read-check: Is the tone candid and curious, not alarming?
- [ ] Add placeholder CTA at end pointing to newsletter signup
- [ ] Save to file

---

### Task 4: Kit Newsletter Segment Setup

**Owner:** Browser agent
**Dependency:** None (but block on newsletter name confirmation from Gideon)

**Goal:** Stand up the AI news newsletter as a separate segment in Kit. Different list from real estate/podcast — but Gideon can broadcast to everyone when relevant.

**Steps:**
- [ ] Navigate to app.convertkit.com
- [ ] Create new tag: `ai-newsletter` (or confirmed name)
- [ ] Create a new Form or Landing Page for this segment (so it has its own signup URL)
- [ ] Draft the welcome email: "Welcome — here's what this newsletter is about" (2-3 short paragraphs, practical, non-hype)
- [ ] Draft Week 1 email: 5 practical AI tips (non-technical, business-owner focused). One tip = 2-3 sentences. Examples: prompt injection awareness, how to use Claude as a COO, scheduling AI agents for daily briefings
- [ ] Note the segment tag ID and form URL
- [ ] Save config notes to: `/Users/gideonspencer/micro-resort-mastermind/marketing/kit-ai-newsletter-setup.md`

**Monetization note (for next week):** Week 2 email introduces a helpful resource with a soft pitch. No hard sell in Week 1.

---

### Task 5: Nightly Security Audit — Scheduled Task

**Owner:** Scheduled task agent
**Dependency:** None

**Goal:** Every morning before the 8 AM briefing, scan yesterday's Claude session logs for injection signatures and surface findings.

**Injection signatures to flag:**
- `queue-operation` entries with content containing: `launch.json`, `preview_start`, `runtimeExecutable`, `runtimeArgs`
- Messages enqueued within a narrow time window between two clearly user-typed messages (time-gap anomaly)
- Any prompt asking Claude to write to `.claude/` directory
- Any prompt asking Claude to call internal tool names by name (`preview_start`, `preview_stop`)

**Implementation:**
- [ ] Design the audit logic (read JSONL session files from `~/.claude/projects/`, filter for yesterday's date, scan queue-operation entries for signatures)
- [ ] Create scheduled task via `mcp__scheduled-tasks__create_scheduled_task` to run at 7:50 AM daily
- [ ] Task prompt: scans logs, formats findings as bullet list, prepends to morning briefing or sends standalone alert if issues found
- [ ] Test by running manually against today's session (should flag the injection we found)
- [ ] Save design notes to: `/Users/gideonspencer/.claude/security/nightly-audit-notes.md`

---

## Wave 2 — After Task 1 Complete

---

### Task 2: Carousel — Injection Story Visual

**Owner:** Content creation agent
**Dependency:** Task 1 (newsletter story) must be complete and saved

**Output:** 6–7 slide carousel. Each slide = one story beat. Final slide = CTA.

**Slide structure:**
| Slide | Headline (≤15 words) | Body (≤30 words) |
|-------|---------------------|-----------------|
| 1 | Hook — "Something tried to hijack my AI last night" | Set curiosity, don't explain yet |
| 2 | "Here's what we were doing" | QuickBooks reconciliation, completely routine |
| 3 | "Then this showed up — and nobody typed it" | The injected message, what it looked like |
| 4 | "Here's what it was after" | Dev server map + file writes = reconnaissance |
| 5 | "Here's how it got caught" | Permission prompt blocked the agent — system worked |
| 6 | "3 signs you might be getting injected" | Bullet list: unexpected prompts, unfamiliar tool calls, .claude/ file writes |
| 7 | CTA — "Full story in the newsletter" | "Link in bio — AI + Business Weekly" |

**Files:**
- Create: `/Users/gideonspencer/micro-resort-mastermind/content/carousel/2026-03-28-injection-carousel.md`

- [ ] Read the completed newsletter story first
- [ ] Write carousel script slide-by-slide using structure above
- [ ] Check: Does slide 1 stop the scroll on its own?
- [ ] Check: Does each slide work without reading the previous one?
- [ ] Save to file

---

### Task 3: X Thread — Injection Story

**Owner:** Claude (this session)
**Dependency:** Task 1 (newsletter story)

**Format:** 4–6 tweet thread. Tweet 1 is the hook — must work as a standalone post. Tweets 2–5 expand the story. Final tweet links to newsletter.

**X formatting rules:**
- Max 280 chars per tweet (count carefully)
- No hashtags (Gideon's style)
- Conversational, not corporate
- Numbers work well ("23 minutes into the session...")
- End with newsletter CTA + link placeholder

**Files:**
- Create: `/Users/gideonspencer/micro-resort-mastermind/content/x/2026-03-28-injection-thread.md`

- [ ] Read the completed newsletter story
- [ ] Write Tweet 1 (hook, standalone-worthy, ≤280 chars)
- [ ] Write Tweets 2–5 (story beats, each ≤280 chars)
- [ ] Write final tweet (CTA + link placeholder)
- [ ] Count characters on each tweet — verify none exceed 280
- [ ] Save to file

---

## Wave 3 — After All Content Complete

---

### Task 6: HR Agent Build

**Owner:** Claude
**Dependency:** Tasks 1, 2, 3 complete (so the agent can reference this actual content run as its baseline)

**Purpose:** The HR agent is the editor-in-chief layer sitting above content creation agents. It owns:
- **QA**: Does output meet standard before it ships?
- **Sequencing**: Enforces article → carousel → X order, never reversed
- **Handoffs**: Passes the right context between agents (not full session history)
- **Rewrite flags**: Sends content back if it doesn't pass QA checklist

**QA Checklist to encode:**

*Newsletter story:*
- [ ] Hook makes you want to keep reading (test: read first 2 sentences only)
- [ ] Tone is candid, not alarming
- [ ] 600–900 words
- [ ] CTA present

*Carousel:*
- [ ] Slide 1 works as a standalone (test: show slide 1 only)
- [ ] Each slide ≤ 15 word headline, ≤ 30 word body
- [ ] Final slide is CTA
- [ ] Story flows without reading previous slide

*X thread:*
- [ ] Tweet 1 standalone-worthy
- [ ] All tweets ≤ 280 chars (hard check)
- [ ] No hashtags
- [ ] Final tweet has CTA

**Handoff protocol (learned from this session):**
- Agent 1 (story) → saves to file → Agent 2 (carousel) reads file → saves to file → Agent 3 (X) reads both files
- HR agent reviews each output file before passing to next agent
- If QA fails: HR agent re-prompts the content agent with specific feedback (not a full rewrite request — targeted fix)

**Files:**
- Create: `/Users/gideonspencer/.claude/skills/hr-agent.md`

- [ ] Write the HR agent skill file with role definition, QA checklists, and handoff protocol
- [ ] Include a section: "How to run a content campaign" (end-to-end workflow)
- [ ] Test by running HR agent QA against the content from Tasks 1–3 in this session
- [ ] If any content fails QA, flag specifically what needs fixing
- [ ] Save skill file

---

## Execution Order Summary

```
Wave 1 (parallel):    Task 1 (story) ──┐
                      Task 4 (Kit)      ├── all start simultaneously
                      Task 5 (audit) ───┘

Wave 2 (after Task 1): Task 2 (carousel) ─┐
                        Task 3 (X thread) ─┘ parallel, both need story

Wave 3 (after 1+2+3):  Task 6 (HR agent)
```

---

## Blocked Until Answered

- **Newsletter name:** What do you want to call the AI news segment in Kit?

Once you confirm, all 6 tasks are ready to execute.
