# Voice-First Writing

A voice-first writing system for [Cowork](https://claude.com/product/cowork) and Claude Code. Captures how you actually sound and produces content in your authentic voice, not AI writing about your ideas.

The system works by getting you talking naturally, observing how you communicate (not what you say about how you communicate), and building a living voice guide that sharpens with every session. Drafts are built raw-first from your speech patterns, then sculpted. The result sounds like you because it started as you.

## Installation

```
claude plugins add voice-first-writing
```

## Quick Start

### 1. Install the plugin

```
claude plugins add voice-first-writing
```

### 2. Run setup

```
/setup
```

Setup walks you through:
- Configuring your workspace (directory structure, preferences)
- Capturing your voice (quick 10-minute version or deep extended interview)
- Creating your first platform format guide
- Orientation to the system

### 3. Start writing

```
/draft
```

## Commands

### `/setup` — First-Time Onboarding

Creates your workspace, captures your voice, and walks you through the system. Run this once.

### `/interview` — Deep Voice Capture

Extended conversation (30-60 min) that produces a comprehensive voice guide. The AI gets you talking about what you care about and observes how you communicate. Not a questionnaire. A conversation designed to surface authentic voice.

### `/quickstart` — Quick Voice Capture

Shorter version (10-15 min). Gets a working voice guide from 5-7 questions. Good enough for a first draft, refines through use.

### `/draft` — Drafting Session

The main creative workflow. You riff on an idea, the AI pulls the strongest lines and structure, you confirm, and the AI drafts raw-first in your voice. Follows the 6-step writing process.

### `/flywheel` — The Content Flywheel

Generates a cycle's worth of platform posts from web research intersected with what you've actually been building. Reads your tinkering log, asks what's on your mind, scans your projects, researches the discourse, and drafts posts that pass through the portable-observation gate ("would this still be interesting if you stripped the project context?") and critical review. Your platform strategy doc — audience, cadence, register mix, never-scan list — is the contract; the flywheel is just the engine. Publishing integration (Typefully) is optional, bring-your-own-key.

### `/derive` — Article to Posts

Derives 2-3 standalone platform posts from a finished article. Each post extracts one insight and stands on its own. Not a summary, not a promo.

### `/review` — Draft Review

Reviews a draft against your voice guide for anti-patterns, voice consistency, and energy calibration. Flags specific issues with suggested fixes.

### `/critical-review` — The Stranger Test

Reviews a draft as a stranger who has never met you and is encountering the piece cold. Not a voice check — that's `/review`. This one answers: would a neutral reader keep reading, or bounce? Flags where attention drifts, when authentic tendencies tip into overuse, and asks the hard question every piece is avoiding. Identifies problems; doesn't rewrite.

Runs as an isolated subagent (the bundled `critical-reviewer` agent) so the reviewer genuinely has no memory of the drafting session — the context isolation is what makes the stranger test honest. Its verdict is advisory, not binding: the writing-process skill documents how writer/critic conflicts get resolved without sanding the voice off.

### `/resume` — Resume a Draft

Picks up an in-progress draft from where the last session left off. Loads working notes, reorients, and continues the process.

### `/publish` — Publish Content

Handles both articles and posts. Articles move from `ready/` to `published/` with full confirmation. Posts move from `posts/` to `posts/published/` with a lighter flow that supports bulk publishing. Updates tracking docs for both.

### `/wrap` — Session Wrap

Closes out a working session with documentation. Creates a session summary, checks for voice guide updates, captures new content ideas.

### `/formatguide` — Platform Format Guide

Quick interview to generate a format guide for a specific platform (LinkedIn, Substack, etc.). The format guide works alongside the voice guide to constrain content for that platform.

## Skills

| Skill | Description |
|-------|-------------|
| `writing-process` | The 6-step voice-first methodology: riff, pull, confirm, draft raw-first, critical review, read out loud. Self-updating system for voice guides and process refinement. |
| `voice-observation` | How to read voice from typed text. Signals, patterns, and mental model building for text-based voice capture. |
| `tinkering` | Autonomous capture of what you just built, wherever you built it. Appends short dated entries to a global log that feeds the content flywheel. Fires on its own when a real unit of work wraps — no ceremony. |

## The Writing Process

1. **You talk.** Riff on the idea. Not bullet points, not a thesis. Just talk about it.
2. **AI pulls.** Identifies strongest lines, real argument, natural structure, energy level. Reflects it back.
3. **You confirm or correct.** A conversation, not a review. Everything stays anchored to how you said it.
4. **AI drafts, constrained.** Bound by your voice guide, your actual phrases, the agreed energy level. First draft is raw, not polished.
5. **A stranger reads it cold.** The critical review catches what the drafting collaborator can't — it was in the room when the assumptions got made. Fresh eyes find where a neutral reader bounces.
6. **You read it out loud.** Any sentence that feels wrong coming out of your mouth gets cut or rewritten.

Raw-first, always. A draft that sounds like you talking at a bar is right. A draft that reads like a finished article is too polished.

## Configuration

`/setup` creates a `config.json` in your project root:

```json
{
  "voice_observation_mode": "always-on",
  "default_platform": null,
  "directories": {
    "drafts": "writings/drafts",
    "ready": "writings/ready",
    "published": "writings/published",
    "posts": "writings/posts",
    "posts_published": "writings/posts/published",
    "planning": "planning",
    "voice_guide": "writings/voice-guide.md",
    "format_guides": "writings"
  }
}
```

- **`voice_observation_mode`**: `"always-on"` observes voice patterns during any command and flags updates. `"wrap-only"` saves voice observation for `/wrap` sessions only.
- **`default_platform`**: Set to `"linkedin"`, `"substack"`, etc. to skip the platform prompt. `null` means always ask.
- **`directories`**: All paths relative to project root. Customize to match your workspace structure.

## File Structure

```
voice-first-writing/
├── .claude-plugin/plugin.json
├── CLAUDE.md
├── README.md
├── config.template.json
├── commands/
│   ├── setup.md
│   ├── interview.md
│   ├── quickstart.md
│   ├── draft.md
│   ├── derive.md
│   ├── review.md
│   ├── resume.md
│   ├── publish.md
│   ├── wrap.md
│   └── formatguide.md
└── skills/
    ├── writing-process/
    │   └── SKILL.md
    └── voice-observation/
        └── SKILL.md
```

## How It Works

The system solves a specific problem: AI-assisted writing drifts toward the AI's voice. The back-and-forth process (AI drafts, human edits) produces content that's competent and readable but could have been written by anyone. The rough edges, specific cadence, moments of uncertainty and sudden clarity get smoothed out.

The fix isn't better prompts. It's a different process.

Instead of generating text and injecting personality, the system captures your natural voice first and constrains the AI to it. The voice guide is a living document that evolves with use. Every drafting session, every review, every session wrap is an opportunity to sharpen the model of how you communicate.

Over time, the system gets better. Not because the AI learns (it doesn't carry memory between sessions), but because the documentation gets more precise with every interaction.

## The Self-Updating System

- **Voice guide**: Updated when new patterns are observed, when drift is detected, when anti-patterns emerge.
- **Format guides**: Refined through actual use in drafting and derivation.
- **Session summaries**: Capture decisions, observations, and what's queued for next time.

The AI flags potential updates during sessions. You approve or reject. Nothing changes without your say.
