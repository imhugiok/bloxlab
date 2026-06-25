# Design notes — the quality layer

Internal rationale and dev notes. User-facing docs live in the [README](../README.md);
the quality bar itself lives in [`knowledge/anti-ai-slop.md`](../knowledge/anti-ai-slop.md).
This file only records the *why* behind the decisions, so they don't get re-litigated.

## The one decision that shapes everything

Roblox already ships a first-party AI assistant and an official `Roblox_Studio` MCP that
can run code, generate meshes/materials/3D models, and search assets. The generative parts
run in Roblox's cloud, so no third-party tool can beat them there.

So bloxlab does **not** rebuild the engine. Claude Code is the brain (free with the
subscription — no Anthropic API key), the official MCP is the hands, and our only value is
the **taste**: per-genre game-design knowledge + an anti-slop checklist + build recipes that
make the output look intentional instead of auto-generated. The moment we'd try to
reimplement generation or asset search, we'd be losing to Roblox's own cloud.

## Why a Claude Code plugin (and not a standalone tool)

- The brain and the hands already live inside Claude Code (the MCP is connected there).
- Skills are just Markdown recipes — easy to read, fork, and PR. Low barrier for contributors.
- `${CLAUDE_PLUGIN_ROOT}` lets every skill pull the shared `knowledge/` at run time, so the
  anti-slop layer stays in one place instead of being copy-pasted into 14 files.

## Dev notes (things that bite)

- **Installed plugins are a cached copy** — they do not auto-update. After editing skills:
  bump the version in `.claude-plugin/plugin.json`, then `/plugin` update + `/reload-plugins`.
- **To test a skill you don't need to install it** — follow its `SKILL.md` and drive the
  official MCP directly. (That's how every skill in this repo was battle-tested.)
- **`Lighting.Technology` can't be read or written** from the `execute_luau` sandbox
  ("lacking capability RobloxScript"). Wrap all Lighting writes in `pcall`. Light numbers are
  mood-dependent and must be calibrated empirically via `screen_capture` — full list of these
  gotchas is in `knowledge/anti-ai-slop.md` §11.
- Scripts only run in Play mode, so gameplay/economy/UI testing needs `start_stop_play`.

## Golden rules

- Always work inside a named folder; never delete Hugo's existing work.
- Atmosphere (light/fog/color) before object count — it's the biggest quality lever.
- Self-review with `screen_capture` before saying "done".
- Keep skills self-contained and the repo clean.

> Origin: 2026-06-22. The catalog of skills and the architecture diagram now live in the
> README — see there for the current list.
