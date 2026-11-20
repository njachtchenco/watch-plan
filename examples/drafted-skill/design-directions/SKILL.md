---
name: design-directions
description: Make 2 to 4 clickable HTML mockups of a screen in different design directions, so you can pick one before anything gets built. Use when asked for "design options", "show me a few directions", "mock this up", "what could this screen look like", or before building a new screen.
---

# Design directions

Turns a screen idea into a few single-file HTML mockups you can open and click, so you give
feedback on something you can see instead of a long written plan.

## Steps

1. Ask what the screen is for, who uses it and what must be on it. Use the AskUserQuestion tool
   with suggested answers. Don't ask for a visual style: that's what the directions are for.
2. Make 2 to 4 directions that differ in layout and feel, not just colour. Each one is a single
   HTML file with its CSS and any script inline and realistic sample content, saved as
   `docs/mockups/<screen>/<direction>.html`.
3. Open them in the browser, or give the paths, with one line on each direction.
4. Ask which one to keep, or what to take from each. Revise the pick if asked.
5. Write the pick and the reasons in `docs/mockups/<screen>/README.md`.

## Don't

- Write app code or touch `src/`. Mockups are throwaway.
- Load scripts or fonts from the internet: each file has to open on its own.
- Build the feature. That's a separate request.

Source: "How we Claude Code", Claude (Anthropic's YouTube channel), talk by Arno,
https://www.youtube.com/watch?v=IlqJqcl8ONE
