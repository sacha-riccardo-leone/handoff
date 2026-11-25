---
name: handoff
description: End-of-session save so the next session restarts instantly. Writes a short, factual "where I am / next step" block to HANDOFF.md in the project, for /pickup to read. Use when the user says /handoff, "save progress", "let's stop here", "end of session", "wrap up for today", or before /clear or closing a long session on a project.
---

# Handoff

Write ONE short block to ONE file. Facts only: what is true now, not what you hope. Write in the language the user speaks in this conversation.

## 1. Gather

- If the project is a git repo: `git status --short`, `git log --oneline -5`, current branch.
- From this conversation: what changed, what was decided and why, what failed, what is half done.
- Do not explore the codebase to fill gaps. If you don't know, leave it out.

## 2. Write

Where: an existing `HANDOFF.md` at the git root (else the current folder). If none exists, create it there. If the project's CLAUDE.md names another handoff file, use that.

Put this block at the **top** of the file. Replace the previous `## Last session` block; keep everything else in the file. Keep 2 older blocks at most under `## Earlier`, shortened to their "Next step" line; delete older ones.

```
## Last session: <YYYY-MM-DD HH:MM>
**Branch:** <branch> · **Uncommitted:** <n files, or "none">

**Where things stand**
- 3 to 5 bullets: what works now, what was done this session

**Next step**
1. The single next action: which file, what to do, how to know it's done
2. Then…
3. Then…

**Blocked / to decide**
- Open questions for the user, or "nothing"

**Gotchas**
- Commands, quirks or dead ends that cost time this session (so they don't cost time again)
```

30 lines max. A next step must be concrete enough that someone with zero context could start it.

If `HANDOFF.md` is new, ask once whether to add it to `.gitignore` (personal notes) or commit it (team notes). Don't ask again in later sessions.

## 3. Reply

3 lines max: the next step, any uncommitted work worth committing now, and "Next session: /pickup".
