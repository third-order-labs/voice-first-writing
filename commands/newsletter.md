---
description: Generate a periodic newsletter — a curated roundup, one deeper insight piece, and a build-in-public note, assembled from what you published and built
argument-hint: "[period — e.g. 'march', '2026-03', 'march-april'; defaults to the previous month]"
---

# /newsletter — Periodic Newsletter

**Config**: This command reads directory paths from `config.json`. Falls back to defaults if config is missing.

**Skills Referenced**: writing-process

**Agents Referenced**: critical-reviewer

Generate a newsletter for a period. Semi-automated: the curation sections draft from existing data; the insight section uses a riff process with the user. That split is the design — full automation produces an AI digest nobody subscribes to.

## Arguments

- `/newsletter` — defaults to the previous calendar month
- `/newsletter march` or `/newsletter 2026-03` — specific month
- `/newsletter march-april` — multi-month range

## Before anything else

Read (non-negotiable):
1. The voice guide (path from `config.json`)
2. The format guide for the newsletter's platform, if one exists
3. `planning/content-backlog.md` — active threads and published work
4. `planning/interest-map.md` — what the user is building and thinking about (this also defines the newsletter's domain: the roundup covers *the user's* corner of the world, whatever that is)
5. `planning/platform-strategy.md` — if it defines a newsletter section mix, it overrides the default structure below

If the interest map or strategy doc doesn't exist (setup Step 5 is skippable), don't block: ask the user to describe their domain and what they've been building in a couple of sentences, use that in place of the missing docs, and suggest running `/setup` afterward to make it permanent. Without a strategy doc there is no scan list — so skip the project scan in Step 1 rather than guessing, and treat the never-scan rule as "nothing identifying clients or employers, ever."

## Default structure

Three sections, each with a distinct purpose and voice register. The strategy doc can override this mix; absent that, this is the shape:

### Section 1: The Roundup
**What it is:** A curated summary of what happened in the user's domain this period that they found interesting, interleaved with what they published. Not a link dump. A narrative tour of the period.

**Voice:** Casual curator. "Here's what caught my attention and why." Energy 2.

**Sources:** published content from the period, flywheel research archives (`planning/flywheel-research-*.md`), and a supplemental web search for major developments the flywheel missed.

**Structure:** 3-5 highlights from the broader domain; for each, 1-2 sentences on what happened and 1 sentence on why it matters or what the user thinks. Weave in the user's own published posts where relevant — as continuity, not self-promotion. Scannable. 200-300 words max.

### Section 2: The Insight
**What it is:** One deeper observation or argument. The piece that justifies the newsletter existing beyond curation. The section that makes someone think "I should keep subscribing."

**Voice:** Same as a long-form post. Reflective, experience-driven, earns the claim. Energy 2-3.

**Process:** Requires a riff with the user. Do NOT fully automate this — it's the human-in-the-loop piece that keeps the newsletter from reading like a generated digest.

1. Present 2-3 candidate topics: a post from the period that resonated and deserves more room, a trend across the period's research or published content, an unresolved backlog thread, or a question surfaced by the project scan.
2. The user picks one or proposes something different.
3. Quick riff — 3-5 questions, not a full `/draft` session. Enough to get the user's actual language and thinking into the piece.
4. Draft 300-500 words constrained by the voice guide and the riff language.
5. The user reviews and edits.

### Section 3: Note from the Trenches
**What it is:** What the user has been building. Build-in-public energy. Casual, specific, honest about what's working and what isn't.

**Voice:** "Here's what I've been up to." Energy 2. Uncertainty, half-finished things, and experiments all belong.

**Sources:** the project scan (per the strategy doc's scan list), new projects or experiments started during the period, system/tooling changes. Professional work in general themes only — the strategy doc's never-scan list applies absolutely, and nothing identifying clients or employers appears even obliquely.

**Structure:** 2-4 project updates — what changed, what's new, what surprised them. Honest about status ("Still early." "This broke." "Not sure where this is going." All valid). 150-250 words.

## Step 1: Gather Data

1. **Published content for the period** — scan the published directories for everything dated within the period; list with 1-line summaries.
2. **Research archives** — read `planning/flywheel-research-*.md` files from the period; note the most interesting unused findings.
3. **Project scan** — same as flywheel Step 1d: the strategy doc's scan list only, never-scan list absolute. Focus on what changed during the period.
4. **Supplemental web search** — major developments in the user's domain during the period that the archives missed. 5-8 items max.
5. **Compile a briefing** for the user: what you published, what happened in the domain, what you were building, and 2-3 insight candidates.

## Step 2: Riff on the Insight

Present the candidates. The user picks (or proposes something else). Then riff:
- "What's the thing about this that you keep coming back to?"
- "Who needs to hear this and what are they getting wrong?"
- "How does this connect to what you're building?"

3-5 questions. Not a full `/draft` session.

## Step 3: Draft

Draft all sections in a single document:

```
# [Newsletter Title]

**Period**: [Month Year]
**Status**: Draft
**Platform**: [newsletter platform / TBD]

---

## The Roundup

[Section 1]

---

## [Insight Title]

[Section 2]

---

## From the Trenches

[Section 3]
```

**Drafting rules (all sections):**
- Voice guide constraints apply throughout
- No em-dashes. No throat-clearing. No ChatGPT reframes.
- The newsletter should read like one person wrote all three sections (because one person did). Consistent register throughout.
- Section transitions should feel natural, not segmented.

**Section-specific rules:**
- **Roundup:** Scannable. Short paragraphs. Don't over-explain.
- **Insight:** Raw-first, same as `/draft`. Should read like the user thinking on the page, not a polished essay.
- **Trenches:** Build-in-public honesty. Not a highlight reel. Include the messy parts.

Save to the drafts directory (from `config.json`, default: `writings/drafts/`) as `YYYY-MM_newsletter-[month].md`.

## Step 4: Critical Review

Run the `critical-reviewer` agent on the full newsletter:

> Review the draft newsletter at [file path]. This is a periodic newsletter with three sections: a roundup (curated highlights), an insight piece (deeper argument), and a build-in-public update. Review as a subscriber who chose to read this. Focus on: would they finish all three sections? Does each section earn its space? Does the insight section sound like a real person with experience? Does the roundup add value beyond what they could find themselves? Also read the voice guide.

The writer/critic conflict rules from the writing-process skill apply. Common newsletter issues:
- **Roundup too long.** Scannable, not exhaustive. Cut the weakest items.
- **Insight too safe.** If the reviewer says "reasonable but not memorable," push the user for a sharper angle.
- **Trenches too polished.** If it reads like a project status report, roughen it up.

## Step 5: The User Reviews

Not optional. The newsletter has the user's name on it and includes riff content. They read the full draft, edit the insight section, approve. Move to the ready directory (from `config.json`, default: `writings/ready/`) when approved.

## Step 6: Publish

Platform-dependent — most newsletter platforms (LinkedIn newsletters, Substack, Buttondown) want content pasted into their own tool, so publishing is typically manual. Note the platform and date in the file metadata when published, and move to the published directory (from `config.json`, default: `writings/published/`).

## Important notes

- Don't force a newsletter if the period was thin. Skip or do a lighter version. Cadence pressure produces filler.
- The insight section is the reason people subscribe. Protect it.
- The never-scan list is absolute, and the trenches section mentions professional work in general terms only — no client or employer specifics, ever.
- The roundup references the user's published posts but must not read as a "here's everything I wrote" recap. It's "here's what happened" with the user's posts woven in as their contributions to the conversation.
- The newsletter compounds over time. Early issues establish the format. Consistency matters more than perfection.
