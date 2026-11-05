# Story Writing Workflow

This repo includes a structured story-writing workflow under `story/`, used to draft chapters iteratively across sessions.

- **Source of Truth:** `story/docs/story-bible.md` holds all character profiles, world-building, traits, and overall chapter outlines. `story/docs/handoff-state.md` tracks the current story state, recent plot changes, and immediate handoff notes for the next chapter.
- **Pre-Writing Rule:** Before drafting or editing any chapter, ALWAYS read both `story/docs/story-bible.md` and `story/docs/handoff-state.md`, as well as the most recent chapter in `story/chapters/` (if one exists), to maintain tone, pacing, and continuity.
- **State Protection Rule:** Do NOT modify `story-bible.md` or `handoff-state.md` while actively brainstorming or drafting a chapter unless explicitly asked to, or when the `/sync-state` command is run.

## Custom commands
- `/write-chapter <number>` — drafts or revises the given chapter using the story bible and handoff notes, saves it to `story/chapters/chapter-NN.md`.
- `/sync-state` — the only routine way `story-bible.md` and `handoff-state.md` should be updated; syncs them with what's happened in recent chapters/sessions.
