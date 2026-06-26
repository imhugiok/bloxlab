# Contributing to BloxLab

Thanks for wanting to help. BloxLab is a Claude Code plugin: a set of skills that build **quality** Roblox games via the official `Roblox_Studio` MCP, with an anti-AI-slop quality layer. New skills, fixes, and quality improvements are all welcome.

🇪🇸 *Resumen en español al final.*

## Before you start

For anything bigger than a small fix, **open an issue first** so we can agree on the approach before you write code. Use the "Propose a skill" or "Bug report" templates.

## How the project is structured

```text
.claude-plugin/        plugin.json + marketplace.json (manifest + version)
skills/<name>/SKILL.md  one skill = one /bloxlab:<name> command
knowledge/             shared rules every skill reads (anti-ai-slop.md, intake.md)
docs/                  design notes
```

## Anatomy of a skill

Every skill is a `skills/<name>/SKILL.md` with:

1. **Frontmatter** — `name` and a `description` that tells Claude when to use it.
2. **Intake first (`## 0`)** — never build blind. Ask what the user wants (the 6-option intake) and confirm in one line before building.
3. **Quality layer** — an imperative line telling the model to read and apply `${CLAUDE_PLUGIN_ROOT}/knowledge/anti-ai-slop.md`, plus a condensed inline fallback so it still works in local-test mode (where the variable is not substituted).
4. **Build recipe** — domain-specific steps using the official MCP, in verifiable stages (blockout → atmosphere/systems → detail), not one giant script.
5. **Mandatory self-review** — `screen_capture`, critique against the anti-slop rules, fix, repeat.
6. **Hard rules** — work in a named `Workspace/<Name>` folder, never delete the user's work, `pcall` risky ops, never fake asset IDs, stop safely on failure.

The fastest way to write one: copy an existing skill close to your genre (e.g. `skills/horror-map/SKILL.md`) and adapt it.

## Quality bar (the whole point)

Output must not look auto-generated. Read `knowledge/anti-ai-slop.md` and apply it: kill uniformity, atmosphere before object count, intentional palette (`Color3`, not default `BrickColor`), human scale, intentional imperfection, and a mandatory screenshot self-review. A skill that ships generic-looking results defeats the purpose of the project.

## Roblox technical reality (read this)

`knowledge/anti-ai-slop.md` has a "technical gotchas" section written from real Studio testing. Notably:

- You **cannot** set `Lighting.Technology` from `execute_luau` — wrap all `Lighting` writes in `pcall` so a failure doesn't abort the build.
- Lighting must be **calibrated empirically per mood** (dark horror = low ambient + light pools; bright/liminal = high ambient + flat light). Don't trust fixed numbers; iterate with `screen_capture`.
- High `Reflectance` reads as a white mirror — use low reflectance for water.

Don't fight these; work with them.

## Testing a skill

You need Roblox Studio with the official `Roblox_Studio` MCP connected to Claude Code (see the [README](README.md)). Then either:

- Install the plugin and run `/bloxlab:<name>`, or
- Follow your `SKILL.md` steps directly against the MCP (no install needed).

Build on a **throwaway place**, and verify with `screen_capture` before calling it done. If you ran scripts in Play, check `get_console_output` for runtime errors.

## Pull requests

1. Fork, then branch (`feat/<thing>` or `fix/<thing>`). Don't work on `main`.
2. Keep PRs small and focused — one skill or one fix per PR.
3. Match the style of the file you're editing (existing skill bodies are written in Spanish).
4. Describe what you built and **how you tested it** — a screenshot helps a lot.

## License

By contributing you agree your work is licensed under the project's [MIT license](LICENSE).

---

## 🇪🇸 Resumen

BloxLab es un plugin de Claude Code: skills que construyen juegos de Roblox de calidad vía el MCP oficial, sin look de IA. Para cambios grandes, **abre un issue primero**. Un skill = `skills/<nombre>/SKILL.md` (frontmatter + intake primero + leer `${CLAUDE_PLUGIN_ROOT}/knowledge/anti-ai-slop.md` + recipe por pasos + auto-revisión con `screen_capture`). Pruébalo en un place de prueba con Studio + MCP conectado. PRs chicos y enfocados, desde una rama, nunca `main`. Lo más rápido: copia un skill existente parecido y adáptalo. MIT.
