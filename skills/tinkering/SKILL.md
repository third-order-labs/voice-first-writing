---
name: tinkering
description: >-
  Capture a short log entry of what was just built, explored, or discovered in
  this session and append it to the tinkering log that feeds the content
  flywheel. Fire this AUTONOMOUSLY when a substantive chunk of work just
  wrapped — a feature shipped, a bug root-caused, an experiment concluded, an
  architecture decided, a gnarly gotcha solved — or when the user signals
  they're wrapping up or stepping away ("that's done", "good stopping point",
  "okay I'm out", "let's wrap"). Do NOT fire on trivial edits, mid-task
  checkpoints, or read-only/Q&A turns. Also invokable manually as /tinkering,
  optionally with an argument to emphasize what's notable.
---

# /tinkering — Capture What Just Happened

Quick, low-friction capture of what was built, explored, or discovered in the current session. Writes to a tinkering log that feeds the content flywheel.

This is the connective tissue of the whole system: the flywheel can only write about what got captured. Work that never lands in the log evaporates — two weeks later it's "I built some stuff" instead of a concrete story with texture. The log is raw material, not content; entries are observations, not drafts.

## When to fire autonomously

This skill is autonomous-eager: you may invoke it without being asked when a real unit of work just finished. Good triggers:

- A feature or arc shipped end-to-end.
- A bug got root-caused or a tricky gotcha got solved (especially "do not re-hit this" territory).
- An experiment, spike, or architecture decision concluded.
- The user signals a session boundary: "that's done", "good stopping point", "okay I'm out", "let's wrap", "calling it."

Do NOT fire on: trivial one-line edits, mid-task checkpoints where work is still in flight, pure Q&A or read-only turns, or sessions where nothing substantive changed. When in doubt and the session is still moving, hold off. One entry per meaningful unit of work, not one per tool call.

## How it works

**Default (no arguments):** You have the session context. Distill what just happened into a short tinkering entry. No questions needed. Write 2-3 sentences, max a short paragraph, capturing what was done and anything notable. Then append it to the log.

**With arguments** (e.g., `/tinkering the cache invalidation approach is the interesting part here`): Use the provided context to guide the entry. The user is telling you what they think is notable or wants to emphasize something specific. Combine their input with your session context to write the entry.

## When to ask questions

Only ask clarifying questions if:
- You genuinely don't have enough context (e.g., conversation was heavily compacted and you lost the details)
- The session covered multiple distinct things and you're not sure which one the user wants captured
- The user's argument is ambiguous

Do NOT default to an interview. The whole point is speed. If you have the context, just write.

## The log

The log path resolves in this order:

1. `tinkering_log` in a `config.json` in the current working directory (the writing workspace sets this)
2. Default: `~/.claude/tinkering.md`

The default is deliberately global, not per-project: tinkering happens wherever you build — any repo, any directory — and the flywheel reads one log from the writing workspace. A per-project log would fragment the signal. Create the file if it doesn't exist.

**Entry format:**
```
## YYYY-MM-DD HH:MM
**Project**: [project name or directory name, inferred from current working directory]
**What**: [2-3 sentences max. What was built, explored, discovered, or tinkered with. Be specific enough that someone reading this in 2 weeks has useful context.]
**Notable**: [Optional. One sentence. Something that surprised you, broke interestingly, or connects to a bigger idea. Skip this field entirely if nothing stands out.]
**Said**: [Optional. 1-2 lines the user actually typed this session, verbatim, in quotes. See "The Said field" below. Skip if nothing qualifies.]

```

Leave a blank line after each entry for readability.

## The Said field

The other fields record what happened. This one records what the user *thought* about it, in their own words, because that's the part the flywheel can't reconstruct later. A draft built on a verbatim line from the user reads like them; a draft built on a project summary reads like a summary.

Pick lines from the user's own messages in this session (never your own output) where they react, wonder, complain, get excited, or think out loud about the work: "Ummmm, soooo, huh, not sure. I feel I want to do more with this but not sure what...." qualifies. Instructions ("run the tests", "fix the import") don't.

- Verbatim. Keep typos, lowercase, "lol", swears, trailing dots. Don't clean it up; the roughness is the point.
- One or two lines, not a transcript. If nothing qualifies, omit the field. Most entries won't have one.
- Never include client names, credentials, or anything from a project the user has marked off-limits for content. When unsure, leave it out.

## Rules

- Keep it short. This is a log entry, not a session summary.
- Be specific. "Worked on the pipeline" is useless. "Rewrote the ETL dedupe to hash on (source_id, updated_at) — cut the nightly run from 40 minutes to 6" is useful.
- Use the project name from the current working directory, not a guess.
- Timestamps should use the current local time.
- Don't editorialize. Capture what happened, not what it means for content strategy. The flywheel does that mapping later.
- If the session was genuinely uneventful (debugging, yak-shaving, nothing interesting), say so briefly. Not every entry needs to be interesting. "Spent 2 hours on a flaky CI test. Timezone-dependent date assertion. Nothing notable." is a valid entry.
