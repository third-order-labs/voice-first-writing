---
description: End-of-session wrap — create session summary, flag voice guide updates, capture new ideas
---

# /wrap — Session Wrap

**Config**: This command reads directory paths from `config.json`. Falls back to defaults if config is missing.

**Skills Referenced**: voice-observation

Close out a working session with proper documentation.

## Before starting

Check that these exist and handle gracefully if missing:
- Voice guide (path from `config.json`, default: `writings/voice-guide.md`) — if missing, skip the voice guide check section. Note: "No voice guide found. Consider running `/setup` or `/quickstart` to create one."
- Content backlog (path from `config.json`, default: `planning/content-backlog.md`) — if missing, skip the content backlog check. Note: "No content backlog found. New ideas from this session will be included in the session summary instead."
- Planning directory (from `config.json`, default: `planning/`) — if missing, create it before writing the session summary.

Also check `config.json` for the `voice_observation_mode` setting:
- If `"always-on"`: Voice observations may have already been flagged during the session. During the voice guide check below, focus on anything that wasn't already surfaced, and consolidate any observations that were flagged but not yet written to the voice guide.
- If `"wrap-only"`: This is the designated time to review the full conversation for voice patterns. Do the complete voice guide check below.
- If config is missing or the setting isn't present, default to doing the full voice guide check.

The session summary itself is always created — that's the minimum output of `/wrap`.

## Session summary

Create a session summary at the planning directory using the path pattern `session-summary-YYYY-MM-DD.md` (using today's date).

If a summary already exists for today (from an earlier session), append to it with a section header noting this is a continuation.

Include:

- **What was worked on**: Drafts created/edited, pieces moved through the pipeline, planning updates
- **Decisions made**: Any choices about content direction, voice guide changes, process changes
- **Observations**: New patterns noticed, ideas that surfaced, thread connections discovered
- **Voice guide updates**: Any changes made to the voice guide during this session (or note "none")
- **What's ready to execute next**: What's queued up for the next session

Keep it concise and factual. This is a reference doc, not a narrative.

## Voice guide check

Review the conversation for:
- **New patterns**: Did the user make any verbal moves, argument structures, or phrasing choices that aren't captured in the voice guide?
- **New anti-patterns**: Did anything come up that sounded wrong or AI-generated that should be added to the kill list?
- **Contradictions**: Did the user consistently do something that contradicts the current voice guide?

If any of these are found:
1. Flag them to the user with specific examples from the conversation
2. If the user agrees, update the voice guide in this session
3. Note the update in the session summary

## Content backlog check

Review the conversation for:
- New content ideas or topics that surfaced
- New connections between existing threads
- New observations worth capturing as raw material

If found, add them to the content backlog (path from `config.json`, default: `planning/content-backlog.md`) in the appropriate section (new thread, existing thread observation, or evergreen post queue).

## Confirm

Tell the user what was captured and written. Keep it brief.
