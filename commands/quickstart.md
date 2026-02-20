---
description: Quick voice capture — 5-7 questions to build a starter voice guide
---

# /quickstart — Quick Voice Capture

**Config**: This command reads directory paths from `config.json`. Falls back to defaults if config is missing.

**Skills Referenced**: voice-observation

Fast voice calibration session. Produces a starter voice guide from a short conversation. Good enough for a first draft that's recognizably the person. Not as deep as `/interview`, but gets someone into the drafting loop fast.

## Setup

Check if a voice guide already exists (path from `config.json`, default: `writings/voice-guide.md`). If it does, confirm with the user whether they want to revise the existing one or start fresh. If revising, read the existing guide first so you know what's already captured.

## Mode

Conversational. Warm but not therapist-y. You're getting to know how someone thinks and talks, not analyzing them. Match their energy. If they're casual, be casual. If they're measured, don't force looseness.

## Preamble (before the first question)

Open with something like this — keep it brief since quickstart is already short:

> "Before we start — don't compose, don't edit. Typos, abbreviations, whatever. I'm paying attention to how you communicate, not just what you say. The more this feels like texting a friend, the better. Cool?"

Wait for their response before the first question.

## The questions

Ask these one at a time. Don't dump them all at once. React to each answer before moving to the next. Your reactions should be genuine, not performative ("That's so interesting!"). If something they say sparks a follow-up, take it. The goal is conversation, not a questionnaire.

1. **The opener**: "What do you do, and what's the thing about it that most people misunderstand?" — Gets them talking about their world in their own framing. The "misunderstand" part surfaces how they push back on default narratives.

2. **The opinion**: "What's something in your field that everyone seems to agree on that you think is wrong, or at least oversimplified?" — Surfaces how they argue. Do they build to the point or lead with it? Do they hedge or swing? How do they handle disagreement?

3. **The story**: "Tell me about a time you built or made something you're proud of. Not the polished version. What actually happened?" — Surfaces narrative style. How do they tell stories? Chronological? Do they jump to the point? Where do they put the emotion?

4. **The frustration**: "What's something that drives you nuts that you wish you could fix?" — Surfaces intensity, vocabulary under pressure, natural profanity level, what they care about enough to get heated over.

5. **The uncertainty**: "What's something you're still figuring out? Something you don't have a clean answer for yet?" — Surfaces how they handle ambiguity. Do they sit with it? Rush to resolve it? Flag it honestly?

6. **The taste question**: "Show me something you've read or watched recently that you thought was really well done. What made it good?" — Surfaces their standards, what they aspire to, the gap between what they produce and what they admire.

7. **The anti-pattern** (optional, if time/energy): "What kind of writing or content makes you cringe? Like, what's the stuff you'd never want to sound like?" — Direct signal on what to avoid.

## Voice observation

See the **voice-observation** skill for detailed guidance on reading voice from text.

## Output

After the conversation, generate a voice guide at the voice guide path (from `config.json`, default: `writings/voice-guide.md`). Use this structure:

```markdown
# [Name]'s Voice — Style & Tone Reference

## Core voice identity
[2-3 sentences. Who is this person, how do they communicate, what drives the writing.]

## Default stance
[What lenses do they see through? What do they question by default?]

## Diction and syntax
[How they actually talk. Sentence patterns, vocabulary, profanity, formality level.]

## Structural patterns
[How they build arguments. How they open, develop, close.]

## Energy levels
- Level 1 — [their version of observational/exploratory]
- Level 2 — [their version of analytical/working-through-it]
- Level 3 — [their version of making-a-claim/heat]
- Level 4 — [their version of declarative/final]

## What they sound like when they mean it
[3-5 example phrases from the conversation that felt most authentically them. Quoted exactly.]

## What they never sound like
[Based on their anti-patterns, cringe reactions, and what was notably absent from their speech.]

## Verbal tics and tendencies (natural, keep these)
[Recurring phrases, argument moves, habits worth preserving.]

## Format-specific guidance
See platform format guides (create one with `/formatguide`). Voice stays consistent across formats; structural and length adjustments live in the format guide for each platform.

## AI writing anti-patterns
[Start with common ones. Refine as drafting sessions reveal what sounds wrong in their voice.]
- Em-dashes (AI tell, avoid regardless of personal preference)
- [Others based on conversation]

---

*This is a living document. It gets sharper with every drafting and review session.*
```

Present the voice guide to the person before saving. Ask: "Does this feel like you? What's wrong? What's missing?" Revise based on their feedback, then save.

## Important

This is a starter. Tell them: "This is a first pass. It'll get better every time we write together. The drafting process is where the real calibration happens."

## A note on memory

You don't carry this conversation forward. The voice guide IS your memory. Write it specific enough that a future instance of you, with zero memory of this conversation, can produce output that sounds like this person. If a nuance isn't in the document, it's gone.
