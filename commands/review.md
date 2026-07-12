---
description: Review a draft against the voice guide — check for anti-patterns, voice consistency, energy calibration
argument-hint: "<path to draft file, or 'latest' for most recent>"
---

# /review — Draft Review

**Config**: This command reads directory paths from `config.json`. Falls back to defaults if config is missing.

**Skills Referenced**: writing-process

Review a draft for voice consistency, anti-patterns, and energy calibration.

This is the voice check. For readability and impact as a stranger would read it, use `/critical-review` — the two are deliberately separate reviews.

## Setup

1. Read the voice guide (path from `config.json`, default: `writings/voice-guide.md`) fully.
2. Read the draft file specified. If "latest" or no argument given, find the most recently modified file in the drafts directory (from `config.json`, default: `writings/drafts/`).

## Review checklist

Work through each of these systematically. Be specific. Reference line numbers.

### Voice match
- Does this sound like the user? Read each paragraph and ask: would the user say this out loud to someone?
- Are there sentences that are technically correct but could have been written by anyone?
- Does it open the way the voice guide says this person opens? (Default if the guide is silent: specific experience or observation, not a thesis statement.)
- Does the ending match the voice guide's structural patterns and energy level?

### Energy calibration
- What energy level does the metadata claim? Does the piece actually deliver that level?
- Are there sections that spike to Level 3-4 without earning it?
- Is the intensity consistent or does it wobble?

### Anti-pattern scan
Check for every item in the voice guide's "AI writing anti-patterns" section and "What [name] never sounds like" section. Scan for:

- Em-dashes (AI tell — flag by default; the only pass is a voice guide that explicitly records them as the user's genuine pre-AI habit)
- Every specific anti-pattern listed in the voice guide
- Every "never sounds like" pattern from the voice guide
- Constant intensity (every paragraph at the same energy level with no variation)

Reference the voice guide by name when flagging issues so the user can verify the rule.

### Structural check
Check the draft against the voice guide's structural patterns section — this check is only as person-specific as that section, so use its rules, not a generic template. The kinds of things it typically covers:
- How this person builds an argument (e.g., narrative "here's what happened, here's what I noticed, here's what it means" vs. claim-first)
- Whether strong claims are earned the way this person earns them (usually: showing the work first)
- Their formatting conventions (some voices shift gears with section breaks, some use headers, some write straight through)
- Their sentence rhythm (e.g., short sentences after long ones) — and whether the draft actually varies, or sits at one register throughout

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
