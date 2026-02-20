---
description: Review a draft against the voice guide — check for anti-patterns, voice consistency, energy calibration
argument-hint: "<path to draft file, or 'latest' for most recent>"
---

# /review — Draft Review

**Config**: This command reads directory paths from `config.json`. Falls back to defaults if config is missing.

**Skills Referenced**: writing-process

Review a draft for voice consistency, anti-patterns, and energy calibration.

## Setup

1. Read the voice guide (path from `config.json`, default: `writings/voice-guide.md`) fully.
2. Read the draft file specified. If "latest" or no argument given, find the most recently modified file in the drafts directory (from `config.json`, default: `writings/drafts/`).

## Review checklist

Work through each of these systematically. Be specific. Reference line numbers.

### Voice match
- Does this sound like the user? Read each paragraph and ask: would the user say this out loud to someone?
- Are there sentences that are technically correct but could have been written by anyone?
- Does it open with a specific experience or observation (not a thesis statement)?
- Does the ending match the voice guide's structural patterns and energy level?

### Energy calibration
- What energy level does the metadata claim? Does the piece actually deliver that level?
- Are there sections that spike to Level 3-4 without earning it?
- Is the intensity consistent or does it wobble?

### Anti-pattern scan
Check for every item in the voice guide's "AI writing anti-patterns" section and "What [name] never sounds like" section. Scan for:

- Em-dashes (universal AI tell, always flag regardless of voice guide)
- Every specific anti-pattern listed in the voice guide
- Every "never sounds like" pattern from the voice guide
- Constant intensity (every paragraph at the same energy level with no variation)

Reference the voice guide by name when flagging issues so the user can verify the rule.

### Structural check
- Does it build through narrative ("here's what happened, here's what I noticed, here's what it means")?
- Are strong claims earned by showing the work first?
- Are section breaks (---) used to shift gears instead of headers?
- Do short sentences follow long ones? Is there rhythm variation?

### Verbal tics check
Review the voice guide's "Verbal tics and tendencies" section. These should be present in the draft (sparingly, naturally). Their absence often means the draft has been over-polished. Check:
- Are the person's signature phrases and verbal habits showing up?
- Do recurring moves appear where they'd naturally occur?
- Has over-editing stripped out the texture that makes it sound like them?

### The test
For each flagged issue, provide:
1. The specific text (quoted)
2. Why it's a problem (which rule it violates)
3. A suggested fix, or "ask the user how they'd say this"

## Output

After the full review, summarize:
- **Verdict**: Ready for the ready directory? Or needs another pass?
- **Strongest lines**: The parts that are most authentically the user
- **Issues found**: Prioritized list (voice-breaking issues first, minor polish last)
- **Suggested edits**: Specific changes, not vague direction

If the piece is ready, ask if the user wants to move it to the ready directory (from `config.json`, default: `writings/ready/`). When moving:
- Strip any `<!-- WORKING NOTES -->` block from the file. Those are drafting artifacts and don't belong in a finished piece.
- Update the **Status** in the metadata to "Ready".
