---
description: Resume an in-progress draft — pick up where the last session left off
argument-hint: "<filename in drafts/, or 'list' to see what's in progress>"
---

# /resume — Resume a Draft

**Config**: This command reads directory paths from `config.json`. Falls back to defaults if config is missing.

**Skills Referenced**: writing-process

Pick up an in-progress draft from where the last session left off.

## Before anything else

Read the voice guide (path from `config.json`, default: `writings/voice-guide.md`) fully. Same as `/draft`, non-negotiable.

## Mode

Same as `/draft`: conversational mode for the entire session. Riff, react, follow up, match energy.

## Find the draft

If a filename is provided, read that file from the drafts directory (from `config.json`, default: `writings/drafts/`).

If "list" or no argument, scan the drafts directory and show the user what's there with status and last modified date. Let them pick.

## Load context

1. **Read the draft file**, including any `<!-- WORKING NOTES -->` block at the bottom.
2. **Read the most recent session summary** (in the planning directory from `config.json`, default: `planning/session-summary-*.md`, most recent by date) for additional context on where things were left.
3. **Read the content backlog** (from `config.json`, default: `planning/content-backlog.md`) if the working notes reference a thread.

## Reorient

Give the user a brief summary of where things stand:
- What the piece is about (from working notes or draft content)
- What step was last completed
- Strongest lines captured so far
- Any open questions from the previous session
- What the next step is

Ask: "Does this still feel right, or has your thinking shifted since last time?"

This is important. Time between sessions changes perspective. The user might want to pick up exactly where they left off, or they might want to redirect. Don't assume continuity. Check.

## Continue the process

Pick up from whatever step comes next:

- **If stopped during Step 1 (riff)**: Resume riffing. Read back what was captured, ask if there's more, or if it's enough to pull from.
- **If stopped during Step 2 (pull)**: Do the pull from the captured riff material. Reflect back strongest lines, argument, structure, energy, platform.
- **If stopped during Step 3 (confirm)**: Show the pull again, resume the confirmation conversation.
- **If stopped during Step 4 (draft)**: Either continue drafting from where it stopped, or if the user has new input, incorporate and redraft.
- **If the draft exists but needs revision**: Treat this like a continuation of Step 4. Read the draft, ask what's working and what isn't, revise.

From here, follow the same rules as `/draft` — raw-first, voice guide constrained, the user's actual phrases, no AI smoothing.

## Update working notes

If the session ends before the piece is finished again, update the `<!-- WORKING NOTES -->` block with current state. Overwrite the previous notes, don't stack them.

When the draft is complete and ready for the out-loud read, remove the working notes block. They've served their purpose.
