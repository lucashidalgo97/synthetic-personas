# synthetic-personas

A reusable Claude Code slash command that runs a synthetic LP persona
against **Ask Violet** at [app.iconnections.io](https://app.iconnections.io).

You install it once, run `/test-violet` in any Claude Code session, and
Claude roleplays as one of two LP archetypes — driving a real Chrome
window, clicking through Violet, narrating its reactions in character, and
writing a short report at the end.

Implements persona-agent spec v1.1: two fixed archetypes, evidence baked
into the prompt as implicit calibration, mandatory `[THINKING]` narration.

## Quick install

```bash
git clone https://github.com/lucashidalgo97/synthetic-personas.git
cd violet-personas
mkdir -p ~/.claude/commands ~/.claude/personas-prompts
cp commands/test-violet.md ~/.claude/commands/
cp prompts/*.md ~/.claude/personas-prompts/
```

Then in Claude Code:

```
/test-violet            # Family Office Generalist (default)
/test-violet A          # Institutional Allocator
```

For a step-by-step walkthrough including prerequisites (Claude Code, the
Claude in Chrome extension, an iConnections login), see
[INSTALL.md](INSTALL.md).

## The two archetypes

- **B — Family Office Generalist.** Singapore-based PM, $4B AUM, sole
  decision authority, $5–30M tickets. High openness, low patience. Looking
  for emerging-market PE or US growth-stage VC.
- **A — Institutional Allocator.** Director of Alternatives at a US public
  pension, $42B AUM, IC recommender, $50–250M tickets. Skeptical, expects
  filters and verified track record. Looking for a $150M private credit
  slot.

Both have a baked-in evidence base distilled from the GA/26 LP Pulse
(n=528), the GA/26 executive synthesis, and the team debrief.

## Files

```
.
├── README.md                              # this file
├── INSTALL.md                              # beginner walkthrough
├── commands/test-violet.md                 # the slash command
└── prompts/
    ├── archetype_b_family_office.md
    └── archetype_a_institutional.md
```

## License

MIT — use it, fork it, ship it.
