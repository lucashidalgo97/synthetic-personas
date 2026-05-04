# synthetic-personas

A reusable Claude Code slash command that runs a synthetic LP or GP persona
against **Ask Violet** at [app.iconnections.io](https://app.iconnections.io).

You install it once, run `/test-violet` in any Claude Code session, and
Claude roleplays as one of three archetypes — driving a real Chrome window,
clicking through Violet, narrating its reactions in character, and writing
a short report at the end.

Implements persona-agent spec v1.1: fixed archetypes, evidence baked into
the prompt as implicit calibration, mandatory `[THINKING]` narration.

## Quick install

```bash
git clone https://github.com/lucashidalgo97/synthetic-personas.git
cd synthetic-personas
mkdir -p ~/.claude/commands ~/.claude/personas-prompts
cp commands/test-violet.md ~/.claude/commands/
cp prompts/*.md ~/.claude/personas-prompts/
```

Then in Claude Code:

```
/test-violet            # Family Office Generalist (default, LP-side)
/test-violet A          # Institutional Allocator (LP-side)
/test-violet C          # Emerging GP, Fund I (GP-side)
```

For a step-by-step walkthrough including prerequisites (Claude Code, the
Claude in Chrome extension, an iConnections login), see
[INSTALL.md](INSTALL.md).

## The three archetypes

**LP side — testing Violet's GP/fund discovery:**

- **B — Family Office Generalist.** Singapore-based PM, $4B AUM, sole
  decision authority, $5–30M tickets. High openness, low patience. Looking
  for emerging-market PE or US growth-stage VC.
- **A — Institutional Allocator.** Director of Alternatives at a US public
  pension, $42B AUM, IC recommender, $50–250M tickets. Skeptical, expects
  filters and verified track record. Looking for a $150M private credit
  slot.

**GP side — testing Violet's LP discovery:**

- **C — Emerging GP, Fund I.** Co-founder of an AI-infrastructure venture
  fund, $10M target, mid-raise at $4.2M soft-circled, no pedigree. Hungry,
  pitchy, sends templated outreach at scale, has been throttled once. New
  to the platform. Wants Violet to surface named LPs that fit a sub-$25M
  Fund I — family offices, HNW, emerging-manager-friendly fund-of-funds.

All three have a baked-in evidence base distilled from internal research:
B and A from the GA/26 LP Pulse (n=528), executive synthesis, and team
debrief; C from the Q1 2026 GP Onboarding Pulse, emerging-manager
benchmarks, and platform engagement telemetry.

## Files

```
.
├── README.md                              # this file
├── INSTALL.md                             # beginner walkthrough
├── commands/test-violet.md                # the slash command
└── prompts/
    ├── archetype_b_family_office.md       # LP — family office PM
    ├── archetype_a_institutional.md       # LP — pension director
    └── archetype_c_emerging_gp.md         # GP — Fund I AI-infra
```

## License

MIT — use it, fork it, ship it.
