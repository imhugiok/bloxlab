# Capa de Calidad para Roblox (rumbo desde 2026-06-22)

## Qué es esto en una frase
Escribir un prompt simple en Claude Code (ej. "crea un mapa tipo backrooms") y que se construya un juego de Roblox **de calidad, que no parezca hecho con IA**.

## Cómo funciona (la arquitectura, simple)
```
Tú escribes en Claude Code  ->  Claude (el cerebro, gratis con tu suscripción)
        ->  usa el MCP oficial "Roblox_Studio" (las manos)
        ->  construye en tu Roblox Studio abierto
```
- **El cerebro:** Claude Code. No usamos tu API key de Anthropic (cara). No hay chat propio en el navegador.
- **Las manos:** el MCP oficial de Roblox (ya conectado en Claude Code y Claude Desktop). Hace todo: ejecutar código, generar mallas/materiales/modelos 3D, buscar e insertar assets, etc.
- **Nuestro valor:** los **skills** (`/horror-map`, `/backrooms`, ...) + el **conocimiento de game design** que hace que el resultado se vea bien y no genérico. Eso es lo único que el asistente nativo de Roblox hace mal.

## Estructura del proyecto
- `skills/<nombre>/SKILL.md` — fuente de cada skill (versionada en el repo).
- `knowledge/` — conocimiento compartido que los skills citan (ej. `anti-ai-slop.md`).
- Copia instalada en `~/.claude/skills/<nombre>/SKILL.md` para que funcione como `/<nombre>` en Claude Code.
- `docs/` — este plan y notas.
- Lo viejo (`mcp-server.mjs`, `plugin/`, `scripts/*dashboard*`, `src/brain`, `src/safety`) queda como referencia histórica. Superado por el MCP oficial; no se borra.

## El MCP oficial: herramientas disponibles (las "manos")
Lectura/inspección: `get_studio_state`, `inspect_instance`, `search_game_tree`, `script_read/search/grep`, `get_console_output`, `screen_capture`, `list_roblox_studios`.
Construcción: `execute_luau` (ejecuta cualquier código = la llave maestra), `multi_edit`.
Generación IA (nube de Roblox, no replicable por terceros): `generate_mesh`, `generate_material`, `generate_procedural_model`.
Assets: `search_asset`, `insert_asset`, `store_image`, `upload_image`.
Pruebas/jugador: `start_stop_play`, `character_navigation`, `user_keyboard_input`, `user_mouse_input`, `wait_job_finished`.
Agentes: `subagent`, `skill`.

## Catálogo de skills (creados)

Todos empiezan con el **intake obligatorio** (`knowledge/intake.md`): preguntan qué quiere el usuario antes de construir (ya tengo algo en mente / un tema / lluvia de ideas / sorpréndeme / solo probando / planear primero). Y todos citan `knowledge/anti-ai-slop.md`.

Modos de juego:
- `/bloxlab:horror-map` — mapa de terror con atmósfera real.
- `/bloxlab:backrooms` — liminal/infinito, luz fluorescente sucia.
- `/bloxlab:obby` — obstáculos justos, progresión, checkpoints.
- `/bloxlab:tycoon` — bucle comprar→producir→crecer.
- `/bloxlab:simulator` — recolectar/click/grind, zonas, mascotas (incl. brainrot).
- `/bloxlab:shooter` — mapa con flujo de combate (+ disparo básico opcional).
- `/bloxlab:tower-defense` — oleadas por un camino, torres con roles.
- `/bloxlab:survival` — recolectar/craftear/resistir, tensión-alivio.
- `/bloxlab:racing` — pista con buen trazado, checkpoints, vueltas.
- `/bloxlab:roleplay-town` — pueblo/ciudad habitable con vida.
- `/bloxlab:escape-room` — puzzles justos encadenados.

Sistemas (piezas para cualquier juego):
- `/bloxlab:game-ui` — HUD/menús/tiendas/diálogos que no se ven genéricos.
- `/bloxlab:key-door-monster` — sistema de objetivo (llaves, puertas, amenaza, meta).
- `/bloxlab:npc` — NPCs con comportamiento (vendedor, guía, enemigo, fauna).

Futuro posible: más géneros (clicker puro, plataformas 2.5D, fishing, cooking), y sub-skills (lighting-mood, terrain, sound-design).

## Workflow para usar/actualizar skills
- Los skills viven en el repo (`skills/`) y se empaquetan en el plugin `bloxlab`.
- Al instalar, Claude Code **copia** el plugin a su caché; **no se auto-actualiza**. Tras agregar/editar skills: subir versión en `.claude-plugin/plugin.json`, y en Claude Code correr la actualización del plugin (`/plugin`) + `/reload-plugins`.
- Para PROBAR un skill no hace falta instalarlo: se sigue su `SKILL.md` y se usa el MCP oficial directo.

## Reglas de oro
- Siempre trabajar dentro de una carpeta nombrada, sin borrar el trabajo existente de Hugo.
- Atmósfera (luz/niebla/color) antes que cantidad de objetos: es la mayor palanca de calidad.
- Auto-revisión con `screen_capture` antes de decir "listo".
- Open source: posible más adelante; mantener el repo limpio y los skills auto-contenidos.
