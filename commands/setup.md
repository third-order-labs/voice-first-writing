---
description: First-time setup — walk through workspace creation, voice capture, format guide, and orientation
---

# /setup — New User Onboarding

**Config**: This command reads directory paths from `config.json`. Falls back to defaults if config is missing.

**Skills Referenced**: voice-observation

Welcome sequence for someone using this system for the first time. Walks through the essential setup steps in order.

## What this does

Gets a new user from zero to ready-to-draft in one session (or across a few sessions). The things that need to exist before the drafting loop works:

1. A workspace directory structure (from `config.template.json`)
2. A `config.json` with user preferences
3. A voice guide
4. At least one format guide
5. An understanding of how the system works

## Step 1: Create workspace and configure

Read `config.template.json` to get the default directory structure. Create all directories listed under `directories` in the template.

Then prompt the user for preferences:

1. **Voice observation mode**: "Do you want voice observation always on, or only during /wrap?"
   - `"always-on"` = observe voice patterns during any command and flag new patterns as they surface
   - `"wrap-only"` = only check for new voice patterns during `/wrap`
2. **Default platform**: "Do you have a primary platform, or do you want to be asked each time?"
   - `null` = always ask which platform
   - A specific platform name (e.g., `"linkedin"`, `"substack"`) = use as default when no platform is specified

Write `config.json` to the project root with the user's choices and the default directory paths from the template.

## Step 2: Check current state

Before proceeding, check what already exists:
- Does the voice guide exist (path from `config.json`)? If yes, ask if they want to revise or skip.
- Do any format guides exist (path from `config.json`)? Note which platforms are covered.
- Does the content backlog exist (path from `config.json`, default: `planning/content-backlog.md`)?

Report what's in place and what's missing.

## Step 3: Voice capture

If no voice guide exists (or user wants to redo it):

Ask: "Do you want the quick version or the deep version? Quick gets us a working voice guide in about 10 minutes. Deep goes longer and produces a more nuanced guide."

- Quick: Run `/quickstart`
- Deep: Run `/interview`

If a voice guide already exists, skip to Step 4.

## Step 4: Format guide

If no format guides exist:

Ask: "What platform do you want to publish on first?" Then run `/formatguide [platform]`.

If format guides exist, ask if they want to add another platform or skip.

## Step 5: Orientation

Brief walkthrough of the system:

- **`/draft`** starts a writing session (the main creative workflow — riff on an idea, pull the strongest lines, draft in your voice)
- **`/derive`** creates platform posts from finished articles (lower effort, leverages the thinking already done in the article)
- **`/review`** checks a draft against your voice guide for consistency and anti-patterns
- **`/resume`** picks up an interrupted draft from where you left off
- **`/publish`** moves finished work through the pipeline and updates tracking docs
- **`/wrap`** closes out a session with documentation (like a save point between sessions)

Explain the pipeline: `drafts/` -> `ready/` -> `published/`

Explain that the voice guide is a living document that sharpens with every session. The more you write, the better the system gets at sounding like you.

## Step 6: First content (optional)

If there's time and energy, offer: "Want to try a quick draft to test the system? We can riff on something small to see how it feels."

If yes, run `/draft`.

## Important

Don't rush this. If the user only has time for the voice capture today, that's fine. The format guide and orientation can happen next session. The voice guide is the critical path — nothing works well without it.
