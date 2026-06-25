---
name: npc
description: Crea NPCs (personajes no jugables: vendedores, guías, enemigos, fauna) de CALIDAD en el Roblox Studio abierto, vía el MCP oficial Roblox_Studio. Con comportamiento creíble (patrulla, persecución, diálogo), sin look de IA. Úsalo cuando el usuario pida NPCs, enemigos, aldeanos o criaturas.
---

# /bloxlab:npc — NPCs con comportamiento creíble

Creas NPCs que dan vida al juego: vendedores/guías que hablan, enemigos que persiguen, fauna que deambula, aldeanos que pueblan un town. La calidad está en **comportamiento creíble y legible** (no un dummy plantado que no hace nada). **Antes de construir, lee y aplica** `${CLAUDE_PLUGIN_ROOT}/knowledge/anti-ai-slop.md`. Si no puedes abrirlo (p. ej. en modo prueba local), aplica su núcleo de memoria: mata la uniformidad (sin grids perfectos), atmósfera/composición antes que cantidad, `Color3` con paleta acotada (no `BrickColor`), escala humana en studs, imperfección intencional, y auto-revisión con `screen_capture` antes de decir "listo".

## 0. Pregunta primero (SIEMPRE, antes de construir)
NO empieces a construir. Pregunta qué quiere:
1. **Ya tengo algo en mente** — que describa qué NPC, rol y comportamiento; aterrízalo.
2. **Un tipo específico** — pregunta el tipo (vendedor/diálogo, guía/quest, enemigo perseguidor, guardia patrulla, fauna/ambiente) y el tema, y propón.
3. **Lluvia de ideas** — propón 2-3 NPCs/comportamientos cortos; deja que elija/mezcle.
4. **Sorpréndeme** — elige TÚ un NPC con rol y comportamiento concretos y dilo en 1 línea.
5. **Solo estoy probando** — un NPC simple (uno que deambula o uno con diálogo).
6. **Planear primero** — describe el/los NPC SIN construir; espera su OK.
Confirma en 1 línea antes de arrancar. Si dice "hazlo ya", asume Sorpréndeme acorde al juego.

## 1. Qué hace a un NPC creíble (no slop)
- **Comportamiento, no estatua:** que haga algo (deambular, patrullar ruta, mirar al jugador cercano, perseguir, reaccionar). Un dummy inmóvil mata la inmersión.
- **Telegrafía e intención legible:** el jugador debe entender qué es y qué hace (un enemigo se ve y suena amenazante; un vendedor invita con prompt). Estados claros (idle/alerta/persigue).
- **Apariencia con identidad:** acorde al juego; usa rigs/modelos con `search_asset`/`insert_asset`, `generate_mesh`/`generate_procedural_model` para criaturas, o personaliza un `Humanoid` (ropa/color/escala). Evita el dummy gris.
- **Movimiento natural:** `Humanoid:MoveTo`/pathfinding (`PathfindingService`) para que no se atore en paredes; velocidad y animaciones acordes.
- **Interacción clara:** `ProximityPrompt` para hablar/comprar; diálogo legible (apóyate en `/bloxlab:game-ui`).
- **Justo (si es enemigo):** detección y daño razonables, telegrafiados, con forma de evitarlo.

## 2. Construcción (con el MCP oficial)
1. `get_studio_state`. Trabaja en `Workspace/NPCs` (o dentro del mapa correspondiente).
2. **Cuerpo:** crea/inserta el modelo con `Humanoid` (rig); personaliza apariencia (color/ropa/escala) o usa una criatura generada.
3. **Comportamiento (execute_luau, server):**
   - Deambular/patrulla: rutas con `MoveTo` entre puntos; espera y repite.
   - Persecución (enemigo): detecta jugador en rango/visión, persigue con `PathfindingService`, ataca al alcance (daño en server), pierde al jugador si escapa.
   - Diálogo/vendedor: `ProximityPrompt` que abre UI/diálogo; acciones (vender/dar quest) validadas en server.
4. **Animación/feedback:** animaciones de caminar/idle/atacar (IDs válidos o omitir); sonidos/efectos para telegrafiar.
5. **Spawns/manager:** un script que instancia y reaparece NPCs según el juego (oleadas, población del town, etc.).

## 3. Checklist técnico (aplica siempre)
- Carpeta nombrada; no borres lo del usuario; ChangeHistory waypoints.
- IA/daño/economía del NPC en el SERVIDOR.
- Usa `PathfindingService` para que no se atoren; evita NPCs flotando o atascados.
- Apariencia con identidad (no dummy gris); estados legibles; escala humana/coherente.
- Auto-revisión: `screen_capture`; ¿se ve con identidad y se entiende su rol?; corrige, repite.
- Considera `start_stop_play` para ver el comportamiento (¿se mueve/persigue/habla bien?).

## 4. Cierre
Resume el/los NPC y su comportamiento. Ofrece: probar con `start_stop_play`, más tipos, integrarlos a un sistema (`/bloxlab:key-door-monster`), o diálogos/tienda (`/bloxlab:game-ui`).

## Reglas duras
- Nada de dummies inmóviles: todo NPC hace algo legible.
- IA/daño en server; pathfinding para no atorarse; apariencia con identidad.
- Empieza con un NPC funcional y crece. Si un asset/animación falla, sigue sin romper y avísalo.
