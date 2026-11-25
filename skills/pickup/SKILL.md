---
name: pickup
description: Restart work on a project in seconds from the HANDOFF.md written by /handoff. Reads only the handoff and git state, says where things stand, and proposes the next step. Use when the user says /pickup, "where was I", "where did we leave off", "let's continue", "pick this back up", or opens a project after a break.
---

# Pickup

Keep the context small. Read, summarize, propose, wait.

## 1. Read only

- `HANDOFF.md` at the git root (or current folder, or the file the project's CLAUDE.md names). Only its top `## Last session` block if the file is long.
- If a git repo: `git status --short`, `git log --oneline -5`, current branch.

No handoff found → say so, show the last 5 commits and uncommitted files, and ask what to work on. Don't invent a summary.

## 2. Check it still holds

Compare the handoff with git:
- Commits newer than the handoff date → work happened since; mention it.
- Branch differs from the one in the handoff → say so.
- Uncommitted files the handoff doesn't mention → flag them.

## 3. Reply

8 lines max, in the user's language:

**Where things stand**: 2 lines
**Next step**: the one concrete action from the handoff
**Heads-up**: only if something is uncommitted, blocked, or contradicts the handoff

Then ask: "Start on it?" and do the step on yes.

Don't explore the codebase before the yes.
