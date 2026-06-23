---
name: simulator
description: Construye un simulator (recolecta/click/grind para subir stats y mascotas) de CALIDAD en el Roblox Studio abierto, vía el MCP oficial Roblox_Studio. Incluye estilo brainrot. Bucle adictivo y legible, sin look de IA. Úsalo cuando el usuario pida un simulator, pet simulator o brainrot.
---

# /bloxlab:simulator — Simulator / brainrot con bucle adictivo

Construyes un simulator: el jugador hace una acción simple (recolectar, click, golpear) → gana moneda/poder → sube de zona → desbloquea mejoras/mascotas → repite. La calidad está en el **bucle satisfactorio, la progresión por zonas y el feedback visual** (no spam de cubos). Estilo "brainrot" = humor absurdo, memes, mascotas raras, números que suben rápido. Aplica anti-AI-slop (`knowledge/anti-ai-slop.md`).

## 0. Pregunta primero (SIEMPRE, antes de construir)
NO empieces a construir. Pregunta qué quiere:
1. **Ya tengo algo en mente** — que describa la acción/tema/mascotas; aterrízalo.
2. **Un tema específico** — pregunta el tema (recolectar X, romper bloques, brainrot/memes, mascotas, fuerza) y propón.
3. **Lluvia de ideas** — propón 2-3 conceptos de simulator cortos; deja que elija/mezcle.
4. **Sorpréndeme** — elige TÚ un concepto fuerte y específico y dilo en 1 línea.
5. **Solo estoy probando** — zona inicial mínima (acción + moneda + 1 mejora).
6. **Planear primero** — plan SIN construir; espera su OK.
Confirma en 1 línea antes de arrancar. Si dice "hazlo ya", asume Sorpréndeme.

## 1. Anatomía de un buen simulator
- **Bucle core:** acción simple repetible (recolectar/click/golpear) → moneda → comprar mejora (más poder/velocidad/capacidad) → la acción rinde más → avanzas. Recompensa inmediata y visible.
- **Progresión por zonas:** zonas con muros de precio (cada zona pide más moneda y da mejores recursos). Siempre una "siguiente zona" visible que motive.
- **Coleccionables/mascotas:** huevos/cajas que dan mascotas con rareza (común→legendario) que multiplican stats. La rareza y el "gacha" enganchan.
- **Feedback:** números flotantes al ganar (`BillboardGui` que sube y se desvanece), sonidos, partículas. El "juice" es clave en este género.
- **Brainrot:** si es el tema, humor absurdo, nombres meme, mascotas ridículas, colores saturados y caos controlado. Aun así, legible y con jerarquía.
- **No-slop:** zonas con identidad visual propia (no el mismo cubo repintado), buena luz, mascotas/props con forma (usa `generate_mesh`/`generate_procedural_model` o `search_asset`).

## 2. Construcción (con el MCP oficial)
1. `get_studio_state`. Trabaja en `Workspace/Simulator_<tema>`.
2. **leaderstats:** server script con `Coins` (o stat temática) y quizá `Power`/`Rebirths`.
3. **Acción core (execute_luau):** zona/recursos que al recolectar (`.Touched` o herramienta) suman moneda; respawn de recursos.
4. **Tienda/mejoras:** pads o UI para comprar upgrades (multiplicadores). Valida en server.
5. **Zonas:** sectores con muro de precio que se desbloquean; cada zona con tema visual distinto y mejores recursos.
6. **Mascotas (opcional):** sistema de huevos con rareza ponderada que otorga multiplicadores; mascota sigue al jugador.
7. **Juice:** texto flotante de ganancia, partículas, sonidos (IDs válidos o omitir).

## 3. Checklist técnico (aplica siempre)
- Carpeta nombrada; no borres lo del usuario; ChangeHistory waypoints.
- Economía y stats en el SERVIDOR (anti-trampas); valida compras en server.
- Evita z-fighting; `Color3`; cada zona con identidad; UI/numeritos legibles.
- Auto-revisión: `screen_capture`; ¿se ve el bucle y las zonas con identidad?; corrige, repite.
- Considera `start_stop_play` para sentir el bucle.

## 4. Cierre
Resume el bucle, zonas y mascotas. Ofrece: probar con `start_stop_play`, más zonas, rebirth/prestigio, o UI con `/bloxlab:game-ui`.

## Reglas duras
- Recompensa inmediata y "siguiente meta" siempre visible.
- Stats en el servidor; feedback visual (juice) sí o sí.
- Empieza con la zona inicial funcional y crece. Si algo falla, sigue sin romper y avísalo.
