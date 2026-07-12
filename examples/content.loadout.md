# Content — Loadout

```yaml
loadout: content
version: 0.1
tier: pro-plus            # content + scheduling + automation = Pro+ baseline
mcp: https://apex.leadshark.io/mcp
cadence: weekly           # suggested loop: Mon or Tue morning; run-now works too
```

**The job:** turn what's working in your market plus your own voice into one
lead-magnet post a week — drafted, CTA'd, wired to a comment-to-DM automation,
and scheduled. You approve everything before it ships.

## Before you run — ask the user

**Only ask what you don't already know.** Before asking anything, check — in
this order:

1. This file's **Config** section below — filled fields are answers; never re-ask them.
2. **The conversation so far** — the user may have already told you.
3. **Your own memory/project context** — prior runs, saved preferences.
4. **The account itself** — `list_recent_posts` reveals audience, language, and
   past CTAs; a prior lead-magnet post often names the asset and keyword.

Whatever is still unknown after that, ask — and confirm what you inferred in
one line ("I'm assuming X from your recent posts — correct?") instead of
re-interviewing. Aim for zero to five questions, not always five.

1. **Who is the post for?** (audience/ICP in one line)
2. **Personal profile, company page, or both?** (`list_companies` shows the pages)
3. **What's the lead magnet?** (the asset/offer + its URL — a guide, template,
   playbook, quiz, page)
4. **What should readers do?** (the CTA — usually "comment WORD and I'll DM it")
5. **Anything off-limits?** (topics to avoid, competitors not to echo)

## Config

> Filled in by the user or the dashboard. The agent reads this; the drawer edits it.

```yaml
audience:            # e.g. "B2B founders doing LinkedIn outbound"
surface:             # personal | company | both
lead_magnet:         # name + URL
cta_keyword:         # e.g. "PLAYBOOK"
avoid:               # topics/competitors to skip
tone_notes:          # optional: anything the drafts keep getting wrong
post_time:           # local time + IANA timezone, e.g. "09:00 Europe/Tallinn"
```

## Steps

### 1. Collect signal — what's working right now
Call `discover_lead_magnets` for the user's niche. Pull the top 5–10
lead-magnet posts by engagement. You're studying **structure and hooks**
(what made people comment), never text to copy.

### 2. Learn the user's voice
Call `list_recent_posts` (the connected account's own posts — NOT
`list_person_posts`, which is for other people) for the last ~20 posts.
**Sanity check:** if what the account actually posts contradicts the Config,
flag it and adapt to the account's reality.

### 3. Draft the post
Write ONE post: the user's voice, a hook pattern that's currently working,
the lead magnet as the payoff, ending in the comment-keyword CTA.
Offer 2 alternate hooks below the draft so approval is a choice, not a veto.

### 4. Prepare the automation
Call `suggest_automation_settings` for the comment-to-DM flow. Draft the DM
copy — short, human, no pitch beyond delivering the asset.

### 5. STOP — approval gate ⛔
Present the packet: signals found → voice notes → the draft (+ alt hooks) →
DM copy → automation settings → proposed post time.
**Do not schedule, publish, or create the automation until the user approves.**

### 6. Schedule it
On approval, call `schedule_post_with_automation` (post + keyword + DM in one
call). Confirm back: what's scheduled, when, and where to watch it.

### 7. Close the loop (next run)
Before step 1 next time: check how last week's post did (`list_post_engagers`).
Note what worked in one line. Feed that into this week's draft.

## Never

- Publish, schedule, or create automations without explicit approval this run.
- Copy another creator's post, structure-swap included.
- Invent engagement numbers, client results, or testimonials.
- DM anyone who didn't comment the keyword.
- Run more than once per cadence window without being asked.

## Done means

- User approved a draft (target: ≤2 edit rounds).
- Post scheduled with automation attached — verify with `list_scheduled_posts`.
- User told where to monitor it.
- One-line learning noted for next run.
