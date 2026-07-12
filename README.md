# loadout.md

**A `loadout.md` is a ready-to-run job for an AI agent** — the playbook,
tools, guardrails, examples, and success criteria packaged into one portable
markdown file. Readable by humans, executable by any agent with the right MCP
connected.

> **Workflows do steps. Loadouts do jobs.**

A workflow says *"when X happens, do Y."* A loadout says *"here is how to win
this whole job: what to ask, what to look for, what tools to use, when to stop
for approval, and what good looks like."* MCP gives agents tools — a loadout
tells them how to use those tools to win.

This repository documents the format. It is deliberately small: the entire
spec fits in one file you can read in five minutes, and the
[examples](examples/) are real files that have run real workflows.

- **Spec:** this README (v0.1)
- **Site + validator:** [loadout.md](https://loadout.md)
- **Examples:** [`examples/`](examples/)
- **Reference runtime:** [Apex by LeadShark](https://www.apex.new) — a governed
  LinkedIn MCP; the first loadout.md files were written for it and proven
  against it in production

---

## Why a file?

Everything else about agents is heavy: platforms, canvases, JSON configs,
proprietary workflow builders. A loadout is the opposite bet — the workflow
IS the document:

- **Portable.** The same file runs in Claude, ChatGPT, Cursor, or any MCP
  client. Paste it into a chat; that's the whole runtime.
- **Readable.** A non-technical operator can open it and understand what their
  agent will and won't do. That legibility is where trust comes from.
- **Diffable.** Version it, review it, PR it. Judgment becomes something a
  team can maintain, not prompt folklore in someone's head.

## The format (v0.1)

A valid loadout.md has seven parts, in this order. Three rules are
non-negotiable; everything else bends.

````markdown
# <Name> — Loadout

```yaml
loadout: <slug>            # required — stable id
version: 0.1
tier: <access tier>        # optional — what plan/permission level runs it
mcp: <server url>          # required — the MCP this file drives
cadence: <rhythm>          # optional — e.g. "weekly", "every weekday 09:00"
```

**The job:** one paragraph. The business outcome this file is responsible
for, in the operator's language — not the agent's.

## Before you run — ask the user

Only ask what you don't already know. Check, in order: this file's Config,
the conversation, your memory, and the account/data the MCP exposes. Confirm
inferences in one line instead of re-interviewing.

1. **<Question one?>** (hint)
2. **<Question two?>** (hint)

## Config

```yaml
key_one:            # answers live here; the keys give form fields stable ids
key_two:            # a dashboard can render this block as a form
```

## Steps

### 1. <Step name>
What to do, naming the real MCP tools in backticks: call `tool_name` …

### 2. STOP — approval gate ⛔
Present everything found and drafted. Do not send, publish, schedule, or
create anything until the user approves.

### 3. <Act, verify, close the loop>

## Never

- The hard boundaries. What this loadout must not do, ever, this run.

## Done means

- Verifiable completion criteria — ideally checkable via an MCP read tool.
````

### The three non-negotiables

1. **Ask first.** The file opens with a config interview, and the agent only
   asks what it can't discover. In a chat runtime the agent asks these
   questions; in a dashboard runtime they render as a form. Same questions,
   two front-ends — that's the point of the format.
2. **One approval gate, minimum.** Somewhere before anything irreversible, the
   workflow slams to a stop and a human approves. A loadout without a gate is
   a script, not a loadout.
3. **Done is verifiable.** "Done means" must be checkable — name the read
   tool that proves the work happened (`list_scheduled_posts`, `list_actions`,
   an API you can query). No vibes-based completion.

### Section reference

| Section | Required | Purpose |
|---|---|---|
| `# Name — Loadout` | ✅ | Identity. Keep the `— Loadout` suffix so files self-identify. |
| yaml header | ✅ | Machine-readable: `loadout` (slug) and `mcp` (server URL) are required; `version`, `tier`, `cadence` optional. |
| `**The job:**` | ✅ | One paragraph. The outcome, not the mechanism. |
| `## Before you run — ask the user` | ✅ | The config interview. Numbered, **bold** questions with parenthetical hints. Mark optional ones. |
| `## Config` | recommended | A yaml block of keys the answers fill. Keys become stable form-field ids for dashboard runtimes. |
| `## Steps` | ✅ | Numbered, sequential, readable — Shortcuts-style, not a flowchart. Name real MCP tools in backticks. Include the gate. |
| `## Never` | ✅ | Hard boundaries: no fabrication, no acting without approval, respect suppression lists and rate limits. |
| `## Done means` | ✅ | Verifiable completion + what to report back. |
| `## If it breaks` | optional | Failure handling: what to do on refusals, empty results, errors. Never retry around a refusal. |

## Running a loadout

**In any MCP client** (Claude, ChatGPT, Cursor, …): connect the MCP named in
the file's header, then paste the whole file with:

```
Load this Loadout and run it.

Follow the file exactly:
- ask me the config questions BEFORE doing anything else
- do not perform any irreversible action without my explicit approval
- when done, verify the result the way the file says to.
```

**In a dashboard runtime:** render the file — the Config block becomes a
form, the steps become a checklist, the gate becomes an approval queue. The
file stays the source of truth; the UI is a viewer.

## Provenance

This format wasn't designed on a whiteboard. It's extracted from loadout
files running end-to-end against a production MCP — interviewing for config,
working live data, stopping at the gate, shipping approved work. The
[examples](examples/) are working files, not mockups; the spec documents what
worked, not what sounded good.

## Contributing

- **Examples welcome** — PR a real loadout.md you've run (scrub anything
  private). Real files only; no hypotheticals.
- **Spec changes** — open an issue first. v0.x is deliberately minimal; the
  bar for adding required sections is high.

## License

MIT — the format is meant to spread.
