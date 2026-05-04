# Install & run `/test-violet` — beginner's guide

This guide walks you through installing the `/test-violet` slash command on
your computer and running your first persona session. No coding experience
required. Total time: about 15 minutes.

---

## What you'll end up with

A new command, `/test-violet`, that you type into Claude Code. When you run
it, Claude pretends to be a real Limited Partner (an investor who allocates
capital to funds), opens `app.iconnections.io` in your Chrome browser, clicks
through Ask Violet, and writes a short report on how Violet performed.

You'll see two artifacts in your Claude Code chat:

1. The persona's stream of thought (`[THINKING]` blocks) and the screenshots
   it took.
2. A short `Session report` at the end summarizing what worked and what
   didn't.

---

## Step 1 — Make sure you have the prerequisites

You need three things. If you already have them, skip to Step 2.

### 1a. Claude Code

Claude Code is Anthropic's command-line tool. If you don't have it:

- Go to <https://claude.com/claude-code> and follow the install instructions
  for your operating system (Mac, Windows, or Linux).
- After install, open a terminal and run `claude` to confirm it works. You
  should see a chat prompt.

### 1b. Google Chrome

Just regular Chrome. Download from <https://www.google.com/chrome/> if you
don't have it.

### 1c. The "Claude in Chrome" extension

This is what lets Claude Code drive your browser.

1. Open Chrome.
2. Go to the Chrome Web Store and search for **"Claude in Chrome"** (or use
   the link Anthropic publishes at <https://claude.com/chrome>).
3. Click **Add to Chrome**.
4. After installing, click the puzzle-piece icon in Chrome's toolbar, find
   "Claude in Chrome," and pin it.
5. Click the extension icon and follow the prompts to **connect it to your
   Claude account**. You'll know it's connected when the extension shows a
   green dot or a "connected" status.

### 1d. An iConnections account

You need to be able to log into <https://app.iconnections.io> with access to
**Ask Violet**. If you don't have an account, contact your iConnections
admin.

---

## Step 2 — Clone the repo and install the slash command

You're going to clone this repository from GitHub, then copy three of its
files into Claude Code's config folder. That config folder lives in your
home directory and is called `.claude` (it starts with a dot).

You need `git` installed. It comes pre-installed on Mac and most Linux
systems. On Windows, get it from <https://git-scm.com/download/win>.

Open a terminal and run:

```bash
git clone https://github.com/lucashidalgo97/synthetic-personas.git
cd synthetic-personas
mkdir -p ~/.claude/commands ~/.claude/personas-prompts
cp commands/test-violet.md ~/.claude/commands/
cp prompts/*.md ~/.claude/personas-prompts/
```

That's it.

### What did those commands do?

- `git clone …` — downloads the kit (this README, the slash command, and
  the two persona prompts) into a folder called `synthetic-personas` in
  whatever directory you ran the command from.
- `cd synthetic-personas` — moves into that folder.
- `mkdir -p ~/.claude/commands ~/.claude/personas-prompts` — creates two
  folders inside your `.claude` config folder if they don't already exist.
- `cp commands/test-violet.md ~/.claude/commands/` — copies the slash
  command file into the place Claude Code looks for slash commands.
- `cp prompts/*.md ~/.claude/personas-prompts/` — copies the two persona
  prompts into a place the slash command knows how to find.

You can verify it worked:

```bash
ls ~/.claude/commands/test-violet.md
ls ~/.claude/personas-prompts/
```

The first should print the path. The second should list two `.md` files.

---

## Step 3 — Log into iConnections in Chrome

The persona drives **your** Chrome browser, so it uses **your** iConnections
session. Open Chrome, go to <https://app.iconnections.io>, and log in. Leave
the tab open.

You only have to do this once per Chrome session — Chrome remembers your
login.

---

## Step 4 — Run your first session

1. Open a terminal.
2. Run `claude` (this starts Claude Code).
3. Once you see the Claude Code prompt, type:

   ```
   /test-violet
   ```

4. Hit Enter.

You'll see Claude:

- Read the persona prompt.
- Open (or focus) Chrome on `app.iconnections.io`.
- Take a screenshot.
- Start narrating in `[THINKING]` blocks like:

  > [THINKING]
  > I see the dashboard. The "Ask Violet AI" bar is at the top with a ⌘K
  > shortcut. I'm here for emerging-market PE — let me click it and start.
  > [/THINKING]

- Click into Ask Violet, type a query, and read the response.
- After a few rounds, the persona will end the session and write a
  **Session report** with what worked and what didn't.

If Claude asks you to log in (because it sees a login page instead of the
dashboard), switch to your Chrome window, log in, then come back to the
terminal and tell Claude to continue.

---

## Step 5 — Try the other archetypes and custom frames

Three archetypes are built in:

**LP side** — these test whether Violet can help allocators find good
funds:

- **B** — Family Office Generalist (default). Singapore-based PM, $4B AUM,
  high openness, low patience.
- **A** — Institutional Allocator. Director of Alternatives at a US public
  pension, $42B AUM, skeptical, expects filters.

**GP side** — this tests whether Violet can help fund managers find LPs:

- **C** — Emerging GP, Fund I. Co-founder of a $10M AI-infrastructure
  venture fund, mid-raise, no pedigree, hungry. Wants named LPs.

Run them:

```
/test-violet            # archetype B
/test-violet B          # same — explicit
/test-violet A          # archetype A
/test-violet C          # archetype C
```

You can also override the situational frame to focus the test:

```
/test-violet B You only have 5 minutes and want to test whether Violet handles a vague mandate gracefully.

/test-violet A You need a $200M private credit allocation and want to see if Violet can produce a defensible shortlist.

/test-violet C You're three weeks from your first close and your anchor LP is wobbling. You need warm-able LPs, not categories.
```

Everything after the archetype letter is treated as the situational frame.

---

## What "good" looks like

A successful run produces:

- 5–15 `[THINKING]` blocks showing the persona reacting to what it sees.
- A handful of screenshots interleaved with clicks and text typed into
  Violet.
- A `Session report` section at the end that names actual funds, calls out
  specific UI strengths/weaknesses, and answers "would the persona come
  back?"

A run with **only** a Session report and no `[THINKING]` blocks means the
persona broke character — try again, and if it keeps happening, let the
maintainer know.

---

## Troubleshooting

### "Command not found: /test-violet"

The file isn't where Claude Code expects. Check:

```bash
ls ~/.claude/commands/test-violet.md
```

If that prints "No such file," redo Step 2.

### "I see a login page instead of the dashboard"

Switch to Chrome, log into <https://app.iconnections.io> manually, then in
the Claude Code chat say "I'm logged in, continue."

### "Claude says it can't drive the browser"

The Claude in Chrome extension isn't connected. Click the puzzle-piece icon
in Chrome, click Claude in Chrome, and check the connection status. Restart
Chrome if needed.

### "The persona keeps asking *me* questions instead of acting"

Tell it: "Stay in character and drive the browser yourself — make
reasonable assumptions." If it persists, end the session and start a new
one.

### "I want to see the transcript later"

Claude Code keeps your session history. From the terminal:

```bash
ls ~/.claude/projects/
```

Each project folder contains JSONL files with the full chat history,
including all `[THINKING]` blocks and screenshots.

---

## Updating

To pull a newer version, run from inside your `synthetic-personas` clone:

```bash
git pull
cp commands/test-violet.md ~/.claude/commands/
cp prompts/*.md ~/.claude/personas-prompts/
```

The `cp` commands will overwrite the old files.

To remove it entirely:

```bash
rm ~/.claude/commands/test-violet.md
rm -r ~/.claude/personas-prompts
```

---

## What's actually happening under the hood

(Optional reading — skip if you don't care.)

When you type `/test-violet`, Claude Code:

1. Reads `~/.claude/commands/test-violet.md` and treats its contents as
   instructions for *itself*.
2. Those instructions tell Claude to read one of the persona prompt files
   and adopt the persona's voice and behavior.
3. The persona prompt instructs Claude to use the `mcp__Claude_in_Chrome__*`
   tools to control your real Chrome window.
4. Claude clicks through Violet in character, narrating in `[THINKING]`
   blocks — that narration is real Claude output you see in your terminal.
5. When the persona ends the session, Claude drops character and writes the
   report.

There's no separate Python script, no API server, no background process —
the entire loop is "Claude reads its own instructions and uses the tools it
already has."
