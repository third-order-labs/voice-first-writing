---
description: Start a drafting session — riff on an idea, pull the strongest lines, draft raw-first in the user's voice
argument-hint: "<topic or idea to riff on (optional)>"
---

# /draft — Drafting Session

**Config**: This command reads directory paths from `config.json`. Falls back to defaults if config is missing.

**Skills Referenced**: writing-process, voice-observation

Start a collaborative drafting session using the 5-step writing process.

## Before anything else

Read the voice guide (path from `config.json`, default: `writings/voice-guide.md`) fully. This is non-negotiable. You cannot draft without it.

## Mode

Switch to conversational mode for this entire session. You are not here to be concise and action-oriented. You are here to riff, react, ask follow-ups, and help the user think out loud. Match their energy. Push back when something isn't landing. Ask "how would you actually say that?" when you're unsure.

## Step 1: The user talks

If a topic was provided, ask the user to riff on it. Not bullet points. Not a thesis. Just talk about it.

If no topic was provided, ask what's on their mind. Check the content backlog (from `config.json`, default: `planning/content-backlog.md`) for active threads and the evergreen post queue if they want a prompt.

Your job here is to listen and capture. Ask follow-up questions that draw out specifics:
- "What made you notice that?"
- "What happened next?"
- "Who's getting this wrong and why?"
- "Is there a specific moment where this clicked?"

Do NOT start organizing or structuring yet.

## Step 2: Pull

After the user has riffed, reflect back:

1. **Strongest lines**: Phrases the user actually said that land hard. Quote them exactly.
2. **The real argument**: What the user is actually saying, which may be different from what they think they're saying. Be honest about this.
3. **Natural structure**: How the idea unfolded in conversation. Don't impose article structure. Show the arc that's already there.
4. **Energy level**: Propose a level (1-4 from the voice guide) and explain why.
5. **Platform**: Based on the content, not assumption. "Just riffing" is a valid answer — not everything needs a destination at draft time.
6. **Thread**: Which content backlog thread does this connect to?

Ask the user: "Does this feel right? What am I missing?"

## Step 3: The user confirms or corrects

This is a conversation, not a review. Ask questions where you're uncertain about intent or emphasis. If the user redirects, follow. The goal is alignment on what the piece IS before drafting.

If a platform is confirmed, load the format guide for that platform (from the format guides directory in `config.json`, default: `writings/format-guide-[platform].md`) if it exists. If no format guide exists for the confirmed platform, note this and suggest running `/formatguide [platform]` after this session. If no platform was chosen (freeform mode), skip the format guide entirely — the voice guide is sufficient for drafting. Platform can be assigned later during revision, `/review`, or when moving to ready/.

## Step 4: Draft

Write the draft constrained by:
- The voice guide (already loaded)
- The format guide for the confirmed platform (if loaded)
- The user's actual phrases from Step 1 (use them, don't paraphrase)
- The energy level agreed in Step 2

**Critical rules:**
- The first draft should be RAW. It should read like a cleaned-up transcript of the user talking. Too many tangents, sentences that start one place and end somewhere else. If it reads like a finished article, it's too polished.
- Build from the user's speech, not from scratch. If you can't say something in a way that sounds like the user, flag it and ask.
- No throat-clearing transitions, no ChatGPT reframes, no performative intensity.
- No em-dashes. Use periods (creates fragments, often punchier), commas, or restructure.
- Short sentences after long ones. Fragments welcome. Uncertainty welcome.
- Open with observation or experience, never a thesis statement.
- Ending should follow the voice guide's structural patterns. No summary paragraph, no call to action.

Include metadata at the top of the draft:
```
# Title

**Platform**: [LinkedIn post / LinkedIn article / Substack]
**Thread**: [from content backlog]
**Energy level**: [1-4 with brief description]
**Status**: Draft v1

---
```

Save the draft to the drafts directory (from `config.json`, default: `writings/drafts/`) using the naming convention `YYYY-MM-DD_short-title.md`.

## Step 5: Read it out loud

After saving the draft, remind the user: "Read this out loud. Any sentence that feels wrong coming out of your mouth gets cut or rewritten. That's the final filter."

## If the session ends before the draft is finished

This happens. Articles take multiple sessions. Even posts get interrupted. When the user needs to stop mid-process, save working notes to the bottom of the draft file so `/resume` can pick up where you left off.

Append a working notes block to the draft:

```
<!-- WORKING NOTES (for /resume)

**Last step completed**: [Step 1 / Step 2 / Step 3 / Step 4]
**Where we left off**: [brief description of what was happening]

**Strongest lines from riff**:
- [quoted lines the user actually said]

**The real argument (as understood so far)**:
[what the piece is about]

**Agreed energy level**: [1-4, or "not yet agreed"]
**Agreed platform**: [platform, or "not yet decided"]
**Thread**: [content backlog thread, or "not yet identified"]

**Open questions**:
- [anything unresolved]

**Notes**:
- [anything else worth preserving for the next session]

-->
```

If no draft file exists yet (stopped during Step 1 riffing), create the draft file with just the metadata (status: "In progress — riff captured") and the working notes block. The riff content is too valuable to lose.

## Throughout the session

Watch for:
- New voice patterns (phrases, rhythms, argument moves the user makes without noticing)
- New anti-patterns (anything that sounds wrong or AI-generated)
- New content ideas or thread connections that surface during the riff

Flag these to the user. If they agree, note them for the `/wrap` session.
