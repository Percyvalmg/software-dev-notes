---
name: dev-notes-from-youtube
description: Turn a YouTube video into a clean, factual software-engineering note in this repo. Use when the user shares a YouTube link and wants a development note, or asks to add a note from a talk or video. Pulls the transcript, writes a readable Markdown note with diagrams, strips opinion and AI-writing patterns, and files it under the right category folder.
argument-hint: "Paste the YouTube link (and optionally the category folder)"
---

# Dev notes from YouTube

Create a software-engineering note in this repository from a YouTube video. The finished note captures the **factual, technical substance** of the video, reads like a person wrote it, and includes diagrams for anything hard to picture.

This repo is a personal dev-notes collection. Notes are grouped into category folders (for example `ai-engineering/`, `ci-cd/`), each with its own `README.md` index, and the root `README.md` lists every category.

## Workflow

### 1. Get the transcript

Use the YouTube transcript MCP server (`youtube_transcript`). If it isn't active, add it with the MCP tooling, then call:

- `get_video_info` — title, description, uploader, duration, and (often) chapter timecodes
- `get_transcript` — the full text

Keep the video title and URL; they go in the note's source line. If the transcript is paginated, follow `next_cursor` until you have all of it.

### 2. Pick the category folder

- If the user names a folder, use it.
- Otherwise infer it from the topic and check the root `README.md` for an existing fit.
- If no folder fits, create a new one: a short dash-case name, a `README.md` index inside it, and a new row in the root `README.md` category table.

### 3. Write the note

Save to `<category>/<dash-case-title>.md`. Match the style of existing notes in the repo (read one first).

Structure that works well:

- an H1 title, then a bold **Source:** line with a Markdown link to the video
- a short "core idea" section that frames the whole topic
- the body, organised by the video's own structure (its chapters or natural progression)
- a summary table when the video compares several things
- a short "key takeaways" list at the end

Rules for the content:

- keep the factual and technical material; drop the presenter's personal color (jokes, rants, catchphrases, "run away" style advice)
- when something is the presenter's opinion or recommendation rather than fact, say so ("the video recommends...") instead of stating it as absolute
- never invent facts, numbers, names, or claims the video didn't make
- prefer bullet points over long paragraphs, but keep a short lead-in sentence before each list so it doesn't read like a wall of bold labels

### 4. Add diagrams

Add ASCII diagrams (inside fenced code blocks) for anything a diagram explains better than prose: branch flows, pipelines, decision trees, architectures, state transitions, comparisons. Aim for clarity over decoration.

### 5. Humanize the prose

Run the note through the **humanizer** skill (`~/.claude/skills/humanizer/SKILL.md`) in file mode, or apply its rules directly. The ones that matter most here:

- no em or en dashes; use commas, colons, periods, or parentheses
- headings in sentence case, not Title Case
- plain verbs (`is`, `has`) over "serves as / boasts / represents"
- no forced groups of three, no vague-source phrases ("experts say"), no generic upbeat endings
- avoid bold mini-heading lists; use plain bullets with a lead-in sentence
- keep every claim intact while changing the wording

Leave code blocks, diagrams, tables, and link targets unchanged.

### 6. Update the indexes

- add a row for the new note in the category `README.md`
- if you created a new category, add it to the root `README.md`

Keep index descriptions factual and neutral, matching the tone of the note.

### 7. Verify before finishing

- the source link resolves to the right video
- every diagram renders and matches what the text says
- no em/en dashes remain
- the category and root indexes both point to the new file
- the note states the video's opinions as opinions, not facts

## Notes

- Default to acting: pull the transcript and draft the note rather than asking a series of setup questions. Only ask if the category is genuinely ambiguous.
- If the transcript is unavailable (no captions), tell the user rather than writing from guessed content.
