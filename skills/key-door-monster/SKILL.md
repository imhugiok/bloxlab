---
name: key-door-monster
description: Implementa un sistema de objetivo (llaves, puertas, monstruo/amenaza y meta) de CALIDAD en el Roblox Studio abierto, vía el MCP oficial Roblox_Studio. Da gameplay y tensión a un mapa existente. Úsalo cuando el usuario pida llaves, puertas, monstruo, objetivo o "loop" de escape.
---

# /bloxlab:key-door-monster — Sistema de objetivo y tensión

Implementas el bucle clásico que convierte un mapa en un JUEGO: busca llaves → abre puertas → evita/sobrevive a una amenaza → llega a la meta. Ideal para sumarlo a un `/bloxlab:horror-map`, `/bloxlab:backrooms` o cualquier mapa. La calidad está en **tensión justa, feedback claro y reglas legibles**. Aplica anti-AI-slop (`knowledge/anti-ai-slop.md`).

## 0. Pregunta primero (SIEMPRE, antes de construir)
NO empieces a construir. Pregunta qué quiere:
1. **Ya tengo algo en mente** — que describa objetivo/amenaza/mapa; aterrízalo.
2. **Un tema específico** — pregunta cuántas llaves, qué amenaza (monstruo que persigue, trampa, tiempo) y dónde (mapa existente o nuevo), y propón.
3. **Lluvia de ideas** — propón 2-3 variantes del bucle cortas; deja que elija/mezcle.
4. **Sorpréndeme** — elige TÚ una configuración fuerte y específica y dilo en 1 línea.
5. **Solo estoy probando** — 1 llave, 1 puerta, 1 amenaza simple, 1 meta.
6. **Planear primero** — plan SIN construir; espera su OK.
Confirma en 1 línea antes de arrancar. Si dice "hazlo ya", asume Sorpréndeme. Pregunta también si hay un mapa existente sobre el que montar el sistema.

## 1. Diseño del bucle (lo que evita el slop)
- **Objetivo claro:** el jugador debe saber qué buscar (X llaves) y a dónde ir (puerta/meta). Comunícalo con UI/pistas, no a ciegas.
- **Llaves significativas:** repartidas en lugares que obligan a explorar/arriesgarse; visibles pero no triviales. Feedback al recogerla (sonido, contador).
- **Puertas como compuertas:** la puerta abre solo con su llave (o N llaves); al abrir, cambio visible (anim, sonido). Estructura el ritmo del nivel.
- **Amenaza justa:** monstruo/peligro que crea tensión sin ser imposible. Si persigue: velocidad y detección razonables, con forma de escapar/esconderse. Telegrafía el peligro (sonido, luz).
- **Meta y final:** una salida clara que da victoria con feedback satisfactorio (y opcional: tiempo/score).
- **Tensión-alivio:** alterna momentos seguros y peligrosos; el peligro constante cansa.

## 2. Construcción (con el MCP oficial)
1. `get_studio_state`. Si hay mapa, identifícalo (`search_game_tree`/`inspect_instance`). Trabaja en una carpeta del sistema (ej. `Workspace/<Mapa>/Objective`).
2. **Llaves (execute_luau):** objetos recolectables (`.Touched`/prompt) que suman a un contador por jugador; feedback al recoger.
3. **Puertas:** requieren la(s) llave(s); al cumplir, se abren (tween/CanCollide) con sonido; bloquean si falta.
4. **Amenaza/monstruo:** un NPC que patrulla/persigue (apóyate en `/bloxlab:npc`) o una trampa/tiempo. Detección y daño/captura en server; telegrafía con audio/luz.
5. **Meta:** zona final que valida objetivo completo y dispara victoria (UI, sonido); opcional cronómetro/score.
6. **Feedback/UI:** contador de llaves y objetivo en pantalla (apóyate en `/bloxlab:game-ui`).

## 3. Checklist técnico (aplica siempre)
- Carpeta nombrada; no borres el mapa/trabajo del usuario; ChangeHistory waypoints.
- Estado del objetivo, llaves y daño en el SERVIDOR (consistencia/anti-trampa).
- Evita z-fighting al añadir piezas; `Color3`; elementos legibles (llaves/puertas se distinguen).
- Telegrafía el peligro; deja siempre una forma justa de evitarlo.
- Auto-revisión: `screen_capture`; ¿se entiende el objetivo y la amenaza?; corrige, repite.
- Considera `start_stop_play` para jugar el bucle (¿es justo y tenso?).

## 4. Cierre
Resume el bucle montado (llaves/puertas/amenaza/meta) y dónde. Ofrece: probar con `start_stop_play`, afinar dificultad, más llaves/puertas, o mejorar el monstruo (`/bloxlab:npc`).

## Reglas duras
- Objetivo siempre legible; amenaza tensa pero evitable; victoria con feedback.
- Lógica en server; telegrafía el peligro.
- Empieza con el bucle mínimo (1 llave/puerta/amenaza/meta) y crece. Si algo falla, sigue sin romper y avísalo.
