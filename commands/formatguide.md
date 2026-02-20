---
description: Quick platform interview to generate a format guide for a specific platform
argument-hint: "<platform name (e.g., linkedin, substack, twitter)>"
---

# /formatguide — Platform Format Guide

**Config**: This command reads directory paths from `config.json`. Falls back to defaults if config is missing.

Quick interview to capture platform strategy and format preferences. Produces a format guide that works alongside the voice guide to constrain content for a specific platform.

## Mode

Informational, not probing. This is not a voice interview. You're gathering preferences and strategy decisions, not uncovering subtle patterns. Ask the question, acknowledge the answer briefly, move to the next one. React genuinely but don't dig unless something is genuinely unclear. Keep this moving. The whole thing should take 10-15 minutes, not an hour.

## Setup

If no platform argument is provided, ask which platform they want to create a guide for.

Read the voice guide (path from `config.json`, default: `writings/voice-guide.md`) first so you understand who you're building this for. The format guide should complement the voice, not contradict it.

Check if a format guide already exists for this platform at the format guides directory (from `config.json`, default: `writings/format-guide-[platform].md`). If it does, confirm with the user whether they want to revise the existing one or start fresh.

## The questions

Ask these one at a time. Brief acknowledgment between each. Don't turn answers into a conversation — just confirm you got it and move on. If something is genuinely ambiguous, one follow-up is fine. Two is too many.

1. **The goal**: "What are you trying to build on [platform]? Not metrics. What's the persona or reputation you want when someone lands on your profile?"

2. **The good stuff**: "What do you actually like seeing on [platform]? When you stop scrolling and read something, what made you stop?"

3. **The cringe**: "What makes you want to throw your phone when you see it on [platform]?"

4. **The format feel**: "How do you feel about [platform's] norms? Play within them, push against them, ignore them? Any specific format conventions you want to lean into or reject?"

5. **The connection**: "How does [platform] relate to your other content? Does stuff flow in from articles, other platforms, or a creation process? Or is this standalone?"

6. **The cadence**: "Scheduled posting or organic 'when there's something to say'?"

## Output

After the six questions, generate a format guide at the format guides directory (from `config.json`, default: `writings/format-guide-[platform].md`). Use this structure:

```markdown
# [Platform] Format Guide

## What this is

Format and structural reference for [platform] content. Separate from the voice guide — the voice guide captures how [name] sounds, this doc captures what good [platform] content looks like structurally. Both constrain AI output during drafting and derivation.

## Strategy intent
[Goal and persona from Q1. 2-3 sentences.]

## [Platform] content

### Length
[Based on Q2 and Q4. What length feels right given their preferences and platform norms.]

### Opening
[Based on Q2 and voice guide. How to hook without gaming.]

### Structure
[Based on Q2, Q4. Conversational flow, formatting preferences, what works on this platform for this person.]

### Endings
[Based on voice guide and Q4. How to close.]

### What stays out
[Based on Q3. Platform-specific anti-patterns and cringe triggers.]

## Derivation
[Based on Q5. If content flows from articles or other sources, describe the derivation relationship. If standalone, note that.]

## Platform realities (acknowledged, not optimized for)
[Honest assessment of platform dynamics. What the algorithm rewards vs. what the user actually wants. Based on Q4 and Q6.]

## Product note
This doc is designed to be generalizable. The structure — strategy intent, format preferences, derivation process — could be templated for any user negotiating their own platform preferences through a format interview.

---

*Living document. Refines through use.*
```

Present the format guide before saving. Ask: "Does this capture it? Anything wrong or missing?" One round of revisions, then save.

## Important

Keep it light. This is a 10-minute capture, not a deep dive. The format guide will sharpen through actual use — drafting sessions and derivation runs will surface what's missing. Get the foundation down and move on.

## A note on memory

Same as the voice guide: you don't carry this conversation forward. The format guide IS the memory. Write it specific enough that a future session can produce platform-appropriate content without this conversation's context.
