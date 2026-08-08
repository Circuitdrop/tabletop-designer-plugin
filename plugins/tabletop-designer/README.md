# Tabletop Designer

A Claude Code plugin for designing and building card and board games. It has two parts:

- **`game-designer`** — a subagent specialized in designing and balancing card and board games.
- **`game-code-reviewer`** + the **game-code-review-loop** skill — an iterative second-opinion review process for code changes to a game's engine/logic, so bugs and mistakes get caught and fixed before a change is considered done, not just designed well.

## What it's for

**Design work** — invoke `game-designer` whenever you're working on tabletop/card game design:

- Inventing a new game from a concept (theme, player count, target feeling)
- Balancing an existing card set or in-game economy
- Auditing a ruleset for dominant strategies, runaway-leader problems, or kingmaker risk
- Drafting or reviewing rules text for clarity and teachability
- Structuring a playtest and interpreting the results
- Reviewing game-content data (card JSON, spreadsheets, design docs) already in your project

It brings a structured process (core loop → central decision → economy → interaction model → content → rules text), concrete math (expected value, cost curves, escalating-returns checks), and a checklist of common tabletop design failure modes (analysis paralysis, feel-bad hidden traps, snowballing, kingmaker exposure).

**Code changes** — the `game-code-review-loop` skill fires automatically (no invocation needed) whenever Claude finishes editing a game's engine, rules, state-management, or API/content-loading code. It spawns `game-code-reviewer` to check the change for bugs, edge cases, inefficiencies, and mismatches with the intended rules; Claude applies any real findings and re-runs the reviewer, looping until the reviewer reports the change clean. It skips pure content/data edits (a JSON stat tweak, a new card added via an existing schema) unless asked to review those too.

## Usage

Once installed and enabled, invoke the designer explicitly:

```
@tabletop-designer:game-designer review the balance of the card set in lib/content/data/items.json
```

or let Claude Code invoke it automatically — its description is written so Claude reaches for it whenever the task is tabletop/card game design, even without an explicit @-mention.

The code-review loop needs no invocation at all — it's a skill, so Claude reaches for it on its own after game-logic code changes. You can also trigger it explicitly:

```
@tabletop-designer:game-code-reviewer check the changes I just made to lib/engine/heist.ts for bugs
```

## Install

From a Claude Code session, with this repo cloned or referenced by URL:

```
/plugin marketplace add <path-or-git-url-to-this-repo>
/plugin install tabletop-designer@tabletop-designer-marketplace
/reload-plugins
```

See the repo root [README](../../README.md) for marketplace-level details.
