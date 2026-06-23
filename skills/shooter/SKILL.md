---
name: shooter
description: Construye un shooter (FPS/TPS o arena de combate) de CALIDAD en el Roblox Studio abierto, vía el MCP oficial Roblox_Studio. Mapa con buen flujo de combate y game feel, sin look de IA. Úsalo cuando el usuario pida un shooter, FPS, PVP o arena de combate.
---

# /bloxlab:shooter — Shooter con buen flujo de combate

Construyes un shooter centrado en un **mapa con buen flujo** (cobertura, sightlines, rutas) y, si se pide, mecánica de disparo básica. La calidad está en el **diseño de combate** (no una caja plana) y el game feel. Aplica anti-AI-slop (`knowledge/anti-ai-slop.md`).

## 0. Pregunta primero (SIEMPRE, antes de construir)
NO empieces a construir. Pregunta qué quiere:
1. **Ya tengo algo en mente** — que describa modo/tema/tamaño; aterrízalo.
2. **Un tema específico** — pregunta setting y modo (FFA arena, equipos/captura, urbano, desierto, espacial) y propón.
3. **Lluvia de ideas** — propón 2-3 conceptos de mapa/modo cortos; deja que elija/mezcle.
4. **Sorpréndeme** — elige TÚ un concepto fuerte y específico y dilo en 1 línea.
5. **Solo estoy probando** — una arena pequeña con cobertura y 2 spawns.
6. **Planear primero** — plan SIN construir; espera su OK.
Confirma en 1 línea antes de arrancar. Si dice "hazlo ya", asume Sorpréndeme.

## 1. Diseño de combate (lo que evita el slop)
- **Cobertura y sightlines:** mezcla de líneas largas (para rifles) y espacios cerrados (para corto alcance). Coberturas a media altura repartidas, no simétricas y monótonas.
- **Rutas y flujo:** múltiples caminos entre puntos clave, flancos, verticalidad (rampas, segundos pisos, cajas para saltar). Evita un solo pasillo o una caja vacía.
- **Spawns justos:** spawns separados y protegidos (sin spawn-kill), idealmente por equipo.
- **Puntos focales:** un objetivo/centro disputado (bandera, punto, loot) que genere acción.
- **Balance visual vs claridad:** tema fuerte, pero los enemigos deben leerse contra el fondo (no camuflaje accidental). Color de equipos claro.
- **Escala:** pasillos y coberturas a escala humana; alturas saltables.

## 2. Construcción (con el MCP oficial)
1. `get_studio_state`. Trabaja en `Workspace/Shooter_<tema>`.
2. **Blockout del mapa:** define puntos clave y conéctalos con varias rutas + verticalidad. Coberturas asimétricas. Todo `Anchored`.
3. **Spawns/equipos:** `SpawnLocation` por equipo (TeamColor) en zonas seguras.
4. **Tema/atmósfera:** materiales, props (`search_asset`/`insert_asset`), `generate_mesh`/`generate_material` para piezas hero, skybox y luz que mantenga clara la lectura de jugadores.
5. **Combate (si se pide):** herramienta de arma básica (raycast desde la cámara, daño al `Humanoid`, cadencia/cooldown, recarga). Daño en server (validación) para evitar trampas. Mantenlo simple y limpio.
6. **Objetivo de modo (opcional):** punto a capturar, banderas, o conteo de eliminaciones (leaderstats).

## 3. Checklist técnico (aplica siempre)
- Carpeta nombrada; no borres lo del usuario; ChangeHistory waypoints.
- Daño/score en SERVIDOR (anti-trampas).
- Evita z-fighting; `Color3`; equipos legibles; escala humana.
- Auto-revisión: `screen_capture` desde ojos de jugador; ¿hay cobertura, rutas y lectura clara?; corrige, repite.
- Considera `start_stop_play` para sentir el flujo.

## 4. Cierre
Resume mapa/modo. Ofrece: probar con `start_stop_play`, añadir armas/modo, NPCs enemigos (`/bloxlab:npc`), o UI/HUD (`/bloxlab:game-ui`).

## Reglas duras
- Mapa con cobertura, rutas múltiples y verticalidad; nunca una caja plana.
- Spawns justos; lógica de daño en server.
- Empieza con la arena base y crece. Si un asset/script falla, sigue sin romper y avísalo.
