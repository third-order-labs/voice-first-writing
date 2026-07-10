# Voice-First Writing

A voice-first writing system for [Claude Code](https://claude.com/claude-code) and [Cowork](https://claude.com/product/cowork). Captures how you actually sound and produces content in your authentic voice, not AI writing about your ideas.

The system works by getting you talking naturally, observing how you communicate (not what you say about how you communicate), and building a living voice guide that sharpens with every session. Drafts are built raw-first from your speech patterns, then sculpted. The result sounds like you because it started as you.

It solves two problems that show up in every long-running writing agent:

1. **Agentic voice drift.** AI-assisted writing converges on the AI's voice. Session after session, the rough edges, specific cadence, and moments of uncertainty get smoothed into competent text that could have been written by anyone. This system's answer is a set of drift countermeasures: a living voice guide the agent is constrained by (and that updates from observation, not self-description), an anti-pattern kill list, energy calibration, texture preservation rules, and a read-aloud gate as the final human filter. See [How It Works](#how-it-works).
2. **Writer/critic conflict.** A drafting agent and a reviewing agent will disagree, and naively applying the critic's feedback sands every draft down to the same neutral competence. This system runs the critic as an isolated subagent with zero drafting context (the "stranger test") and resolves conflicts with explicit jurisdiction rules: the critic is advisory, the writer's source phrasings are protected, and stripping all texture is defined as the failure mode. See [The Writer/Critic Architecture](#the-writercritic-architecture).

## Installation

In Claude Code:

```
/plugin marketplace add third-order-labs/claude-plugins
/plugin install voice-first-writing@third-order-labs-plugins
```

## Quick Start

### 1. Run setup

```
/setup
```

Setup walks you through:
- Configuring your workspace (directory structure, preferences)
- Capturing your voice (quick 10-minute version or deep extended interview)
- Creating your first platform format guide
- The strategy interview: what you build, what's off-limits, what you keep coming back to, where it publishes
- Orientation to the system

### 2. Start writing

```
/draft
```

### 3. Let the flywheel take over

Work on your projects as usual — the `tinkering` skill autonomously logs what you build. Then, once a cycle:

```
/flywheel
```

It intersects your recent work with web research and drafts a batch of posts in your voice, each one critically reviewed before it reaches you.

## Commands

### `/setup` — First-Time Onboarding

Creates your workspace, captures your voice, interviews you about your projects and platforms, and walks you through the system. Run this once.

### `/interview` — Deep Voice Capture

Extended conversation (30-60 min) that produces a comprehensive voice guide. The AI gets you talking about what you care about and observes how you communicate. Not a questionnaire. A conversation designed to surface authentic voice.

### `/quickstart` — Quick Voice Capture

Shorter version (10-15 min). Gets a working voice guide from 5-7 questions. Good enough for a first draft, refines through use.

### `/draft` — Drafting Session

The main creative workflow. You riff on an idea, the AI pulls the strongest lines and structure, you confirm, and the AI drafts raw-first in your voice. Follows the 6-step writing process.

### `/flywheel` — The Content Flywheel

Generates a cycle's worth of platform posts from web research intersected with what you've actually been building. Reads your tinkering log, asks what's on your mind, scans your projects, researches the discourse, and drafts posts that pass through the portable-observation gate ("would this still be interesting if you stripped the project context?") and critical review. Your platform strategy doc — audience, cadence, register mix, never-scan list — is the contract; the flywheel is just the engine. Publishing integration (Typefully) is optional, bring-your-own-key.

### `/take` — Capture a Hot Take

Zero-friction capture for the short spicy one-off before it evaporates. Pulls the most recent take-shaped riff from the conversation (or takes your text), applies minimal shaping under explicit spicy-preservation rules — one move not three, keep the half-thought markers, no neat conclusions — and saves or ships. Deliberately skips the full process: no voice-guide ceremony, no critical review. Status lives in frontmatter, not folders.

### `/derive` — Article to Posts

Derives 2-3 standalone platform posts from a finished article. Each post extracts one insight and stands on its own. Not a summary, not a promo.

### `/review` — Draft Review

Reviews a draft against your voice guide for anti-patterns, voice consistency, and energy calibration. Flags specific issues with suggested fixes. This is the voice check; `/critical-review` is the readability check. Deliberately separate reviews.

### `/critical-review` — The Stranger Test

Reviews a draft as a stranger who has never met you and is encountering the piece cold. Not a voice check — that's `/review`. This one answers: would a neutral reader keep reading, or bounce? Flags where attention drifts, when authentic tendencies tip into overuse, and asks the hard question every piece is avoiding. Identifies problems; doesn't rewrite.

Runs as an isolated subagent (the bundled `critical-reviewer` agent) so the reviewer genuinely has no memory of the drafting session — the context isolation is what makes the stranger test honest.

### `/resume` — Resume a Draft

Picks up an in-progress draft from where the last session left off. Loads working notes, reorients, and continues the process.

### `/newsletter` — Periodic Newsletter

Assembles a newsletter from what you published and built during a period: a curated roundup, one deeper insight piece (riffed with you, never fully automated — that's what keeps it from reading like an AI digest), and a build-in-public note from the trenches. Runs the whole thing through critical review before you see it.

### `/publish` — Publish Content

Handles both articles and posts. Articles move from `ready/` to `published/` with full confirmation. Posts move from `posts/` to `posts/published/` with a lighter flow that supports bulk publishing. Updates tracking docs for both.

### `/wrap` — Session Wrap

Closes out a working session with documentation. Creates a session summary, checks for voice guide updates, captures new content ideas.

### `/formatguide` — Platform Format Guide

Quick interview to generate a format guide for a specific platform (LinkedIn, Substack, etc.). The format guide works alongside the voice guide to constrain content for that platform.

## Skills

| Skill | Description |
|-------|-------------|
| `writing-process` | The 6-step voice-first methodology: riff, pull, confirm, draft raw-first, critical review, read out loud. Self-updating system for voice guides and process refinement. Includes the writer/critic conflict-resolution rules. |
| `voice-observation` | How to read voice from typed text. Signals, patterns, and mental model building for text-based voice capture. |
| `tinkering` | Autonomous capture of what you just built, wherever you built it. Appends short dated entries to a global log that feeds the content flywheel. Fires on its own when a real unit of work wraps — no ceremony. |

## Agents

| Agent | Description |
|-------|-------------|
| `critical-reviewer` | The stranger. Reads a draft cold with zero drafting-session context and reports where a neutral reader bounces, which authentic tendencies tipped into overuse, and the one hard question the piece is avoiding. Advisory by design. |

## The Writing Process

1. **You talk.** Riff on the idea. Not bullet points, not a thesis. Just talk about it.
2. **AI pulls.** Identifies strongest lines, real argument, natural structure, energy level. Reflects it back.
3. **You confirm or correct.** A conversation, not a review. Everything stays anchored to how you said it.
4. **AI drafts, constrained.** Bound by your voice guide, your actual phrases, the agreed energy level. First draft is raw, not polished.
5. **A stranger reads it cold.** The critical review catches what the drafting collaborator can't — it was in the room when the assumptions got made. Fresh eyes find where a neutral reader bounces.
6. **You read it out loud.** Any sentence that feels wrong coming out of your mouth gets cut or rewritten.

Raw-first, always. A draft that sounds like you talking at a bar is right. A draft that reads like a finished article is too polished.

## The Writer/Critic Architecture

Two agents with deliberately conflicting jobs:

- **The writer** (the drafting collaborator in `/draft` and `/flywheel`) is constrained by your voice guide and builds from your actual phrases. It's biased toward you by design — it heard the riff, knows the projects, holds the context.
- **The critic** (the `critical-reviewer` agent) runs as an isolated subagent with none of that context. It can't be charmed by the backstory because it never heard it. It answers one question: would a stranger keep reading?

They will conflict. That's the point — a critic that never disagrees with the writer isn't reading hard enough. The conflicts resolve by rule, not by whoever spoke last:

1. **The critic is advisory, not binding.** Applied mechanically, its feedback would converge every draft on the same neutral competence — the exact failure the system exists to prevent.
2. **Source phrasings are protected.** Your actual words from the riff are load-bearing. The critic can flag that they lose a stranger; the fix is grounding around them, never replacing them with cleaner ones.
3. **Tic-density zero is the failure mode.** If revision strips every casual marker and rough edge, the critic won and the writing lost.
4. **Jurisdiction splits the vote.** The critic wins on comprehension and structure. The voice guide wins on style and register. When a flag lands in both territories, fix the comprehension problem *in the voice*.
5. **You are the court of last resort.** The read-aloud test settles anything still contested. If the line feels wrong in your mouth, the critic's version dies, however correct it was.

The full rules live in the `writing-process` skill; `/flywheel` applies them automatically to every batch.

## Configuration

`/setup` creates a `config.json` in your project root:

```json
{
  "voice_observation_mode": "always-on",
  "default_platform": null,
  "tinkering_log": "~/.claude/tinkering.md",
  "publishing": {
    "target": null
  },
  "directories": {
    "drafts": "writings/drafts",
    "ready": "writings/ready",
    "published": "writings/published",
    "posts": "writings/posts",
    "posts_published": "writings/posts/published",
    "takes": "writings/takes",
    "planning": "planning",
    "voice_guide": "writings/voice-guide.md",
    "format_guides": "writings"
  }
}
```

- **`voice_observation_mode`**: `"always-on"` observes voice patterns during any command and flags updates. `"wrap-only"` saves voice observation for `/wrap` sessions only.
- **`default_platform`**: Set to `"linkedin"`, `"substack"`, etc. to skip the platform prompt. `null` means always ask.
- **`tinkering_log`**: Where the tinkering skill appends entries. Global by default so capture works from any project.
- **`publishing.target`**: `null` (default) stages finished flywheel posts in a folder for manual publishing. `"typefully"` pushes them to Typefully as drafts — credentials go in a `.env` file (`TYPEFULLY_API_KEY`, `TYPEFULLY_SOCIAL_SET_ID`), never in config.
- **`directories`**: All paths relative to project root. Customize to match your workspace structure.

## File Structure

```
voice-first-writing/
├── .claude-plugin/plugin.json
├── .gitignore
├── CLAUDE.md
├── LICENSE
├── README.md
├── config.template.json
├── agents/
│   └── critical-reviewer.md
├── commands/
│   ├── setup.md
│   ├── interview.md
│   ├── quickstart.md
│   ├── draft.md
│   ├── flywheel.md
│   ├── take.md
│   ├── derive.md
│   ├── review.md
│   ├── critical-review.md
│   ├── resume.md
│   ├── newsletter.md
│   ├── publish.md
│   ├── wrap.md
│   └── formatguide.md
└── skills/
    ├── writing-process/
    │   └── SKILL.md
    ├── voice-observation/
    │   └── SKILL.md
    └── tinkering/
        └── SKILL.md
```

## How It Works

The system solves a specific problem: AI-assisted writing drifts toward the AI's voice. The back-and-forth process (AI drafts, human edits) produces content that's competent and readable but could have been written by anyone. The rough edges, specific cadence, moments of uncertainty and sudden clarity get smoothed out.

The fix isn't better prompts. It's a different process.

Instead of generating text and injecting personality, the system captures your natural voice first and constrains the AI to it. The drift countermeasures, in the order they fire:

1. **The voice guide is built from observation, not self-description.** People are bad at describing how they sound. The capture interviews get you talking and read the patterns directly — sentence rhythm, hedging habits, escalation triggers, verbal tics, what you never say.
2. **The writer is constrained, not prompted.** Drafts must be built from your actual phrases at an agreed energy level, with an anti-pattern kill list (em-dashes, throat-clearing, the "It's not X. It's Y." reframe) enforced at draft time.
3. **Texture is protected during revision.** The writer/critic rules above stop the review pass from sanding the voice off — the most common drift vector isn't the first draft, it's the third revision.
4. **The read-aloud gate.** The final filter is human and physical: any sentence that feels wrong coming out of your mouth gets cut. This catches AI smoothing that editing misses.
5. **The guide is living.** Every session can flag new patterns and anti-patterns; the documentation gets more precise with use. Drift is corrected continuously instead of accumulating.

Over time, the system gets better. Not because the AI learns (it doesn't carry memory between sessions), but because the documentation gets more precise with every interaction.

## The Self-Updating System

- **Voice guide**: Updated when new patterns are observed, when drift is detected, when anti-patterns emerge.
- **Format guides**: Refined through actual use in drafting and derivation.
- **Interest map and platform strategy**: The flywheel refreshes the interest map every cycle; the strategy doc evolves as your platforms do.
- **Session summaries**: Capture decisions, observations, and what's queued for next time.

The AI flags potential updates during sessions. You approve or reject. Nothing changes without your say.
