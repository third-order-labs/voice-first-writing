---
description: Run the content flywheel — generate a cycle of platform posts from web research intersected with what you've actually been building
argument-hint: "[platform name, or 'all' for every platform in your strategy]"
---

# /flywheel — The Content Flywheel

**Config**: This command reads directory paths from `config.json`. Falls back to defaults if config is missing.

**Skills Referenced**: writing-process, tinkering

**Agents Referenced**: critical-reviewer

Generate a cycle's worth of content from web research intersected with the user's current projects and interests. Produces draft posts, runs critical review on each, and stages them for publishing.

The flywheel supplements the manual `/draft` process, it doesn't replace it. Deeper pieces still go through the full riff → pull → confirm → draft → critical review → read aloud pipeline.

## The strategy doc is the contract

This command is the **engine**. What it produces is governed by the user's **platform strategy doc** at `planning/platform-strategy.md` (path from `config.json` under `directories.planning`). The strategy doc defines, per platform:

- **Intent** — what the platform is for (credibility, reach, community, a professional funnel)
- **Audience** — who actually reads it, described concretely
- **Cadence** — how many posts per cycle
- **Register mix** — the kinds of posts and the ratio between them
- **Rules** — platform-specific drafting constraints (length, openings, endings, whether sources get named, whether professional positioning is allowed)
- **Project scan config** — which project directories to scan for recent activity, and which are NEVER scanned (client work, private repos)

If the strategy doc doesn't exist, stop and say so: "The flywheel needs `planning/platform-strategy.md`. Run `/setup` (or just tell me about your platforms and I'll scaffold it)." Don't guess a strategy. A flywheel with no strategy produces generic content in nobody's voice for nobody's audience.

## Arguments

- `/flywheel` — run for the default platform (first platform in the strategy doc)
- `/flywheel <platform>` — run for a named platform
- `/flywheel all` — run every platform in the strategy doc as separate batches in one session. They share the interest map and research but produce different content. Don't reformat one platform's posts for another; they're different content for different audiences.

## Before anything else

Read (non-negotiable):
1. The voice guide (path from `config.json`, default: `writings/voice-guide.md`)
2. The format guide for each target platform (from the format guides directory)
3. `planning/platform-strategy.md` — the strategy contract
4. `planning/interest-map.md` — current interest map (search fuel + thread freshness). If it doesn't exist yet, Step 1 creates it.
5. `planning/content-backlog.md` — active threads and published work reference

If publishing is configured (see Step 6), read the required environment variables from `.env` at the workspace root.

## Step 1: Update the Interest Map

The interest map should reflect what the user is working on *right now*, not last cycle.

### 1a. Tinkering log (primary signal)

Read the tinkering log (path from `config.json` under `tinkering_log`, default: `~/.claude/tinkering.md`) for entries from the last 2 weeks. This is the highest-fidelity signal for what the user has actually been working on, because it's captured in-session with full context. Work that never made it into a git commit (exploration, prototyping, dead ends worth writing about) shows up here.

If the tinkering log doesn't exist or has no recent entries, note that and rely more heavily on the check-in and project scan.

### 1b. Quick check-in (required)

Ask the user 2-3 quick questions:
- "What have you been working on this week?"
- "Anything surprise you or piss you off?"
- "Any experiments or rabbit holes?"

This is NOT optional. The tinkering log and project scan capture what happened mechanically. The check-in captures what's on the user's mind, which is often different. If the user passes ("nothing to add" / "just run it"), that's fine, but always ask.

### 1c. Session summaries

Scan `planning/session-summary-*.md` for summaries from the last 2 weeks. These capture drafting and planning work inside this workspace. Cross-reference with the tinkering log for activity in other projects.

### 1d. Project scan

The strategy doc lists the project directories to scan. For each:
- `git log --oneline --since="2 weeks ago"` (if it's a git repo)
- Note active branches
- Read the README or CLAUDE.md first 30 lines for context (only if not already captured in the interest map)

For large repos, only scan git activity — don't read source code.

**Respect the never-scan list absolutely.** Directories the strategy doc marks as off-limits (client work, employer code, private material) must not be read, referenced, or pulled from under any circumstances, and nothing from them may appear in content — not even obliquely.

### 1e. Recent content check

Scan the published directory for anything from the last 2 weeks. Note themes to avoid repeating and angles that are getting stale.

### 1f. Update the interest map

Rewrite `planning/interest-map.md` with:
- Updated "Currently Building" section from the scan
- Updated "Thread Freshness" based on recent published content
- Refreshed "Search Fuel" terms based on current activity
- Any new angles from the check-in

## Step 2: Web Research

Use web search to find 10-15 interesting pieces of discourse that intersect the interest map: posts and threads from builders (not influencers), blog posts and technical articles, news in the user's domain, newsletters from practitioners.

**Search strategy:**
- Use the "Search Fuel" terms from the interest map
- Prioritize terms connected to fresh, high-priority angles
- Mix core interests with adjacent/contrarian topics
- Look for things that connect to the user's current project activity

**For each piece found, capture:**
- Source URL
- Key claim or observation (1-2 sentences)
- Which interest map thread it connects to
- The connection to the user's work/experience — **this is critical; if there's no connection, skip it**

**Quality filter:**
- Skip hype and marketing
- Skip listicle content
- Skip anything the user has already covered (check recent published content)
- Prioritize pieces where the user has direct experience that adds to or contradicts the take

Save the research results to `planning/flywheel-research-YYYY-MM-DD.md` for reference. Unused strong finds are legitimate fuel for other platforms or future cycles — note them in the Step 7 summary rather than discarding them.

## Step 3: Select and Map

From the research, select the best candidates per the strategy doc's cadence and register mix.

### The portable observation gate

Every build-in-public candidate must pass this check before it gets through to drafting:

> **Would this still be interesting if you stripped the project context?**

The audience doesn't live inside the user's projects. "Built X this week" reads as out-of-nowhere unless the *interesting thing in the build* is portable. Builds are fuel for the observation. The observation is the headline.

- If the interesting thing only works inside one project's framing, kill the candidate.
- If there's a portable observation embedded — a tension, a generalizable insight, a moment that resonates without the project context — keep it and lead with that observation.
- "Built X this week" is the cost. The wrinkle in X is the headline.

**Exception: artifact posts.** When the strategy doc includes an artifact register — posts where a specific build IS the headline (an architectural choice, a tool that does something genuinely novel) — the gate relaxes. The post must still be legible to a stranger in 2 sentences, but it doesn't need to abstract away from the artifact.

### Cadence is sacred — derive when fuel is light

Don't skip a cycle when fuel is short.

- **Derivation pass:** When research + project scan don't yield enough portable observations to fill the cadence, extract a second angle from the strongest 1-2 sources. Same observation, different beats.
- **Upper bound:** at most one source generates 2 posts per cycle. Past that the feed starts repeating itself.
- **Standalone framing:** When two posts come from the same source, frame each so the reader can't tell. Different angles, different formats, scheduled apart.

### Selection

Apply the strategy doc's content mix and register mix rules for the target platform. Then for each selected piece, map out:
- The source observation/claim
- The user's experience that connects to it
- The angle
- Format (per the platform's format guide)
- Proposed energy level
- Which backlog thread it feeds

## Step 4: Draft

Write the posts constrained by three documents in this priority order: the voice guide (how the user sounds), the platform format guide (what the platform wants), and the strategy doc's per-register rules (what this kind of post does).

**Critical rules (same as /draft):**
- Posts should sound like the user talking, not the user reacting to an article
- No em-dashes. No throat-clearing. No ChatGPT reframes ("It's not X. It's Y.")
- One idea per post
- No calls to action, no engagement bait
- Endings: land on the insight or leave it open
- Source material is fuel, not subject: unless the register explicitly leads with a finding, the source stays invisible and the post is about the user's experience
- Scan each draft for inflection points; if it has zero of the user's verbal tics (per the voice guide), that's the personality-sanded-off pattern — put texture back in at the draft step, not the review step

**Metadata block for each post:**
```
# Title

**Platform**: [platform / format]
**Thread**: [from content backlog]
**Energy level**: [1-4]
**Status**: Flywheel draft
**Fuel**: [1 sentence on the source or project context, for the user's reference only]

---
```

Save to the published directory (from `config.json`) using `YYYY-MM-DD_short-title.md` (prefix with a platform tag if the strategy doc uses one). Flywheel files live in `published/` from creation; the **Status field carries the workflow state** (`Flywheel draft` → `Flywheel final` → `Published`) as the piece moves through review and staging.

## Step 5: Critical Review

For each draft, run the `critical-reviewer` agent:

> Review the draft post at [file path]. This is a flywheel-generated post (drafted from web research intersected with the author's experience) for [platform]. Energy level [X]. Review as a stranger would read it. Focus on: readability, impact, whether a neutral reader would finish it, and whether it sounds like a real person with experience versus someone reacting to an article they read. Also read the voice guide.

**Use the prompt as written. Do NOT expand it with anti-pattern checklists.** The reviewer is already calibrated to its job: stranger-readability, impact, would-they-finish. Over-prompting it with anti-pattern lists pushes it toward standard craft-critique defaults, which over-flag the user's actual voice patterns as anti-patterns. The drafting step carries the voice-compliance load. The review step is the stranger-reader pass, not voice police.

### Weighing the feedback

The writer/critic conflict rules from the writing-process skill apply in full:

- **The reviewer is advisory, not binding.** Apply when craft and voice agree. Override when they don't.
- **Source phrasings are protected.** When the user gave you a specific line during the check-in, the published piece should use that line. If the reviewer flags it as aphoristic or moralizing, it stays anyway. The rawer version sounds like the user; the paraphrase sounds like craft. Default to the user.
- **Tic preservation.** Sparse is the rule, zero is the failure mode. If a reviewed draft has zero verbal tics, adding 1-2 back is correction, not decoration.

### Flywheel-specific issues to fix when the reviewer raises them

- **Reactive tone.** Reads like "I saw this article and here's what I think" → rewrite to anchor in experience first.
- **Missing specificity.** Flywheel posts risk abstraction because they start from someone else's observation → add specific project details, moments, examples from the user's work.
- **Thread fatigue.** Sounds like something the user already said → kill it and draft a replacement from the research backlog.
- **Summary, not angle.** Reads like a summary of someone else's piece with no first-person ground → anchor it in what the user built or saw.

**Killing a piece:** If the verdict is fatal and a rewrite won't fix it, delete the file. Don't leave abandoned drafts in the published folder. Quality over quantity.

**Surviving review:** Update the Status field from `Flywheel draft` to `Flywheel final`.

## Step 6: Publish

Publishing is optional and configured in `config.json`:

```json
"publishing": {
  "target": "typefully"
}
```

**If `publishing.target` is unset or null:** the pipeline ends here. `Flywheel final` posts sit in the published directory as the staging queue; the user posts them manually. Say so in the summary. This is the default and it is not a degraded mode.

**If `publishing.target` is `"typefully"`:** push each `Flywheel final` post to Typefully as a draft (no scheduling — the user approves and schedules from the Typefully app). Credentials come from environment variables (via `.env` at the workspace root), never from config: `TYPEFULLY_API_KEY` and `TYPEFULLY_SOCIAL_SET_ID`.

```
POST https://api.typefully.com/v2/social-sets/{TYPEFULLY_SOCIAL_SET_ID}/drafts
Authorization: Bearer {TYPEFULLY_API_KEY}
Content-Type: application/json

{ "platforms": { "<platform-key>": { "enabled": true, "posts": [{"text": "POST CONTENT"}] } } }
```

Platform keys: `linkedin` for LinkedIn, `x` for Twitter/X. For threads, pass multiple `posts` entries. Strip markdown before pushing — plain text only.

**After a successful push:** update the post's Status from `Flywheel final` to `Published` (commitment to the queue, not confirmation it went live), and append a one-line entry to the content backlog's published section under the post's platform (format: `"Title" (YYYY-MM-DD) — brief description`). If the strategy doc defines its own tracking rules, those override this default.

**If a push fails:** leave Status as `Flywheel final`, don't update the backlog, and report the failure in the summary for manual retry.

## Step 7: Summary

Present the user with:
- Every post: title, platform, format, thread, energy level, fuel source, final Status
- Which interest map threads were covered, and which are still underserved
- Strong research finds that went unused (future fuel)
- Any observations worth noting (new angles, surprising findings)
- Any publish failures needing manual retry
- Where things stand: which folder the files are in, and where review/scheduling happens next

Save the summary to `planning/flywheel-summary-YYYY-MM-DD.md`.

## Important notes

- When in doubt about whether something sounds like the user, it probably doesn't. Cut it.
- Never-scan directories from the strategy doc are absolute. Nothing from them appears in content, ever.
- The Status field is the workflow state; the folder reflects commitment. Don't move flywheel files between folders to track state.
