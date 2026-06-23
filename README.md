# HugoBlox

**Quality game-building skills for Roblox, as a Claude Code plugin.**

HugoBlox is a set of [Claude Code](https://claude.com/claude-code) skills that build **good-looking, well-designed Roblox games from a simple prompt** — without the generic "AI-slop" look. You type something like `/hugoblox:horror-map`, Claude asks what you want, and then builds it in your open Roblox Studio.

## Why

Roblox Studio now ships a first-party AI assistant and an official MCP server that can already do the heavy lifting (run code, generate meshes/materials, search assets). What it does *not* do well is **taste** — results tend to look generic and templated.

HugoBlox is the missing **quality layer**: per-genre design knowledge + an anti-AI-slop checklist + a build recipe, so the output feels intentional, not auto-generated.

```
You (a prompt in Claude Code)
   → Claude  (the brain)
   → official "Roblox Studio" MCP  (the hands: execute code, generate, search assets)
   → HugoBlox skills  (the taste: how to make it actually good)
   → your open Roblox Studio
```

No API keys required — Claude Code is the brain.

## Requirements

1. **Roblox Studio** with the MCP server enabled: *Studio → Assistant → MCP Servers → "Enable Studio as MCP server"*, then connect it to Claude Code via Quick Connect.
2. **Claude Code** with the official `Roblox_Studio` MCP connected (the skills call its tools).
3. This plugin installed (below).

## Install

```text
/plugin marketplace add <path-or-repo-of-this-folder>
/plugin install hugoblox@hugoblox
/reload-plugins
```

After updating skills, bump the version in `.claude-plugin/plugin.json`, then update the plugin and run `/reload-plugins`.

## Usage

Open Roblox Studio on a test place, then in Claude Code run any skill, e.g.:

```text
/hugoblox:horror-map
/hugoblox:backrooms
/hugoblox:obby
```

Every skill **asks what you want first** (already have an idea / a theme / brainstorm / surprise me / just testing / plan first), then builds and **self-reviews with screenshots** before calling it done.

## Skills

**Game modes**

| Skill | Builds |
|---|---|
| `horror-map` | Horror map section with real atmosphere |
| `backrooms` | Liminal, endless, sickly-fluorescent space |
| `obby` | Fair obstacle course with checkpoints |
| `tycoon` | Buy → produce → grow money loop |
| `simulator` | Collect/grind loop, zones, pets (incl. brainrot) |
| `shooter` | Combat map with real flow (+ optional shooting) |
| `tower-defense` | Waves down a path, towers with roles |
| `survival` | Gather/craft/survive with tension-and-relief |
| `racing` | Track with a real layout, laps, checkpoints |
| `roleplay-town` | A town/city that feels lived-in |
| `escape-room` | Fair, chained puzzles |

**Systems (drop into any game)**

| Skill | Adds |
|---|---|
| `game-ui` | HUD/menus/shops/dialogs that don't look generic |
| `key-door-monster` | Objective loop: keys, doors, threat, goal |
| `npc` | NPCs with believable behavior |

Shared knowledge the skills follow lives in [`knowledge/`](knowledge/) (`anti-ai-slop.md`, `intake.md`).

## Status

Early / in active development. The architecture and skill recipes are in place; not every skill has been battle-tested in Studio yet. Feedback and contributions welcome.

## License

MIT — see [LICENSE](LICENSE).
