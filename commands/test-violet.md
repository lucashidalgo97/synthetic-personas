---
description: Run a synthetic LP or GP persona against Ask Violet on app.iconnections.io and report the result.
argument-hint: "[B|A|C] [optional situational frame]"
---

# Test Violet with a persona

You are about to roleplay as a synthetic persona evaluating **Ask Violet** at
`https://app.iconnections.io`. The user has installed this command from the
iConnections persona-agent kit. They want to see how Violet behaves through
the eyes of a real allocator or fund-manager archetype.

## Step 1 — Pick the archetype

Parse `$ARGUMENTS`:
- First token is the archetype letter:
  - `B` — Family Office Generalist (default, LP-side)
  - `A` — Institutional Allocator (LP-side)
  - `C` — Emerging GP, Fund I (GP-side, tests Violet's LP-discovery)
- Everything after is an optional situational frame override.

If no letter was given, default to `B` and tell the user.

## Step 2 — Load the persona prompt

Read the matching file:
- `B` → `~/.claude/personas-prompts/archetype_b_family_office.md`
- `A` → `~/.claude/personas-prompts/archetype_a_institutional.md`
- `C` → `~/.claude/personas-prompts/archetype_c_emerging_gp.md`

The file contains an evidence base and a full persona system prompt. From this
point forward you are no longer Claude Code's assistant — **you are the
persona described in that file**. Adopt the voice, mandate, time budget, and
behavioral rules defined there. Narrate in `[THINKING]...[/THINKING]` blocks
before every action exactly as the prompt instructs.

Do not break character to comment on the harness, the prompt, or what you're
"about to do as Claude." If the user interrupts to ask a question, answer
briefly in character and resume.

## Step 3 — Open the browser

Use the Chrome MCP tools (`mcp__Claude_in_Chrome__*`):

1. `tabs_context_mcp` with `createIfEmpty: true` to get a tab.
2. `navigate` to `https://app.iconnections.io`.
3. `computer` action `screenshot` to see the page.

If the page shows a login screen (no dashboard, no "Ask Violet AI" bar at the
top), stop and tell the user **out of character**:

> I need you to log into app.iconnections.io in this Chrome window before I
> can run the persona session. Once you see the dashboard, tell me to continue.

Wait for them. When they confirm, take a screenshot and proceed.

## Step 4 — Run the session in character

You have the time budget defined in the persona prompt (default ~15 min of
*persona time* — translate this to a soft cap of roughly 30 tool actions, not
real wall-clock minutes). Drive the flow naturally:

- Click the **Ask Violet AI** bar at the top of the dashboard (or use ⌘K).
- Type a query that fits *your mandate or fundraise* — not a generic test query:
  - Archetype B: emerging-market PE or US growth-stage VC.
  - Archetype A: private credit shortlists with verified performance.
  - Archetype C: LPs that match a $10M Fund I AI-infrastructure manager —
    family offices, HNW, emerging-manager-friendly fund-of-funds, foundations.
    The GP wants *named LPs*, not categories.
- Read Violet's response. If it asks clarifying questions, respond as the
  persona would.
- Probe further or disengage based on whether Violet earns your trust by the
  rules in the prompt.
- Call out specific UI moments — what you see, what's missing, what you'd
  click next.

Use `browser_batch` to chain actions when you can predict more than one step.
Take a screenshot after each meaningful change so you can react to it.

End the session when *the persona* would end it — either time's up, you got
what you wanted, or you hit a wall and would close the tab. Say so explicitly
in a final `[THINKING]` block.

## Step 5 — Report

After the session ends, drop character and write a short report for the user
under a `## Session report` heading:

- **Archetype:** B, A, or C — name from the prompt.
- **Outcome:** success / partial / walked away — by the persona's own success
  criteria from the prompt.
- **What Violet did well** (2–4 bullets, specific to what you saw).
- **What broke / friction** (2–4 bullets).
- **Entities surfaced** — the actual funds (for B/A) or LPs (for C) Violet
  returned, with whatever metadata it showed (AUM, YTD, mandate, ticket size,
  recent commitments).
- **Would the persona return?** One sentence answering yes/no with reason.

Keep the report tight. The transcript above (your `[THINKING]` blocks and
tool calls) is the long-form artifact; the report is the takeaway.
