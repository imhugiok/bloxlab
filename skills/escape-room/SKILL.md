---
name: escape-room
description: Construye un escape room / puzzle (acertijos encadenados para escapar) de CALIDAD en el Roblox Studio abierto, vía el MCP oficial Roblox_Studio. Puzzles justos y bien hilados, sin look de IA. Úsalo cuando el usuario pida un escape room, sala de escape o juego de puzzles.
---

# /bloxlab:escape-room — Escape room con puzzles justos

Construyes una sala (o varias) donde el jugador resuelve acertijos encadenados para avanzar/escapar. La calidad está en **puzzles justos, bien señalizados y con buena cadena lógica**, en un espacio creíble. Aplica anti-AI-slop (`knowledge/anti-ai-slop.md`).

## 0. Pregunta primero (SIEMPRE, antes de construir)
NO empieces a construir. Pregunta qué quiere:
1. **Ya tengo algo en mente** — que describa tema/dificultad/cantidad de puzzles; aterrízalo.
2. **Un tema específico** — pregunta el escenario (laboratorio, mansión, prisión, templo, nave, oficina) y propón.
3. **Lluvia de ideas** — propón 2-3 conceptos de escape cortos; deja que elija/mezcle.
4. **Sorpréndeme** — elige TÚ un concepto fuerte y específico y dilo en 1 línea.
5. **Solo estoy probando** — una sala con 1-2 puzzles encadenados y la puerta de salida.
6. **Planear primero** — plan SIN construir; espera su OK.
Confirma en 1 línea antes de arrancar. Si dice "hazlo ya", asume Sorpréndeme.

## 1. Diseño de puzzles (lo que evita el slop)
- **Cadena clara:** cada puzzle da la pista/llave del siguiente (código → caja → llave → puerta → ...). El jugador siempre sabe "qué busco ahora", aunque no cómo aún.
- **Justo, con señalización:** las pistas existen y son hallables (no adivinar números al azar). Recompensa observar el entorno. Evita pixel-hunting imposible.
- **Variedad de mecánicas:** códigos, palancas/secuencias, emparejar símbolos, peso/presión, luz/color, orden de botones. No el mismo puzzle repetido.
- **Feedback:** al acertar, algo CAMBIA visible/audible (se abre, se enciende, suena). Al fallar, pista sutil, sin castigar de más.
- **Espacio creíble y temático:** una sala que parece un lugar real (laboratorio, etc.), con la atmósfera adecuada; los objetos del puzzle integrados, no flotando.
- **Dificultad progresiva:** el primer puzzle enseña; suben en complejidad.

## 2. Construcción (con el MCP oficial)
1. `get_studio_state`. Trabaja en `Workspace/EscapeRoom_<tema>`.
2. **Sala temática:** construye el espacio (paredes, props, atmósfera) que dé el tema; integra los elementos de puzzle como parte del decorado.
3. **Puzzles (execute_luau):** lógica por puzzle: teclado/código que valida, palancas con estado, zonas de presión, botones en secuencia; al resolver, dispara el cambio (abrir compartimento, dar ítem/llave, encender).
4. **Cadena:** conecta puzzles: la salida de uno habilita el siguiente; la última abre la puerta de escape.
5. **Pistas:** coloca pistas legibles en el entorno (notas, marcas, colores) con decals válidos o `SurfaceGui` (apóyate en `/bloxlab:game-ui` para textos/pistas).
6. **Salida:** puerta final que se abre al completar la cadena, con feedback claro de victoria.

## 3. Checklist técnico (aplica siempre)
- Carpeta nombrada; no borres lo del usuario; ChangeHistory waypoints.
- Estado de puzzles en SERVIDOR si es multijugador (consistencia/anti-trampa).
- Evita z-fighting; `Color3`; pistas legibles; escala humana; objetos integrados (no flotando).
- Auto-revisión: `screen_capture`; ¿se entiende qué hacer y las pistas se ven?; corrige, repite.
- Considera `start_stop_play` para resolver el primer puzzle tú mismo (¿es justo?).

## 4. Cierre
Resume sala(s), puzzles y cadena. Ofrece: probar con `start_stop_play`, más puzzles/salas, cronómetro/pistas, o NPCs (`/bloxlab:npc`).

## Reglas duras
- Puzzles justos y con pistas hallables; nada de adivinar a ciegas.
- Cada acierto con feedback visible; cadena lógica clara.
- Empieza con 1-2 puzzles encadenados y crece. Si algo falla, sigue sin romper y avísalo.
