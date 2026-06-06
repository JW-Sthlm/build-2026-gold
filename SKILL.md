---
name: build-2026-gold
description: Find the Microsoft Build 2026 announcements that actually matter for YOUR partner business, then turn them into customer conversations, a packaged offer, and a LinkedIn post in your voice. Five prompts. About nine minutes. Use when you're a Microsoft partner who wants to cut through Build noise and find what's actually shippable for your customers this quarter.
---

# build-2026-gold · find your gold in the Build 2026 noise

> Portable skill file. Drops into Copilot CLI, Claude Code, Cursor, or any agent that loads skills with YAML front matter.

## What this is

A portable skill that runs the same five-prompt motion as the [public prompts pack](./prompts.md), but wired up properly:

- Loads your partner context once (from `partner-profile.md` in your project root)
- Runs the five prompts in order with the right tools at each step (`fetch` for primary blogs, `reason` for sorting, `write` for the artefacts)
- Writes each output to `./build-2026-gold/` as a file you can hand to your team
- Stays in YOUR voice (English by default, anti-buzzword guard rails baked in)

Works in any agent that loads skill files with YAML front matter. Tested in **Copilot CLI**. The same SKILL.md drops cleanly into **Claude Code**, **Cursor**, custom **MCP hosts**, and any framework that follows the Anthropic / OpenAI / Microsoft skill convention. For tools without skill loaders (ChatGPT chat, Gemini chat, Claude.ai chat), use the [prompts pack](./prompts.md) directly. Same motion, no install.

Total time on a warm cache: about nine minutes. Five prompts.

## When to use this skill

Use when:
- You want to find the Build 2026 announcements that change YOUR Monday, not anyone's Monday
- You're prepping for a partner team meeting, a customer call, or a community session
- You want a packaged offer out the other end, not a recap

Do NOT use when:
- You want a generic Build recap. Read [the prompts pack](./prompts.md) version, run it in any chat, done.
- You don't have a partner profile yet. Write one first · five lines is enough.

## Prerequisites

A `partner-profile.md` somewhere in your project, following this shape:

```markdown
# Partner profile

- Name and niche: ...
- Primary solution areas: ...
- Top 3 customer segments: ...
- Active deals this quarter (3-5, one line each): ...
- Most-asked customer question last 30 days: ...
- Deal I most want to land this quarter: ...
- What my team can deliver in 3 weeks: ...
```

If you have signals in the project (customer call notes, email exports, deal logs), the skill will pick those up too. Optional.

## The five moves

When invoked, the skill executes these in order. Each move waits for explicit "next" before continuing · you can stop, edit context, and resume.

### Move 1 · Pull from the source
Tools: `fetch` against primary Microsoft blogs only (devblogs, github.blog, azure blog, bing blog, techcommunity, Foundry blog). Cross-checks against the partner profile and recent signals.
Output: `build-2026-gold/01-source-list.md` · 10-15 announcements, status-tagged, source-cited, with one-line relevance note per item.

### Move 2 · Sort: cool vs yours
Tool: `reason` over the source list.
Output: `build-2026-gold/02-sorted.md` · two buckets, "Cool moonshots" vs "Mine this quarter", with one sentence per item in Bucket B explaining why it changes the conversation.

### Move 3 · Customer conversations
Tool: `reason` + `write`.
Output: `build-2026-gold/03-conversations.md` · three account-specific conversations: opening line, objection killed, concrete next step.

### Move 4 · Build me an offer
Tool: `plan` + `write`.
Output: `build-2026-gold/04-offer.md` · three-week fixed-price offer for the top item: name, weekly activities, deliverables, take-aways, reusable IP, price band, delivery roles.

### Move 5 · Make me the source
Tool: `write` with humaniser guard rails (no em dashes, no rule of three, no "leverage / unlock / transform", varied sentence rhythm).
Output: `build-2026-gold/05-source.md` · a LinkedIn post (180 words max) and a six-line email to a specific customer.

## How to invoke

```
@build-2026-gold run
```

The skill will:
1. Find or ask for `partner-profile.md`
2. Confirm scope ("ready to run all five? or stop after each?")
3. Execute, writing outputs as it goes
4. Print a summary table at the end with clickable links to each artefact

To run a single move:
```
@build-2026-gold run move 3
```

To re-run a single move with edits:
```
@build-2026-gold revise move 3 · focus on the Nordic Bank deal specifically
```

## Voice and quality rules baked in

Move 5 outputs are pushed through humaniser-style guard rails:
- Zero em dashes (U+2014)
- Banned words: leverage, unlock, transform, empower, journey, landscape, snapshot (as filler), seamless, robust, comprehensive
- Sentence-length variation enforced: must include at least one sentence under 6 words and one over 25
- No "Excited to share", no "I hope this finds you well"
- First-person, conversational, peer-to-peer tone
- No hashtags on LinkedIn output

If a draft fails the check, the skill rewrites and shows you both versions.

## Output folder

All artefacts land in `./build-2026-gold/` inside your project root, gitignored by default. Sub-folder structure:

```
build-2026-gold/
  01-source-list.md
  02-sorted.md
  03-conversations.md
  04-offer.md
  05-source.md
  _context.md         # snapshot of the partner profile used for this run
  _summary.md         # one-page summary with links to all five
```

## Variants

The skill is reusable for any Microsoft (or non-Microsoft) event. Swap the source list at the top of Move 1 and the skill works for Ignite, GitHub Universe, the next Build, partner-of-the-month drops, anything.

To create a variant:
```bash
cp -r ~/.copilot/skills/build-2026-gold ~/.copilot/skills/ignite-2026-gold
# edit the source blogs and the five prompt bodies; the engine stays the same
```

## Credits

Built by [Johan Wallquist](https://www.linkedin.com/in/jwallquist/) for the EMEA Agentic AI partner community. Source repo: [github.com/JW-Sthlm/build-2026-gold](https://github.com/JW-Sthlm/build-2026-gold).
