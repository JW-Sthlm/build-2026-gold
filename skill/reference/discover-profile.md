# Step 0 · Discover profile · the recipe

The skill needs a partner profile to ground every move. This file is the exact recipe the agent runs to find or build one. The skill does not bundle any MCPs · it asks the host for whatever tools are available and picks the richest path.

## The decision tree

```
1. Is there a partner-profile.md in the project AND modified in last 14 days?
   YES → use it. Skip to Move 1.
   NO  → continue.

2. Does the host expose a WorkIQ / Microsoft Graph tool? (workiq.*, graph.*, teams.*, mail.*)
   YES → run the WorkIQ recipe below.
   NO  → continue.

3. Does the host expose a web-fetch tool? (fetch, browse, http, curl)
   AND has the user mentioned a company website or domain?
   YES → run the web recipe below.
   NO  → continue.

4. Run the interactive recipe.
```

After every path, the agent writes `build-2026-gold/_profile.md` with a one-line note on the source, then shows it to the user with: *"Here's what I derived. Confirm, edit, or replace before I run the five moves."*

## Tier 1 · file (always wins when present)

```
read partner-profile.md
if last-modified > 14 days ago, ask: "this is older than 2 weeks. refresh from WorkIQ / web, or use as-is?"
write build-2026-gold/_profile.md with header "Source: partner-profile.md (manual)"
```

## Tier 2 · WorkIQ / Microsoft Graph (the freshest signal)

The agent runs these prompts against whichever Graph-flavoured tools the host exposes. Tool names vary by MCP · the skill checks for any of `workiq.*`, `graph.*`, `teams.SearchMessages`, `mail.SearchMessages`, `calendar.ListEvents`.

```
1. NICHE + SOLUTION AREAS
   Search Teams chats + emails last 90 days.
   Query: "customer pitch" OR "we help" OR "our practice" OR "our offer" OR "we specialise"
   Reason over results → 1-line niche + top 3 solution areas.

2. TOP CUSTOMER SEGMENTS
   Search calendar last 60 days for external meetings (subject contains "with" or invitee on different domain).
   Group by inviting org. Top 3 by meeting count = top segments.

3. ACTIVE DEALS
   Search Teams + mail last 30 days.
   Query: "proposal" OR "SOW" OR "next steps" OR "decision" OR "pricing" OR "Q&A"
   Group by external counterparty. Pick 3-5 with most thread volume = active deals.

4. MOST-ASKED CUSTOMER QUESTION
   Search Teams + mail last 30 days for messages from external domains containing "?".
   Cluster by topic (reason). Pick the cluster with most independent customers.

5. DEAL I MOST WANT TO LAND
   Ask the user. One question, not derivable from signal.

6. WHAT MY TEAM CAN DELIVER IN 3 WEEKS
   Ask the user. One question.
```

Write `build-2026-gold/_profile.md` with header *"Source: WorkIQ · last 90 days · derived [date]"*. Always end with: *"Confirm, edit, or replace before I run the five moves."*

## Tier 3 · web (good for cold partners)

The agent fetches the company's public surfaces and derives the profile from marketing copy. Needs the partner's domain (asks the user once: "what's your company URL?").

```
1. fetch <domain>/                                  → niche, tagline, top solution areas
2. fetch <domain>/about OR /company                 → positioning, size hint
3. fetch <domain>/customers OR /case-studies        → named customer segments
4. fetch <domain>/insights OR /news OR /blog        → recent talking points (last 90 days)
5. fetch <domain>/services OR /solutions            → what they actually deliver
6. reason: synthesise into profile shape.

For the 3 fields not derivable from public marketing:
- "active deals this quarter": skip, mark as "<set manually>"
- "most-asked customer question": infer from recent blog/insights themes, prefix with "(inferred from public content)"
- "deal I most want to land": ask the user. One question.
```

Write `build-2026-gold/_profile.md` with header *"Source: web · <domain> · derived [date]"* and flag the inferred / manual fields explicitly so the user knows what to verify.

## Tier 4 · interactive (always works)

Ask the six questions one at a time. Short questions, no preamble. Write `build-2026-gold/_profile.md` with header *"Source: interactive · [date]"*.

```
1. "What's your niche in one line? (e.g. 'data platform partner for Nordic financial services')"
2. "Your top 3 solution areas?"
3. "Top 3 customer segments?"
4. "3-5 active deals this quarter, one line each?"
5. "What customer question have you heard most in the last 30 days?"
6. "Which deal do you most want to land this quarter, and what could your team deliver in 3 weeks?"
```

## Confirmation gate

Every path ends the same way. The agent shows the derived profile and asks:

> Here's what I derived. Three options:
> 1. Looks good · run the five moves.
> 2. Let me edit it first · I'll open it and you continue when ready.
> 3. Replace · you write your own and I'll use that.

No move 1 fires until the user picks one. The profile is the foundation · five minutes of confirmation here saves an hour of "the agent missed my niche" later.

## What the skill is NOT doing

- It is not installing MCPs. Host's job.
- It is not authenticating to Graph. Host's job · skill assumes the tools are already authorised.
- It is not deciding which Graph scope to use. Host's job · skill uses whatever the host exposes.
- It is not caching the profile across runs. Each run starts from Step 0 with the 14-day freshness check on the file.

This keeps the skill portable. Copilot CLI, Claude Code, Cursor, custom MCP hosts · same SKILL.md, different available tools, the discovery tree adapts.
