# tabletop-designer-plugin

A self-contained [Claude Code plugin marketplace](https://code.claude.com/docs/en/plugin-marketplaces) with one plugin: **tabletop-designer**, which adds a `game-designer` subagent — an expert at designing and balancing card and board games.

See [plugins/tabletop-designer/README.md](plugins/tabletop-designer/README.md) for what the agent does and how to invoke it.

## Try it locally (no install needed)

```bash
claude --plugin-dir ./plugins/tabletop-designer
```

Then in the session, either @-mention it or just ask a game-design question — its description is written so Claude reaches for it automatically:

```
@tabletop-designer:game-designer help me design a 3-5 player bluffing game about black-market smugglers
```

## Install for real (from this repo)

```
/plugin marketplace add /Users/loganadams/Downloads/tabletop-designer-plugin
/plugin install tabletop-designer@tabletop-designer-marketplace
/reload-plugins
```

Once you push this repo to GitHub (or another git host), replace the local path above with the repo URL so it can be shared with others:

```
/plugin marketplace add <your-org>/tabletop-designer-plugin
/plugin install tabletop-designer@tabletop-designer-marketplace
```

## Repo layout

```
tabletop-designer-plugin/
├── .claude-plugin/
│   └── marketplace.json          # lists the plugin(s) in this marketplace
├── plugins/
│   └── tabletop-designer/
│       ├── .claude-plugin/
│       │   └── plugin.json       # plugin manifest
│       ├── agents/
│       │   └── game-designer.md  # the subagent itself
│       └── README.md
└── README.md                     # this file
```

## Extending it

To add more to the plugin later — a `/tabletop-designer:balance-pass` skill, card-generation scripts, etc. — add `skills/` or `commands/` directories under `plugins/tabletop-designer/` per the [plugin structure reference](https://code.claude.com/docs/en/plugins-reference#plugin-directory-structure). To add a second plugin to this same marketplace, add another entry to `.claude-plugin/marketplace.json` and a matching directory under `plugins/`.
