# Tabletop Designer

A Claude Code plugin that adds `game-designer`, a subagent specialized in designing and balancing card and board games.

## What it's for

Invoke it whenever you're working on tabletop/card game design:

- Inventing a new game from a concept (theme, player count, target feeling)
- Balancing an existing card set or in-game economy
- Auditing a ruleset for dominant strategies, runaway-leader problems, or kingmaker risk
- Drafting or reviewing rules text for clarity and teachability
- Structuring a playtest and interpreting the results
- Reviewing game-content data (card JSON, spreadsheets, design docs) already in your project

It brings a structured process (core loop → central decision → economy → interaction model → content → rules text), concrete math (expected value, cost curves, escalating-returns checks), and a checklist of common tabletop design failure modes (analysis paralysis, feel-bad hidden traps, snowballing, kingmaker exposure).

## Usage

Once installed and enabled, invoke it explicitly:

```
@tabletop-designer:game-designer review the balance of the card set in lib/content/data/items.json
```

or let Claude Code invoke it automatically — its description is written so Claude reaches for it whenever the task is tabletop/card game design, even without an explicit @-mention.

## Install

From a Claude Code session, with this repo cloned or referenced by URL:

```
/plugin marketplace add <path-or-git-url-to-this-repo>
/plugin install tabletop-designer@tabletop-designer-marketplace
/reload-plugins
```

See the repo root [README](../../README.md) for marketplace-level details.
