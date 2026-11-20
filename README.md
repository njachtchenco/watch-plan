# watch-plan

Paste a video link into Claude Code and get back a short plan for **your** setup: which tips you
already have, which don't apply to you, which are worth doing, and where the video is just wrong.
Or turn the video into a new skill.

**Credit:** `/watch` is [claude-video](https://github.com/bradautomates/claude-video) by Bradley
Bonanno (github.com/bradautomates, MIT). It does the watching. watch-plan is built on top of it.

## What it does

- **Plan mode.** Claude watches the video (YouTube, Instagram, TikTok or a file), lists every tip
  in it, and checks each one against your real files: your `CLAUDE.md`, skills, agents, hooks,
  settings and earlier plans. Every tip gets a verdict: **already have**, **doesn't apply**,
  **worth doing** or **wrong**. Claims about how Claude Code works get checked against the docs
  before anything is built on them. You get one plan file, ranked by what saves you the most time,
  and nothing changes until you pick.
- **Skill mode.** If the video teaches something you'll do again, it checks you don't already have
  a skill for it, drafts one, shows it to you, and saves it only where you say.

## Install

You need **Claude Code** (the terminal, VS Code or the desktop app's Code tab). It doesn't work in
the regular Claude chat app.

Run these three lines in Claude Code:

```
/plugin marketplace add njachtchenco/watch-plan
/plugin install watch@nick-jach
/plugin install watch-plan@nick-jach
```

Already have `watch@claude-video`? Skip the second line. The `watch` install comes straight from
Bradley's repo, so you get his updates.

The first time you use it, `/watch` walks you through its setup. It needs Python 3.10+, `ffmpeg`
and `yt-dlp`, and helps you install them.

**Instagram and TikTok:** these videos rarely have captions, so `/watch` needs a way to transcribe
them. Pick one in its setup: local WhisperX (free, about 3 GB, nothing leaves your computer) or a
free Gemini key (Google watches the whole video). YouTube videos usually have captions and need
neither.

## Use it

Plan mode:

```
/watch-plan https://www.youtube.com/watch?v=...
```

or just ask: "watch this and tell me what applies to my setup: <link>"

Skill mode:

```
make a skill from this video: <link>
```

## Example

[`examples/`](examples/) has both modes run on a real talk, [How we Claude Code](https://www.youtube.com/watch?v=IlqJqcl8ONE)
from Anthropic's Claude channel, checked against a small sample project. The plan is
[here](examples/sample-project/docs/HOW-WE-CLAUDE-CODE-PLAN-2026-11.md): three items worth doing,
one setting that looked done but was being ignored, and every other tip with a reason.

## License

MIT. See [LICENSE](LICENSE).
