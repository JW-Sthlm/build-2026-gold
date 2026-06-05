# Five prompts to find your Build 2026 gold

These five prompts mirror the live terminal demo from the EMEA Agentic AI community call. Run them in order. They work in any AI chat: **ChatGPT, Claude, Copilot, Gemini, Mistral, the Copilot CLI** — anywhere. About nine minutes end to end. Some chats with web search will give you more grounded results.

The point is not to learn Build 2026. The point is to find **your** gold inside it.

---

## Before you start — paste this once

The agent is only as useful as the context you give it. Spend two minutes filling this in, then paste it as your **first message**. Every prompt below works against this context.

```
ABOUT ME AND MY PARTNER BUSINESS:

- Partner name and niche: (e.g. "Frontier Consultancy, Nordic specialist
  helping mid-market financial services adopt agentic AI on Microsoft stack")
- Primary solution areas: (e.g. "Modern Work + Data & AI, Copilot rollouts,
  custom agent dev on Foundry + Agent 365")
- Top 3 customer segments: (e.g. "Nordic banks, insurance, public sector")
- Active deals I'm in the middle of: (one line each, 3-5 deals)
- Most-asked customer question last 30 days: (one sentence)
- The deal I most want to land this quarter: (one sentence, name it)
- What my team can actually deliver in 3 weeks: (one sentence)

Use this context to ground every answer. Be brutally honest about
what is and isn't relevant. Don't pad with generic Microsoft talking
points.
```

---

## Prompt 1 — Pull from the source

```
Find the most important Microsoft Build 2026 announcements for MY
partner business based on the context I just gave you.

Rules:
- Primary Microsoft blogs only (devblogs.microsoft.com, github.blog,
  azure.microsoft.com/blog, blogs.bing.com, techcommunity, the Foundry
  blog). No LinkedIn takes, no third-party recaps.
- Cross-check each item against my niche, my deals, and my customers'
  most-asked question.
- Tag each item: GA / Public Preview / Limited Preview / Concept Reveal.
- Cite the source URL.
- Give me 10-15 items. No more.

Output as a numbered list. One line per item: name, what it is in
plain language, status tag, source URL, why it matters for me
specifically.
```

---

## Prompt 2 — Sort: cool vs yours

```
Now sort that list into two buckets. Be brutal.

BUCKET A - "Cool moonshots": amazing tech, headline-worthy,
won't change anything I do this quarter. New hardware concepts,
research breakthroughs, far-horizon product reveals.

BUCKET B - "Mine this quarter": will change a customer conversation,
unblock a deal, or open a new offer in the next 90 days for MY
specific business.

Anything that doesn't clearly belong in B goes in A. Default to
honesty over enthusiasm. If I end up with 8 in B and 4 in A, you
were too generous.

For each item in B, add one sentence: "Why this changes my
conversation."
```

---

## Prompt 3 — Customer conversation

```
Take the top 3 items from Bucket B.

For each one, give me the customer conversation I should be having
next week. Format:

- Account or segment: (use the deals and segments I listed)
- Opening line I can actually say out loud: (one sentence, natural,
  no jargon)
- The objection or blocker this kills: (one sentence)
- The very next step I propose at the end of the call: (a concrete
  artefact, meeting, or commitment - not "let's stay in touch")

Three conversations. Total under 250 words. Ready to send.
```

---

## Prompt 4 — Build me an offer

```
Take the single biggest item from Bucket B - the one that maps to
the deal I most want to land this quarter.

Package it as a three-week, fixed-price partner offer my team can
pitch on Monday morning. Not a discovery call. An actual offer.

Required structure:
- Offer name: (specific, memorable, not "Assessment")
- Outcome the customer gets in 3 weeks: (one sentence)
- Week 1, Week 2, Week 3: real activities, real deliverables
- Take-aways the customer keeps: (3 concrete artefacts)
- Reusable IP my team keeps for next time: (2 things)
- Price band: (rough range, not exact)
- Who on my side delivers it: (roles, not names)

Constraint: every deliverable has to be something my team can
actually produce in the time stated. No "comprehensive frameworks".
```

---

## Prompt 5 — Make me the source

```
Now make me the source, not the forwarder. Two artefacts.

1. A LinkedIn post (180 words max) in MY voice:
   - First-person, conversational
   - One specific customer question I'm hearing this month
   - Connect it to one Build 2026 announcement from Bucket B
   - End with how my team is packaging it (reference the offer
     from Prompt 4)
   - No corporate buzzwords ("unlock", "leverage", "transform",
     "empower", "journey", "landscape")
   - No em dashes
   - No hashtags
   - No "Excited to share..."
   - One short sentence somewhere. Vary the rhythm.

2. A six-line email to ONE specific customer from my deal list
   who asked the question I'm posting about:
   - Subject line (under 6 words)
   - Open with what they actually said on the last call
   - Connect to the announcement
   - Propose a concrete 15-30 min slot this week
   - No "I hope this finds you well"
   - Signed in my voice

Output both. Ready to copy-paste.
```

---

## After Prompt 5

You now have:

- A grounded shortlist of what at Build 2026 is actually yours
- Three customer conversations ready for next week
- One packaged offer your team can quote on
- A LinkedIn post and a customer email in your voice

Run this every time a Microsoft event drops. Same five prompts. New context.

---

## Want the full automated version?

The five prompts above run great in any chat. If you want to wire them into the **Copilot CLI** as a one-command skill that loads your partner context automatically, see [`SKILL.md`](./SKILL.md) in this repo.

If you want the partner positioning, training, and reusable assets that go around this kind of motion, that's [Frontier Consultancy](https://jw-sthlm.github.io/frontier-consultancy-public/partners/).

If you want to join the EMEA Agentic AI partner community where we share this kind of work every two weeks, the sign-up is on the landing page.
