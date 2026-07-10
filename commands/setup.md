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
5. An interest map and platform strategy (what you build, what you care about, where it publishes)
6. An understanding of how the system works

## Step 1: Create workspace and configure

Read `config.template.json` to get the default directory structure. Create the workspace directories it defines: `writings/drafts`, `writings/ready`, `writings/published`, `writings/posts`, `writings/posts/published`, and `planning`. Note that two `directories` entries are NOT directories to create: `voice_guide` is a file path (the voice capture step writes it later) and `format_guides` names the parent directory format guides are written into. Don't `mkdir` those.

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
- Does the content backlog exist (in the planning directory from `config.json`: `planning/content-backlog.md`)?

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

## Step 5: Projects, interests, and platform strategy

This step seeds the content flywheel. Skippable ("we can do this later — `/flywheel` will ask for it"), but without it the system can only write when the user shows up with an idea; with it, the system can propose content from what the user is actually doing.

Interview conversationally — this is a conversation, not a form. Cover four areas:

1. **What are you building?** Current projects, side projects, experiments, work themes. For each: what it is in one sentence, and where it lives on disk if it's code (these become the flywheel's project scan list).
2. **What's off-limits?** Client work, employer code, anything private. This becomes the **never-scan list** — directories and topics that must never be read or referenced in content. Take this seriously and err toward exclusion: "if in doubt, leave it out" is the right default for someone's professional obligations.
3. **What do you keep coming back to?** Interests, opinions, recurring arguments, the topics they'd riff on unprompted. These become the initial threads and search fuel.
4. **Where does this go?** For each platform they publish on: what it's for (credibility, reach, community, professional positioning), who actually reads it there, how often they want to post, and what kinds of posts feel right. If they don't know yet, capture rough answers — the strategy doc is living, like the voice guide.

Then scaffold three documents in the planning directory (paths from `config.json`):

- **`planning/interest-map.md`** — sections: Currently Building (from area 1), Threads (from area 3), Search Fuel (terms the flywheel researches with), Thread Freshness (empty for now; the flywheel maintains it).
- **`planning/platform-strategy.md`** — one section per platform with: Intent, Audience, Cadence, Register mix, Rules, plus a top-level Project Scan section listing scan directories and the NEVER-SCAN list with a note that it is absolute. This doc is the flywheel's contract.
- **`planning/content-backlog.md`** — sections: Active Threads (seeded from area 3), Evergreen Queue (empty — ideas that aren't time-sensitive), Published Work (empty), In Progress (empty). If it already exists, leave it alone.

Finally, ask about publishing: "When the flywheel finishes a batch, do you want posts staged in a folder for you to publish manually, or pushed to a scheduling tool?" Manual staging is the default. If they use Typefully, set `publishing.target` to `"typefully"` in `config.json` and tell them to put `TYPEFULLY_API_KEY` and `TYPEFULLY_SOCIAL_SET_ID` in a `.env` file at the workspace root — credentials never go in `config.json`.

## Step 6: Orientation

Brief walkthrough of the system:

- **`/draft`** starts a writing session (the main creative workflow — riff on an idea, pull the strongest lines, draft in your voice)
- **`/flywheel`** generates a cycle of platform posts from web research intersected with what you've been building (reads the tinkering log + your platform strategy)
- **`tinkering`** captures what you just built, autonomously, wherever you're working — it's the flywheel's primary fuel; you mostly never invoke it, it fires itself
- **`/derive`** creates platform posts from finished articles (lower effort, leverages the thinking already done in the article)
- **`/review`** checks a draft against your voice guide for consistency and anti-patterns
- **`/critical-review`** reads a draft as a stranger would — readability and impact, not voice (a separate, isolated reviewer by design)
- **`/resume`** picks up an interrupted draft from where you left off
- **`/publish`** moves finished work through the pipeline and updates tracking docs
- **`/wrap`** closes out a session with documentation (like a save point between sessions)

Explain the pipeline: `drafts/` -> `ready/` -> `published/`

Explain that the voice guide, interest map, and platform strategy are living documents that sharpen with every session. The more you write, the better the system gets at sounding like you.

## Step 7: First content (optional)

If there's time and energy, offer: "Want to try a quick draft to test the system? We can riff on something small to see how it feels."

If yes, run `/draft`.

## Important

Don't rush this. If the user only has time for the voice capture today, that's fine. The format guide, strategy interview, and orientation can happen next session. The voice guide is the critical path — nothing works well without it. The platform strategy is the flywheel's critical path — `/flywheel` won't run without it, but everything else works fine.
