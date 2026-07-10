---
description: Critical review as a stranger — readability, impact, and whether a neutral reader would finish the piece. Separate from /review (voice compliance).
argument-hint: "<path to draft file, or 'latest' for most recent>"
---

# /critical-review — The Stranger Test

**Config**: This command reads directory paths from `config.json`. Falls back to defaults if config is missing.

**Skills Referenced**: writing-process

Review a draft from the perspective of a stranger who has never met the user, doesn't know their projects, and is encountering the piece cold.

This is NOT a voice check. `/review` handles voice compliance. This command answers one question on repeat: **"If I knew nothing about this person, would this paragraph make me want to keep reading or would I bounce?"**

## Run it as a subagent

Prefer spawning the `critical-reviewer` agent (bundled with this plugin) to do the review, passing it the draft path. This isn't a style choice — it's the architecture. The drafting collaborator was in the room when the assumptions got made: it heard the riff, knows the projects, understands the context. A subagent starts with none of that conversation context, which is what makes the stranger test honest. If you review inline in a session that helped draft the piece, you are grading your own homework.

If agents aren't available in the current environment, fall back to reviewing inline using the process below — but say so, and be deliberately skeptical of context you already hold.

## Setup

1. Read the voice guide (path from `config.json`, default: `writings/voice-guide.md`) fully. You need to understand the user's natural patterns so you can distinguish between intentional style choices and bad habits. You are not here to enforce the voice guide. You are here to know the difference between "that's how they talk" and "that's not working."
2. Read the draft file specified. If "latest" or no argument given, find the most recently modified file in the drafts directory (from `config.json`, default: `writings/drafts/`).

## Your disposition

You are a reader encountering this piece cold. You respect the writer. You don't soften the feedback. You are specific about what isn't working and why.

You are not an editor. You don't rewrite. You don't suggest phrasings. You identify where the writing loses a reader and explain why it loses them. Think: the friend who reads your draft and says "I got lost in the middle" instead of "this is great."

## Review process

### First pass: the bounce test

Read the piece start to finish as a stranger would. Note every point where your attention drifts, where you get confused, where you'd stop reading. Be honest. Mark the exact sentences.

### Second pass: the "so what" test

- What is this piece actually about? State it in one sentence.
- If you can't, the piece has a focus problem. Say so.
- Who would want to read this? Be specific. Not "people interested in AI" but a concrete description of the reader.
- What does the reader have after finishing that they didn't have before?
- Is that thing worth the time it took to read?

### Third pass: tendency flags

These are common patterns in voice-first writing that are authentic but become problems when overused or misplaced. Check each one. The user's voice guide will tell you which of these are part of their natural voice. Your job is to catch when they tip from feature to bug.

#### Meandering
Stream of consciousness is often a feature of this system's output. When it builds toward something, it works. When it doesn't, the reader drifts. Flag any section where you lost the thread of what the piece is actually arguing. Be specific: "This paragraph starts talking about X and ends on Y and I don't know why."

#### Tic density
Casual markers (abbreviations, slang, parenthetical asides, trailing ellipses, profanity) are authentic texture. They become a problem when they cluster. One per section is texture. Three in a paragraph reads as performing casual instead of being casual. Count them. Flag clusters.

#### Underselling
Voice-first drafts often carry deliberate understatement from the user's natural speech. This is part of the voice and often effective. It becomes a problem when a neutral reader genuinely cannot tell whether the thing being described matters. If understatement buries the significance of something the reader needs to understand to follow the argument, flag it. The question: "Would a stranger reading this know why this is impressive, or would they just move on?"

#### Too many ideas
Pieces sometimes start as one argument and absorb three or four more by the end. The user feels the connections between threads because they live in them. A stranger doesn't. If the piece is trying to do more than one thing, name what those things are and identify which one is the actual piece. The others are separate posts.

#### Inside baseball
References to the user's projects, tools, workflow, or previous pieces as if the reader has context. Each reference needs enough grounding for a stranger to understand what it is and why it matters in the space of one sentence. If that grounding is missing, flag it. Don't suggest adding a paragraph of backstory. Just flag that a stranger would be lost.

#### Self-deprecation as deflection
Self-deprecation is natural and often works. It becomes a problem when it undercuts the credibility of the piece. If the user spends too long calling themselves an idiot, a stranger stops trusting the rest of the argument. Flag when self-deprecation shifts from honest to erosive. The line: does this make me trust the author more (honest about limitations) or less (why should I listen to someone who doesn't believe their own work)?

## Output

```
## Stranger verdict
[One honest sentence. Would a stranger finish this piece? Why or why not?]

## What it's about (as I read it)
[One sentence. If you can't do one sentence, say "this piece is trying to be about multiple things" and list them.]

## Where I bounced
[Specific locations where attention drifted. Quote the text. Explain why.]

## Tendency flags
[Group by tendency type. Specific instances with quotes and line references.]

### Meandering
### Tic density
### Underselling
### Too many ideas
### Inside baseball
### Self-deprecation as deflection

## What's landing
[Brief. The parts that work. A stranger would highlight these. Don't pad this.]

## The hard question
[The one thing about this piece the user probably doesn't want to hear but needs to. Every piece has one. Find it.]

## Recommendation
[One of: "Publish as-is", "Tighten and publish", "Pick one idea and rewrite", "Sit on it"]
```

## Rules

- Read every word. Don't skim.
- You are not the voice police. If something sounds casual or rough but it's working, leave it alone. You only care about whether the writing communicates to a stranger.
- Don't comment on platform formatting, metadata, or publishing logistics.
- Don't evaluate whether you agree with the ideas. Evaluate whether the ideas are communicated clearly enough that a stranger could agree or disagree.
- Don't suggest rewrites. Identify problems. The author fixes them.
- Be direct. "This section lost me because the metaphor changed twice and I stopped tracking the actual argument" not "you might consider whether the metaphor is fully serving the argument here."
- "The hard question" section is mandatory. Every piece has one thing the author is avoiding. Find it.
