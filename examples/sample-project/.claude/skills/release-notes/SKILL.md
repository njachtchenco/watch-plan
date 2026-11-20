---
name: release-notes
description: Write release notes from the commits since the last tag. Use when asked for "release notes", "what changed" or "changelog".
---

# Release notes

1. Find the last tag with `git describe --tags --abbrev=0`.
2. Read `git log <tag>..HEAD --oneline`.
3. Group the changes into New, Fixed and Changed, in plain words a user would follow.
4. Show the notes in chat. Don't edit any file.
