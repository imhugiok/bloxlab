---
name: tower-defense
description: Construye un tower defense (oleadas de enemigos por un camino, torres que defienden) de CALIDAD en el Roblox Studio abierto, vía el MCP oficial Roblox_Studio. Sin look de IA. Úsalo cuando el usuario pida un tower defense o TD.
---

# /hugoblox:tower-defense — Tower Defense con buen ritmo

Construyes un TD: enemigos avanzan por un camino hacia una base; el jugador coloca torres con su dinero para detenerlos por oleadas. La calidad está en el **ritmo de oleadas, el balance y un mapa con identidad** (no un camino gris en zigzag plano). Aplica anti-AI-slop (`knowledge/anti-ai-slop.md`).

## 0. Pregunta primero (SIEMPRE, antes de construir)
NO empieces a construir. Pregunta qué quiere:
1. **Ya tengo algo en mente** — que describa tema/torres/enemigos; aterrízalo.
2. **Un tema específico** — pregunta el tema (medieval, zombies, militar, brainrot/memes, fantasía) y propón.
3. **Lluvia de ideas** — propón 2-3 conceptos de TD cortos; deja que elija/mezcle.
4. **Sorpréndeme** — elige TÚ un concepto fuerte y específico y dilo en 1 línea.
5. **Solo estoy probando** — un mapa con 1 camino, 1 torre y 1 oleada.
6. **Planear primero** — plan SIN construir; espera su OK.
Confirma en 1 línea antes de arrancar. Si dice "hazlo ya", asume Sorpréndeme.

## 1. Anatomía de un buen TD
- **Camino legible:** ruta clara de entrada a la base con curvas que creen buenos puntos de torre. Marca el camino visualmente (textura/color distinto del terreno de construcción).
- **Oleadas con ritmo:** dificultad creciente, mezcla de enemigos (rápidos, tanques, masa), pausas entre oleadas para colocar/mejorar. Jefe cada ciertas oleadas.
- **Torres con roles:** variedad (daño único alto, área, lento, soporte). Costo y mejora claros. Decisiones interesantes, no una torre que gana todo.
- **Economía:** dinero por matar + por oleada; precios que obliguen a elegir. Vidas/base que se pierden si pasan enemigos.
- **Feedback:** salud de enemigos, dinero, contador de oleada, daño/efectos visibles.
- **No-slop:** mapa con tema e identidad (no un tablero plano), zonas de construcción claras, buena luz.

## 2. Construcción (con el MCP oficial)
1. `get_studio_state`. Trabaja en `Workspace/TowerDefense_<tema>`.
2. **Mapa + camino:** define waypoints (carpeta de partes invisibles o `Attachment`s) que marcan la ruta; construye el camino visible y zonas de torre alrededor. Tema con material/props.
3. **Enemigos (execute_luau):** modelos con `Humanoid` que recorren los waypoints (`MoveTo`) hacia la base; al llegar restan vidas. Salud por tipo.
4. **Oleadas:** server script que genera oleadas con delays crecientes y mezcla de tipos; anuncia la oleada.
5. **Torres:** colocación en zonas válidas (pad/grid), que detectan enemigos en rango y disparan (daño en server), con costo/mejora. Empieza con 1-2 tipos.
6. **Economía/UI:** `leaderstats` con dinero; HUD con vidas/oleada (puedes apoyarte en `/hugoblox:game-ui`).

## 3. Checklist técnico (aplica siempre)
- Carpeta nombrada; no borres lo del usuario; ChangeHistory waypoints.
- Lógica (oleadas, daño, economía) en el SERVIDOR.
- Evita z-fighting; `Color3`; camino y zonas de torre claramente legibles; escala coherente.
- Auto-revisión: `screen_capture`; ¿se entiende el camino y dónde construir?; corrige, repite.
- Considera `start_stop_play` para ver una oleada.

## 4. Cierre
Resume mapa, oleadas y torres. Ofrece: probar con `start_stop_play`, más torres/enemigos/oleadas, jefe, o UI con `/hugoblox:game-ui`.

## Reglas duras
- Camino y zonas de construcción siempre legibles; oleadas con ritmo creciente.
- Lógica en server; torres con roles distintos (no una que gana todo).
- Empieza con el bucle mínimo (1 camino, 1 torre, 1 oleada) y crece. Si algo falla, sigue sin romper y avísalo.
