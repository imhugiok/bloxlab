---
name: racing
description: Construye un juego de carreras (pista con vueltas, checkpoints, vehículos) de CALIDAD en el Roblox Studio abierto, vía el MCP oficial Roblox_Studio. Pista con buen trazado y game feel, sin look de IA. Úsalo cuando el usuario pida un juego de carreras o racing.
---

# /bloxlab:racing — Carreras con buen trazado

Construyes una carrera: una pista con trazado interesante, checkpoints, vueltas y meta. La calidad está en el **trazado** (curvas que se sientan bien, no un óvalo plano) y la lectura de la pista. Aplica anti-AI-slop (`knowledge/anti-ai-slop.md`).

## 0. Pregunta primero (SIEMPRE, antes de construir)
NO empieces a construir. Pregunta qué quiere:
1. **Ya tengo algo en mente** — que describa tema/tipo de pista/vehículo; aterrízalo.
2. **Un tema específico** — pregunta el escenario (ciudad, desierto, nieve, futurista/neón, kart cartoon) y propón.
3. **Lluvia de ideas** — propón 2-3 conceptos de pista cortos; deja que elija/mezcle.
4. **Sorpréndeme** — elige TÚ un concepto fuerte y específico y dilo en 1 línea.
5. **Solo estoy probando** — un circuito corto con salida, 3-4 checkpoints y meta.
6. **Planear primero** — plan SIN construir; espera su OK.
Confirma en 1 línea antes de arrancar. Si dice "hazlo ya", asume Sorpréndeme.

## 1. Diseño de pista (lo que evita el slop)
- **Trazado con variedad:** mezcla de rectas (velocidad), curvas cerradas (frenado), chicanes y quizá desnivel. Nada de un óvalo plano. Que cada sector tenga carácter.
- **Lectura clara:** bordes/bordillos marcados, dirección obvia, sin trampas de "¿por dónde voy?". Línea de meta y de salida claras.
- **Checkpoints + vueltas:** checkpoints en orden que validan progreso (anti-atajo) y cuentan vueltas; tiempos/posición.
- **Ancho justo:** suficiente para adelantar sin ser un campo abierto; estrecha en curvas técnicas.
- **Ambientación:** decorado a los lados (gradas, props del tema, paisaje), skybox y luz; da sensación de lugar, no una cinta gris flotando.
- **Game feel del vehículo:** si incluyes auto, control responsivo (aceleración/giro razonables); o usa el personaje + plataformas si es estilo "speed run".

## 2. Construcción (con el MCP oficial)
1. `get_studio_state`. Trabaja en `Workspace/Racing_<tema>`.
2. **Pista:** traza el circuito con segmentos (rectas + curvas), bordillos y superficie distinta del entorno. Salida/meta marcadas. Todo `Anchored`.
3. **Checkpoints (execute_luau):** zonas en orden con `.Touched` que registran progreso por jugador, evitan atajos y suman vuelta al cruzar meta tras pasar todos.
4. **Vehículo (si se pide):** un auto simple (VehicleSeat + chasis) o define que se corre a pie; controles básicos.
5. **Cronómetro/posición:** tiempo de vuelta y mejor tiempo (leaderstats); opcional posición entre jugadores.
6. **Ambientación:** props del tema (`search_asset`/`insert_asset`), piezas con `generate_mesh`, skybox y luz acordes.

## 3. Checklist técnico (aplica siempre)
- Carpeta nombrada; no borres lo del usuario; ChangeHistory waypoints.
- Validación de vueltas/checkpoints en SERVIDOR (anti-atajo/anti-trampa).
- Evita z-fighting (la superficie de pista sobre el terreno); `Color3`; dirección legible; escala coherente.
- Auto-revisión: `screen_capture` del trazado; ¿se entiende a dónde ir y se ve variado?; corrige, repite.
- Considera `start_stop_play` para sentir una vuelta.

## 4. Cierre
Resume pista, checkpoints y vehículo. Ofrece: probar con `start_stop_play`, más sectores/circuitos, power-ups, o UI/cronómetro (`/bloxlab:game-ui`).

## Reglas duras
- Trazado con variedad y dirección legible; nunca un óvalo plano gris.
- Checkpoints ordenados validados en server (anti-atajo).
- Empieza con un circuito corto funcional y crece. Si algo falla, sigue sin romper y avísalo.
