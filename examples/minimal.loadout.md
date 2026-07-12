# Morning Brief — Loadout

```yaml
loadout: morning-brief
version: 0.1
mcp: https://apex.leadshark.io/mcp
cadence: every weekday morning
```

**The job:** a two-minute read of what happened on your LinkedIn overnight —
who engaged, who invited, who messaged — ranked by who's worth your attention
today. Read-only: this loadout never writes anything.

## Before you run — ask the user

1. **What does a lead worth your attention look like?** (titles, company types)
2. **How many people should the brief surface?** (default: top 5)

## Config

```yaml
icp:                 # e.g. "founders and GTM leads at B2B SaaS"
brief_size:          # default 5
```

## Steps

### 1. Pull the overnight signals
Call `list_signals` — new commenters, reactors, profile visitors, inbound
invitations, and messages since the last run.

### 2. Rank by fit
Call `enrich` on the new names. Rank against the configured ICP. Drop noise.

### 3. Deliver the brief
Write the brief: who engaged, why they might matter, and one suggested next
move per person. **Suggest only — this loadout takes no actions.**

## Never

- Send, connect, reply, or write anything to LinkedIn — this is a read-only loadout.
- Invent engagement that didn't happen.
- Rank someone highly just because they're famous; fit beats follower count.

## Done means

- The brief is delivered: N people, each with a one-line why and a suggested move.
- Everything in it is traceable to a real signal from `list_signals`.
