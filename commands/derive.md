---
description: Derive 2-3 standalone platform posts from a finished article
argument-hint: "<path to article> [--oneshot] [--platform linkedin|substack|twitter|etc]"
---

# /derive — Article to Posts

**Config**: This command reads directory paths from `config.json`. Falls back to defaults if config is missing.

**Skills Referenced**: writing-process

Derive standalone platform posts from a finished article. Each post extracts one insight and stands on its own — not a summary, not a promo for the article.

## Setup

Read the voice guide and source article before doing anything:

1. Voice guide (path from `config.json`, default: `writings/voice-guide.md`)
2. The source article (path provided as argument)

If no article path is provided, check the ready and published directories (from `config.json`, defaults: `writings/ready/` and `writings/published/`) for the most recently modified article and confirm with the user.

**Determine platform**: Check if a `--platform [name]` flag was passed as an argument. If so, use that. Otherwise, check `config.json` for a `default_platform` value — if set (not null), use that as the default. If no flag and no config default, check the article's metadata for a **Platform** field and use that. If none of the above, ask the user which platform to derive for.

**Load format guide**: Once platform is determined, read the format guide for that platform (from the format guides directory in `config.json`, default: `writings/format-guide-[platform].md`). If no format guide exists for that platform, tell the user and suggest running `/formatguide [platform]` first. Proceed without a format guide only if the user explicitly says to.

## Default flow (propose first)

### 1. Identify extractable insights

Read the article and identify 2-3 insights that could stand alone as platform posts. For each one, provide:
- A one-line description of the insight
- Which part of the article it comes from
- Why it works as a standalone post

Refer to the format guide's "What makes a good extraction" criteria:
- The insight stands alone without the article's supporting argument
- It's specific enough to be interesting
- It has its own natural opening and landing
- It doesn't require context from the article to make sense
- It could plausibly be its own observation

Present these to the user and ask: "These three work? Cut any, redirect any, add any?"

### 2. The user confirms

Wait for confirmation. The user may:
- Approve all
- Cut one or more
- Redirect an insight to a different angle
- Add one they noticed that you missed

Adjust and proceed with the confirmed list.

### 3. Draft posts

For each confirmed insight, draft a post constrained by:
- The voice guide (how the user sounds)
- The format guide (platform post structure, length, opening, ending rules)
- The source article's language and energy (use the user's actual phrases where possible)

**Post rules:**
- Follow the platform format guide's structure, length, opening, and ending rules
- One idea per post
- Kill all AI anti-patterns from the voice guide
- If no format guide is loaded, use sensible defaults: 150-300 words, open with something specific, end on the insight or leave it open

**Energy calibration:**
- Don't auto-match the article's energy level. Each post finds its own level based on which insight it's carrying.
- Compression isn't escalation. Punchier does not mean hotter.

### 4. Save and present

Save each post to the posts directory (from `config.json`, default: `writings/posts/`) using this naming convention:
`YYYY-MM-DD_derived-short-title.md`

Include metadata at the top:

```
# Post Title

**Source**: [article filename]
**Insight**: [one-line description]
**Energy level**: [1-4]
**Status**: draft

---

[post content]
```

Present all posts in the conversation for the user to review. They'll skim, edit if needed, and post on their own schedule.

## Oneshot flow

If `--oneshot` is included in the arguments, skip the proposal step:

1. Read article, voice guide, format guide
2. Identify 2-3 insights and draft posts directly
3. Save to the posts directory
4. Present all posts for review

Same drafting rules, same quality bar. Just no confirmation step in between.

## What this is NOT

- Not a summarizer. Posts are not compressed versions of the article.
- Not a promo generator. No "I wrote about this" posts. No links to the article.
- Not the full writing process. No riffing, no multi-step drafting. The thinking already happened in the article.
- Not fire-and-forget. The user still reviews everything before posting.
