# mentor-plugin

A Claude Code plugin that turns Claude into a Socratic mentor for learning projects.

Instead of handing you answers, Claude will guide you with questions, hints, and explanations — building understanding rather than dependency. At the end of every session it writes a structured learning recap to your Obsidian vault automatically, even if the session ends unexpectedly.

> **Always on.** Once installed in a project, mentor mode is active for every message in that project. Claude will never hand you solutions — it will guide you to find them yourself.

## Install

Install into a project you are using for learning purposes. Mentor mode is scoped to that project — Claude behaves normally everywhere else.

```
/plugin install github:valex91/mentor-plugin
```

**Requirement:** `python3` must be available on your `$PATH` (used by the session-end hook to parse JSON).

## Usage

No invocation needed — mentor mode activates automatically. Just start working.

Tip: tell Claude your background at the start of a session so it can bridge concepts more effectively:

```
I'm learning Go, coming from TypeScript.
```

### Obsidian vault (optional)

At the start of every session Claude will ask:

> "Do you have an Obsidian vault you'd like me to write your session recaps to?"

Paste the absolute path to your vault folder (e.g. `/home/you/MyVault`) or say `skip`. If you provide a path, Claude immediately:

1. Saves the vault path and topic to `~/.claude/mentor-config.json`
2. Creates a draft recap at `~/.claude/mentor-session-draft.md`

From that point on, the draft is updated silently in the background after every significant moment — error caught, hard point flagged, win noted, reading recommendation made. You never need to explicitly close the session for the recap to be saved.

When the session ends — for **any** reason (graceful close, crash, `Ctrl+C`, tab close) — a `SessionEnd` hook automatically moves the draft to:

```
<your-vault>/Learning Recaps/YYYY-MM-DD <topic>.md
```

If a file for today already exists (e.g. two sessions in one day), the new recap is appended with a separator. If the session ended unexpectedly, the file is stamped with a note so you know to review it.

## What it does

**Mentoring**
- Never gives direct solutions — guides with questions and hints
- Asks what you've already tried before correcting
- Explains the *why* behind corrections, not just the *what*
- Bridges new concepts from your existing language knowledge
- Flags repeated mistakes explicitly after the second occurrence

**Learning material**
- Surfaces canonical reading inline whenever a concept trips you up more than once or your mental model is off
- Recommends official docs first, then well-regarded books or interactive resources
- Points to the exact section or chapter — not just a homepage

**Session recap (written to Obsidian)**
- What was worked on
- Errors & misconceptions — root cause and how each was resolved
- Wins
- Concepts to revisit (with reason why)
- Suggested reading — mapped to the hard points from the session
- Next steps
- Mentor notes — a short observation on your learning pattern for the session

## Requirements

- Claude Code with plugin support
- `python3` on `$PATH`
- An Obsidian vault (optional, but recommended)

## License

MIT
