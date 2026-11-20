# Plan from "How we Claude Code": Nov 2026

> **Example output.** This plan is what `/watch-plan` produces. The video is real; the project it
> was checked against (`examples/sample-project/`, "Recipe Box") is a small made-up one, built for
> this example.

A 2026-11-20 session watched one talk and compared every piece of advice in it with **this**
project's Claude Code setup (`CLAUDE.md`, `.claude/settings.json`, the `new-feature` and
`release-notes` skills, `package.json`), not with the talk's generic advice. Every claim about
the setup below was checked in the files. The claims about how Claude Code behaves were checked
against Claude Code's docs. Nothing has been changed: this is a plan, and you pick which items to
do.

## Sources

| Video | Creator | Length | How watched | Verdict |
|---|---|---|---|---|
| [How we Claude Code](https://www.youtube.com/watch?v=IlqJqcl8ONE) | Claude (Anthropic's channel); talk by Arno, Applied AI team | 31:43 | English captions, full transcript, no frames (a live demo; the code on screen is in the talk's workshop repo) | Three ideas are worth doing here. Its main one, verification built into a big app, is more than a one-person app needs yet |

## Status board

Read this first.

| # | Item | Risk | Status |
|---|---|---|---|
| 1 | Click-through HTML mockups before building a UI feature | low (one skill step) | PROPOSED |
| 2 | Auto mode is set where Claude Code ignores it | low | NEEDS YOU: whether you want auto mode at all |
| 3 | Ask questions with the AskUserQuestion tool | low (one line) | PROPOSED |

## 1. Click-through HTML mockups before building a UI feature

**From the talk** (10:25, 11:04): plans as Markdown get long and unread; an HTML page is denser and
you can click it. Ask Claude for a few design directions as HTML files and compare them before
building.

**Here:** `new-feature` step 2 writes a Markdown plan, and almost every feature in Recipe Box is a
screen. A plan says what a screen will hold; a mockup shows it, which is where "that's not what I
pictured" gets caught before the code is written.

**Change:** in `.claude/skills/new-feature/SKILL.md`, after step 2, add: "If the feature has a
screen, also make 2 to 4 single-file HTML mockups in different directions in
`docs/plans/<feature>/`, open them, and ask me to pick one before step 3." Keep the Markdown plan
for data and edge cases.

**Don't:** build mockups for bug fixes or non-UI changes, or let mockup code end up in `src/`.

**Proof it worked:** on the next UI feature, the mockups exist, open in a browser, and the build
matches the one picked.

## 2. Auto mode is set where Claude Code ignores it

**From the talk** (08:08): "You need to be using auto mode."

**Here:** `.claude/settings.json` already sets `"defaultMode": "auto"`, so this looks like
"already have". It isn't: Claude Code's docs say auto mode doesn't take effect from project or
local settings, only from your user settings (`~/.claude/settings.json`) or the
`--permission-mode` flag. The line is silently ignored, and sessions here start in the default
mode.

**Change, your call:** if you want auto mode, set `"permissions": {"defaultMode": "auto"}` in
`~/.claude/settings.json` (it then applies to every project on this machine) and remove the line
here. If you don't, just remove the line, so it stops looking like it does something.

**Proof it worked:** start a new session here; the mode shown under the prompt is the one you
chose.

## 3. Ask questions with the AskUserQuestion tool

**From the talk** (04:42, 07:01, 09:20): Claude is better at drawing out what you want than you
are at writing it down, so let it interview you. Name the areas you care about (the audience, for
one), not the answer, and tell it to use the AskUserQuestion tool, which shows the questions as
options you tap through.

**Here:** `new-feature` step 1 already interviews ("what the feature is for and who will use it"),
so the idea is **already here**. It asks in plain chat, one question at a time.

**Change:** step 1 becomes: "Use the AskUserQuestion tool to ask what the feature is for, who uses
it and what done looks like, with suggested answers. Ask follow-ups the same way."

**Proof it worked:** the next `new-feature` run opens with tappable questions instead of a chat
message.

## What the talk got wrong, or is already solved here

- **"Use Opus 4.7"** (30:44) is out of date: newer Opus models have shipped since the talk (May
  2026). The point under it holds: for screenshot-heavy front-end work, use the strongest model you
  have. Don't pin a version number in a skill.
- **Effort "X high, or max"** (08:08): `effortLevel` in settings takes `low`, `medium`, `high` or
  `xhigh`; `max` only works per session through `/effort` (or an environment variable). See
  "Considered and rejected" for why neither is set here.
- **"Naming the tool is what triggers this workflow"** (09:20) overstates it: Claude can use
  AskUserQuestion without being told. Naming it makes it reliable, which is why item 3 names it.
- **Screenshots for front-end problems** (11:43): nothing to set up. Paste or drag one into the
  prompt when a screen looks off.

## Considered and rejected

- **Verification built into the app** (13:23 to 27:43: components publish their state to the DOM,
  with schemas, fixtures, invariants and probes, run by an agent through the Playwright MCP and
  headless in CI). Built for a team shipping UI changes daily. For a one-person app with unit tests
  it's more to maintain than it saves. Revisit when the app has more screens than you can click
  through by hand; then start small: the Playwright MCP and one "open it and try it, including one
  wrong input" step in `new-feature`.
- **Record each verification run as a video and share it** (14:10, 27:43): there's no one to share
  it with.
- **Fast mode for iterating on specs** (08:08, 30:44): faster, and the talk itself says it costs
  more. Not worth it as a default on a side project; turn it on with `/fast` when you're waiting.
- **Set effort to xhigh by default** (08:08): costs more on every request, including the small
  ones. Raise it with `/effort` for a hard task instead.
- **"HTML specs save tokens in the long run"** (30:44): plausible, not checkable from a talk. Item 1
  stands on catching "not what I pictured" early, not on this.
