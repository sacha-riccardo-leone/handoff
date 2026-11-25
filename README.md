# handoff

**Two Claude Code skills so you never lose your place between sessions.**

- `/handoff` at the end of a session writes a short, factual block to `HANDOFF.md`: where things stand, the single next step, what's blocked, and the gotchas that cost you time.
- `/pickup` at the start of the next session reads that block and your git state, tells you where you are in 8 lines, checks the handoff still matches git, and proposes the next step.

No database and no setup: one Markdown file in your repo.

## Install

```
/plugin marketplace add sacha-riccardo-leone/handoff
/plugin install handoff@handoff
```

Or copy `skills/handoff/` and `skills/pickup/` into `~/.claude/skills/`.

## Use

```
/handoff     # before /clear, closing the laptop, or switching projects
/pickup      # when you come back
```

They also trigger on *"let's stop here"*, *"save progress"*, *"where was I?"*, and *"let's continue"*.

## What a handoff looks like

```markdown
## Last session: 2026-11-25 18:40
**Branch:** feat/billing · **Uncommitted:** 2 files

**Where things stand**
- Stripe checkout works end to end in test mode
- Webhook handler stores events, but doesn't update subscriptions yet

**Next step**
1. In `api/webhooks/stripe.ts`, handle `customer.subscription.updated`. Done when the test in `webhooks.test.ts` passes
2. Then show the plan on the settings page

**Blocked / to decide**
- Proration on downgrade: immediate or at period end?

**Gotchas**
- `stripe listen` must run in a second terminal or webhooks silently never arrive
```

## Details

- It writes in whatever language you're speaking.
- It keeps the last block in full, shortens the two before it to a single line, and deletes older ones, so the file never grows.
- The first time, it asks whether `HANDOFF.md` should be committed (team notes) or gitignored (personal notes).
- `/pickup` doesn't explore your codebase until you say go, which keeps the context small.

## License

MIT
