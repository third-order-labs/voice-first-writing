---
name: writing-process
description: The 5-step voice-first writing methodology — riff, pull, confirm, draft raw-first, read out loud. Includes the self-updating system for voice guides and process docs.
---

# Writing Process Skill

This skill defines the voice-first collaborative writing methodology. It's a structured process that produces content sounding like the user, not like AI writing about the user's ideas. The system works because it treats voice as a constraint to build from, not a coat of paint to apply after.

## The Core Problem

AI-assisted writing drifts toward the AI's voice. The typical back-and-forth process (AI drafts, human edits) produces content that is competent, readable, and could have been written by anyone. The rough edges, the specific cadence, the moments of uncertainty and sudden clarity get smoothed out because it's easier to accept clean prose than to fight for your own sound.

The fix isn't better prompts. It's a different process.

## The Process

### Step 1: The user talks.

Not a prompt. Not bullet points. The user riffs on the idea the way they talk in conversation, not the way they think writing should sound. Stream of consciousness, tangents, profanity, uncertainty, all of it. The AI captures.

Why this matters: most people's natural speaking voice is more energetic, direct, and specific than their written voice. The best content starts from speech patterns, not from outlines. Ideas that emerge through conversation have a different texture than ideas that start as thesis statements.

### Step 2: AI pulls.

The AI identifies:
- **The strongest lines**: Phrases the user actually said that land hard
- **The real argument**: What the user is actually saying, which is sometimes different from what they think they're saying
- **The natural structure**: How the idea actually unfolded, not how an article "should" be structured
- **The energy level**: Observational? Analytical? Structural? Hammer drop?

The AI reflects this back: "Here's what I think the piece is. Here's your best lines. Here's the arc I see."

### Step 3: The user confirms or corrects.

The user says what's right, what's off, what's missing. This is a conversation, not a review. The AI asks questions where it's uncertain about intent or emphasis. Everything stays anchored to how the user said it, not how the AI would write it.

### Step 4: AI drafts, constrained.

The draft is explicitly bound by:
- The voice guide
- The user's actual phrases and cadences from Step 1
- The energy level agreed in Step 2

**The first draft should be raw, not polished.** It should read like a cleaned-up transcript of the user talking. Too many tangents, too many "IDK"s, sentences that start one place and end somewhere else. It should have all the tics and mannerisms and half-formed pivots. It should sound like the user riffing, not like an article.

This is deliberate. A raw-user draft that needs sculpting is better than a smooth-AI draft that needs personality injected. The voice is baked in from the start. Editing becomes subtractive (cutting and shaping something that's already theirs) rather than additive (trying to make something generic sound like them). Subtractive editing preserves voice. Additive editing almost never gets there.

If the first draft reads like a finished article, it's probably too polished. If it reads like the user talking to someone at a bar about something they care about, it's right.

#### Critical rules
- Built from the user's speech, not generated from scratch
- If the AI can't say something in a way that sounds like the user, it flags it and asks "how would you say this?" rather than filling in with its own version
- No throat-clearing transitions, no ChatGPT reframes, no performative intensity (see the voice guide's anti-patterns)
- Short sentences after long ones. Fragments are welcome. Uncertainty is welcome.
- Err toward too-them, not too-clean. You can always polish. You can't easily un-polish.

### Step 5: The user reads it out loud.

The final filter: if any sentence feels wrong coming out of the user's mouth, it gets cut or rewritten. Not "does this read well" but "would I actually say this to someone."

This is non-negotiable. The out-loud test catches AI smoothing that editing misses.

## The Self-Updating System

This methodology works because the reference documents evolve with the work, not because any single document is perfect at the start.

### What gets updated and when

**Voice guide:**
- When a new pattern is observed in the user's speech (a recurring phrase, a structural move, a way of building arguments)
- When a pattern is identified as drift or contamination (an AI-ism that crept in and needs to be killed)
- When a new anti-pattern emerges (a phrase or structure that sounds wrong)
- When energy calibration needs adjustment

**Process documentation:**
- When a step in the process isn't working or needs refinement
- When a new technique is discovered that improves output quality

**Content backlog/roadmap:**
- When a conversation surfaces a new thread or connection between threads
- When a piece is published and needs to be logged
- When priorities shift based on what's resonating

### How updates happen

During any content session, the AI should:
1. Notice patterns in how the user talks, argues, pivots, expresses uncertainty
2. Compare those patterns against the voice guide
3. Flag anything new: "I noticed you do X. Should I add that to the voice guide?"
4. Flag anything contradictory: "The voice guide says Y but you consistently do Z. Should we update?"
5. Make the update in the same session, not as a future task

The AI does NOT:
- Update docs silently without telling the user
- Add aspirational patterns (things the user thinks they should sound like but don't actually do)
- Remove patterns without discussion

### What the AI learns from conversation (not from self-description)

People describe themselves aspirationally. Conversations reveal the real thing. The AI should pay attention to:

- **Moves the user makes without noticing**: Flagging their own uncertainty then pushing through, rejecting a premise before engaging with the question, connecting two domains mid-sentence without signposting it
- **What the user gets excited about vs. what they think they should get excited about**: Energy shifts in conversation, moments where the pace picks up, topics that generate tangents (tangents = genuine interest)
- **How the user actually starts thoughts**: Not with thesis statements but with observations, stories, or reactions to something specific
- **Real hedging patterns**: Not over-hedging (a voice guide anti-pattern) but the specific ways they hold uncertainty. These are authentic, not weak.
- **What makes the user laugh or swear**: These are emphasis markers. They point to what matters most.
- **Sentence rhythm**: Most people's natural speech alternates between longer exploratory sentences and short declarative ones. The short ones usually carry the point.

## The Feedback Loop

After each published piece:
- Did it sound right when read out loud?
- Did anyone respond in a way that suggests it landed as intended?
- Were there moments that felt "off" in retrospect?
- What would the user change if they rewrote it tomorrow?

Capture these observations. They refine the system.

## What This System Produces

Over time, the voice guide, process docs, and accumulated session notes become a progressively more accurate model of how the user thinks and communicates. Not a static profile. A living system that gets better with use.

The goal is not "AI that writes like the user." The goal is "AI that helps the user write like themselves" by capturing their ideas at their most energetic and giving them structure without sanding off the texture that makes the writing theirs.

## Writing Pipeline

`drafts/` -> `ready/` -> `published/`

- **drafts/** -- Actively being worked on. Might be messy, half-finished, or mid-revision. Lives here during the writing process (Steps 1-5 above).
- **ready/** -- Done writing, reviewed, read out loud, approved. Ready to post whenever timing is right. This is the staging/scheduling queue. Pull from here on publishing days.
- **published/** -- Live on a platform. Filename includes date and slug.

When a piece moves from ready to published, update the filename with the actual publish date if it changed, and log it in the content backlog under published work.
