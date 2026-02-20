---
description: Publish articles or posts — move to published, update tracking docs
argument-hint: "<filename, 'list', or 'posts' to publish derived posts>"
---

# /publish — Publish Content

**Config**: This command reads directory paths from `config.json`. Falls back to defaults if config is missing.

Handles two workflows:
- **Articles**: Move from the ready directory to the published directory (full ceremony)
- **Posts**: Move from the posts directory to the posts/published subdirectory (lighter, supports bulk)

## Before starting

Check that these exist (paths from `config.json`):
- The ready directory (default: `writings/ready/`)
- The posts directory (default: `writings/posts/`)
- The content backlog (default: `planning/content-backlog.md`) — if missing, skip the backlog update step and note: "No content backlog found. Create one to track published work, or run `/setup` for full workspace configuration."
- The content roadmap (default: `planning/content-roadmap.md`) — if missing, skip the roadmap update step.

Proceed with whatever steps are possible. Publishing should never be blocked by missing tracking docs.

## Routing

- **Argument is `posts`**: Go to Post Publish Workflow below.
- **Argument is a filename in the posts directory**: Go to Post Publish Workflow for that single file.
- **Argument is `list` or not provided**: List all files in the ready directory. If empty, check the posts directory for unpublished posts and mention those. Let the user choose.
- **Argument is a filename in the ready directory**: Go to Article Publish Workflow.

## Article Publish Workflow

1. **Confirm the piece**: Show the filename and title. Ask the user to confirm, and ask:
   - What platform was it published on? (LinkedIn post, LinkedIn article, Substack)
   - What's the actual publish date? (may differ from the draft date)
   - Any last-second title change?

2. **Move the file**: Move from the ready directory to the published directory. Update the date prefix in the filename to the actual publish date if it changed. Update the Status in the metadata.

3. **Update content backlog** (path from `config.json`, default: `planning/content-backlog.md`):
   - Add the piece to the Published Work section under the correct platform
   - Format: `"Title" (YYYY-MM-DD) — brief description`
   - Note which threads it develops (reference the Active Threads by number)

4. **Update content roadmap** (path from `config.json`, default: `planning/content-roadmap.md`):
   - If this piece was on the roadmap or evergreen queue, mark it as published
   - Update status in the relevant table or wave section

5. **Confirm**: Show the user what was updated.

## Post Publish Workflow

Lighter weight. Supports bulk.

1. **Show available posts**: List all files in the posts directory that don't have `Status: posted` or `Status: scheduled`. Show filename, title, source article, and current status for each.

2. **Confirm scope**: Ask the user which posts to publish:
   - "All of them" — bulk publish everything shown
   - Specific filenames — publish only those
   - If a single file was passed as argument, confirm just that one

3. **Ask once for the batch** (not per-post):
   - What platform? (default: LinkedIn, since most derived posts target it)
   - Publish date? (default: today)

4. **For each confirmed post**:
   - Create a `published/` subdirectory inside the posts directory if it doesn't exist
   - Move the file from the posts directory to the posts `published/` subdirectory
   - Update the date prefix in the filename to the publish date if it changed
   - Update the Status in the metadata to `posted`

5. **Update content backlog** (path from `config.json`, default: `planning/content-backlog.md`):
   - Add all published posts to the Published Work section under the correct platform
   - Format: `"Title" (YYYY-MM-DD) — derived from [source article]`

6. **Confirm**: Show the user the full list of what moved and what was updated. Keep it brief.
