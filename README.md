<!-- Hero image TODO: add assets/hero.png and uncomment
<p align="center">
  <img src="https://raw.githubusercontent.com/ElHugixbb/hugoblox/main/assets/hero.png" alt="HugoBlox — quality Roblox game-building skills for Claude Code" width="840">
</p>
-->

<h1 align="center">HugoBlox</h1>

<p align="center">
  <strong>Quality game-building skills for Roblox — as a Claude Code plugin.</strong><br>
  Type one prompt, get a real Roblox game built in your Studio — <strong>without the generic "AI-slop" look</strong>.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/license-MIT-000000.svg" alt="MIT License">
  <img src="https://img.shields.io/badge/Claude%20Code-plugin-da7756.svg" alt="Claude Code plugin">
  <img src="https://img.shields.io/badge/Roblox-Studio%20MCP-00a2ff.svg" alt="Roblox Studio MCP">
  <img src="https://img.shields.io/badge/no-AI--slop-2ea44f.svg" alt="No AI-slop">
  <img src="https://img.shields.io/badge/skills-14-7c5cff.svg" alt="14 skills">
</p>

> **The engine is solved — taste isn't.** Roblox already ships a first-party AI assistant and an official MCP that can run code, generate meshes/materials, and search assets. What it *can't* do is make the result feel designed. HugoBlox is that missing **quality layer**.

🇪🇸 *Resumen en español al final.*

---

## Why

Roblox's native AI builder (and its official `Roblox_Studio` MCP) already handle the plumbing — and the generative parts (meshes, materials, 3D models) run in Roblox's cloud, so no third-party tool can beat them there. The gap is **taste**: native output looks generic and templated.

HugoBlox doesn't rebuild the engine. It adds per-genre **game-design knowledge** + an **anti-AI-slop checklist** + a build recipe, so what gets built looks intentional, not auto-generated.

```text
You (a prompt in Claude Code)
   → Claude            the brain
   → Roblox_Studio MCP the hands (run code · generate · search assets)
   → HugoBlox skills    the taste (how to make it actually good)
   → your open Roblox Studio
```

No API keys required — Claude Code is the brain.

## Requirements

1. **Roblox Studio** with its MCP enabled: *Assistant → MCP Servers → "Enable Studio as MCP server"*, connected to Claude Code via Quick Connect.
2. **Claude Code** with the official `Roblox_Studio` MCP connected (the skills call its tools).
3. This plugin installed (below).

## Install

**As a Claude Code plugin:**

```text
/plugin marketplace add ElHugixbb/hugoblox
/plugin install hugoblox@hugoblox
/reload-plugins
```

Local development (from a cloned/working folder):

```text
/plugin marketplace add <path-to-this-folder>
/plugin install hugoblox@hugoblox
/reload-plugins
```

## Usage

Open Roblox Studio on a **test place**, then in Claude Code run any skill:

```text
/hugoblox:horror-map
/hugoblox:backrooms
/hugoblox:obby
```

Every skill **asks what you want first** — then builds and **self-reviews with screenshots** before calling it done.

## How it works

A skill is a recipe Claude follows. Each one:

1. **Asks first (intake)** — never builds blind. You pick: *I have an idea · a theme · brainstorm · surprise me · just testing · plan first*.
2. **Builds with the official MCP** — blockout, atmosphere/systems, detailing, scripts.
3. **Self-reviews** — takes a `screen_capture`, critiques it against the anti-AI-slop checklist, fixes, repeats.

Shared rules live in [`knowledge/`](knowledge/): [`anti-ai-slop.md`](knowledge/anti-ai-slop.md) and [`intake.md`](knowledge/intake.md).

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
| `survival` | Gather / craft / survive, tension-and-relief |
| `racing` | Track with a real layout, laps, checkpoints |
| `roleplay-town` | A town/city that feels lived-in |
| `escape-room` | Fair, chained puzzles |

**Systems (drop into any game)**

| Skill | Adds |
|---|---|
| `game-ui` | HUD / menus / shops / dialogs that don't look generic |
| `key-door-monster` | Objective loop: keys, doors, threat, goal |
| `npc` | NPCs with believable behavior |

## The anti-AI-slop rule

Every skill follows the same quality bar ([full list](knowledge/anti-ai-slop.md)): kill uniformity (no perfect grids), atmosphere before object-count, intentional palette (`Color3`, not default `BrickColor`), human scale, intentional imperfection, sound & motion, and a mandatory screenshot self-review before "done".

## Project structure

```text
.claude-plugin/   plugin.json + marketplace.json
skills/           14 skills → /hugoblox:<name>
knowledge/        anti-ai-slop.md, intake.md (shared rules)
docs/             design notes (quality-layer-plan.md)
```

## Status

Early and in active development. The architecture and recipes are in place; not every skill has been battle-tested in Studio yet. Honest by design — skills won't fake asset IDs or sounds, and stop safely instead of breaking your scene. Feedback, issues, and PRs welcome.

## About

Built by **Hugo** ([@ElHugixbb](https://github.com/ElHugixbb)) — making it easy to build *good* Roblox games with AI. Community, MIT-licensed: use it, fork it, open issues and PRs.

<!-- Add your links: site / Instagram / YouTube -->

## License

[MIT](LICENSE).

---

## 🇪🇸 Resumen (Español)

**HugoBlox** es un plugin de **Claude Code** con skills que construyen **juegos de Roblox de calidad a partir de un prompt** — sin el look genérico de IA. Escribes algo como `/hugoblox:horror-map`, Claude **te pregunta qué quieres**, y lo construye en tu Roblox Studio abierto.

- **Cómo funciona:** Claude (cerebro) + el **MCP oficial `Roblox_Studio`** (las manos: ejecuta código, genera mallas/materiales/modelos, busca assets) + los skills de HugoBlox (el buen gusto). **Sin API keys** — el cerebro es Claude Code.
- **Por qué:** la plomería y la generación ya las resuelve Roblox; lo que falta es la **calidad/taste**. Eso es HugoBlox.
- **Requisitos:** Roblox Studio con su MCP activado y conectado a Claude Code + este plugin.
- **Instalar:** `/plugin marketplace add ElHugixbb/hugoblox` → `/plugin install hugoblox@hugoblox` → `/reload-plugins`.
- **Usar:** abre Studio en un lugar de prueba y corre, p. ej., `/hugoblox:horror-map`. Cada skill **pregunta primero** (ya tengo idea / un tema / lluvia de ideas / sorpréndeme / solo probando / planear) y **se autorrevisa con capturas** antes de terminar.
- **14 skills:** terror, backrooms, obby, tycoon, simulator (incl. brainrot), shooter, tower-defense, survival, racing, roleplay-town, escape-room + sistemas (game-ui, key-door-monster, npc).

Regla anti-slop en [`knowledge/anti-ai-slop.md`](knowledge/anti-ai-slop.md). Hecho con cariño por Hugo. MIT.
