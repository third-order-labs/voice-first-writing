---
description: Capture a short spicy take — minimal polish, maximum speed, optional push to your publishing target
argument-hint: "[text] [hold|schedule <when>] [--platform <platform>]"
---

# /take — Capture a Hot Take

**Config**: This command reads directory paths and publishing settings from `config.json`. Falls back to defaults if config is missing.

Short spicy one-off. Minimal polish, maximum speed. The drive-by take evaporates unless there's a zero-friction way to catch it. This is that way.

## Before starting

Do NOT read the full voice guide — this command is deliberately lightweight. The voice rules below are the short list. If publishing is configured (`publishing.target` in `config.json`), read the credentials from `.env`.

## Arguments

- No argument — pull the most recent take-shaped riff from the current conversation
- `"quoted text"` — use that text as the starting point
- `hold` — save to the takes folder but do NOT publish
- `schedule <when>` — schedule for a specific time instead of posting now (requires a publishing target)
- `--platform <platform>` — target platform; default is the first short-form platform in the user's platform strategy, or ask

## Flow

### 1. Capture

Either pull from conversation (the most recent take-shaped riff — a one-liner, hot take, or short observation) or use the provided text. If ambiguous about which riff to capture, ask. One clarifying question max, then go.

### 2. Shape (minimal polish only)

**Start by reading "What makes a take spicy" below.** Apply those principles during shaping. The most common failure mode is sanding the rawness out of the original riff while polishing.

- Strip em-dashes. Replace with period, comma, or colon based on context.
- Kill AI anti-patterns: "It's not X, it's Y" reframes, "Here's what nobody's saying", "Let's talk about", over-qualified hedging.
- Fit to platform per the platform's format guide (short-form limits, whether a 2-3 post thread is acceptable when it doesn't compress to one).
- Keep profanity if it was in the riff at an inflection point. Cut it if it was decoration.
- Do NOT add throat-clearing, setup, or framing the original riff didn't have. Raw-first.

### 3. Save

Save to `writings/takes/YYYY-MM-DD_short-slug.md` (takes directory from `config.json`). Create the folder if it doesn't exist.

Format:

```
---
platform: <platform, or multiple>
status: posted | scheduled | held
source: <brief note on origin — e.g. "conversation 2026-04-17">
---

<take content, or per-platform versions clearly labeled>
```

Takes track status in frontmatter, not by folder moves — they never enter the `drafts/ -> ready/ -> published/` pipeline.

### 4. Ship

**If no publishing target is configured:** save with `status: held` and tell the user where it is. That's a complete run, not a failure — the takes folder is the queue.

**Default (publishing configured, no hold/schedule arg):** show the user the final text and ask: "Ship it?" They can say yes, edit, or hold. On yes, publish immediately.

**If `hold`:** save with `status: held`. Don't touch the publishing API.

**If `schedule <when>`:** parse the time (ISO 8601, the user's timezone unless specified), save with `status: scheduled`, publish with the scheduled timestamp.

### 5. Publishing (Typefully target)

When `publishing.target` is `"typefully"`, POST to the Typefully v2 API with credentials from `.env` (`TYPEFULLY_API_KEY`, `TYPEFULLY_SOCIAL_SET_ID`):

```
POST https://api.typefully.com/v2/social-sets/{TYPEFULLY_SOCIAL_SET_ID}/drafts
Authorization: Bearer {TYPEFULLY_API_KEY}
Content-Type: application/json

{
  "platforms": { "<platform-key>": { "enabled": true, "posts": [{"text": "TAKE"}] } },
  "publish_at": "now"
}
```

- `publish_at` accepts `"now"` (publish immediately), `"next-free-slot"` (auto-queue), or ISO 8601 with timezone. Omit it to save as a plain draft. Do NOT use `publish: true` or `schedule_date` — both are rejected by the v2 API.
- Platform keys: `x` for Twitter/X, `linkedin` for LinkedIn. Threads are multiple `{"text": ...}` objects. Cross-posting is both platform objects in one call, each with its own version.
- Plain text only — strip markdown.

### 6. Confirm

Show: status (posted/scheduled/held), platform(s), draft ID if applicable, file path saved.

## What makes a take spicy

The diagnostic failure mode: a raw riff goes in, and a structured mini-essay comes out (setup → history → conclusion) with none of the spiciness that made it worth capturing. This section exists so that doesn't happen.

### Spicy principles

- **One move, not three.** Setup + argument + landing is a blog post compressed. Drive-by takes do one thing. Assert, observe, provoke, or show — pick one, don't stack them.
- **Specificity with edge.** Name the tool, not the category. Cite the moment, not the activity (the specific query, the exact error, the one meeting). Abstraction kills spice.
- **Keep the half-thought energy.** If the original riff trailed off, let it trail. "starting to think..." / "genuinely wondering..." / "IDK..." are not weakness, they're the texture that makes it sound like a person thinking in real time.
- **Raw register from the source.** The user's original phrasing is almost always spicier than a polished version of it. If they said "I hope that AI coding means the end of ORMs..." don't rewrite to "AI coding should be the end of ORMs." Keep the "I hope" and the trailing dots.
- **Provoke, don't argue.** A question ("what is the ORM for") or a flat assertion ("shit works fine without them") lands harder than a three-beat case. Takes don't need to convince anyone.
- **Profanity at the inflection, not the frame** (if it's in the user's voice at all). "shit works fine" is structural — the swear marks the load-bearing moment. "hot fucking take" is performance — the swear is in the setup where it reads as try-hard. The subtle drop at the punch is the move.
- **No neat conclusions.** A take that wraps up cleanly reads polished. Leave it jagged. The reader is allowed to draw the conclusion.

### Diagnostic questions before shipping

Ask each one. If the answer is yes to any, it's probably flat:
- Does it have three sentences doing three different jobs (setup, argument, landing)?
- Is the punch an abstraction instead of a specific name or moment?
- Did the polish remove half-thought markers that were in the original riff?
- Does the last sentence sound like a summary / TED-talk takeaway?

If any of those, revise. Remove one of the three moves. Swap abstract for specific. Put the trailing dots back. Cut the summary.

### Examples (for calibration)

**Flat** (what to avoid):
> Hot take: AI coding should be the end of ORMs. They existed so you didn't have to write SQL. Now you don't have to write it, but you also don't have to hide from it.

Three moves, polished parallel structure, neat conclusion. Reads like a LinkedIn line.

**Spicier versions** (each doing one move):
> just watched Claude write a 60-line SQL query and nail it first try. genuinely re-examining why I've been letting my ORM write worse SQL for me this whole time

> if the agent writes cleaner SQL than your ORM generates... what is the ORM for

> been using an agent for raw SQL for a week. starting to think ORMs were always scaffolding for people who didn't want to learn SQL. shit works fine without them

## Voice rules (the short list)

- No em-dashes
- No "It's not X, it's Y" reframes
- No throat-clearing openers ("Let's talk about", "Here's what nobody's saying")
- No hedging clutter — unless it's the user's half-thought hedging ("IDK", "starting to think", trailing dots); that's texture, not weakness
- Keep the user's actual phrases from the riff — don't paraphrase into smoother language

## What this is NOT

- Not the 6-step draft process. No voice guide pageantry, no confirmation rounds beyond "ship it?".
- Not an article draft. Takes are one beat, throwaway, out the door.
- Not review-heavy. One sanity check before posting. That's it. No critical review — a stranger-tested take is a contradiction in terms.
- Not a replacement for `/derive`. `/derive` extracts from finished articles; `/take` captures something fresh and small.
