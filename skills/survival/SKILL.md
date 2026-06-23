---
name: survival
description: Construye un juego de supervivencia (recolectar, craftear, resistir amenazas) de CALIDAD en el Roblox Studio abierto, vía el MCP oficial Roblox_Studio. Mundo con tensión y bucle claro, sin look de IA. Úsalo cuando el usuario pida survival, supervivencia o crafteo.
---

# /hugoblox:survival — Supervivencia con tensión y bucle claro

Construyes un survival: el jugador recolecta recursos, craftea/mejora, y resiste una amenaza (hambre, frío, noche, enemigos, desastre). La calidad está en el **bucle de tensión-alivio y un mundo creíble** (no un terreno plano vacío). Aplica anti-AI-slop (`knowledge/anti-ai-slop.md`).

## 0. Pregunta primero (SIEMPRE, antes de construir)
NO empieces a construir. Pregunta qué quiere:
1. **Ya tengo algo en mente** — que describa amenaza/bioma/bucle; aterrízalo.
2. **Un tema específico** — pregunta el escenario (isla, bosque, nieve, apocalipsis zombie, océano, espacio) y propón.
3. **Lluvia de ideas** — propón 2-3 conceptos de survival cortos; deja que elija/mezcle.
4. **Sorpréndeme** — elige TÚ un concepto fuerte y específico y dilo en 1 línea.
5. **Solo estoy probando** — un islote con recursos + 1 amenaza simple (ciclo día/noche o hambre).
6. **Planear primero** — plan SIN construir; espera su OK.
Confirma en 1 línea antes de arrancar. Si dice "hazlo ya", asume Sorpréndeme.

## 1. Anatomía de un buen survival
- **Bucle:** recolectar (madera, comida, mineral) → craftear (herramientas, refugio, fuego) → sobrevivir a la amenaza → expandir. Cada vuelta el jugador está un poco más seguro.
- **Tensión-alivio:** una presión constante (hambre/frío baja con el tiempo; la noche trae peligro) y momentos de alivio (día, refugio, fuego). El ritmo es el corazón.
- **Recursos repartidos:** nodos de recurso por el mapa que obligan a explorar y exponerse; no todo a la mano.
- **Amenaza creíble:** depredadores/enemigos (NPCs) o ambiental (tormenta, marea, oscuridad). Que se sienta peligro real pero justo.
- **Mundo con identidad:** bioma con relieve, vegetación, agua, puntos de interés (no un plano texturizado). Usa terreno/props.
- **Stats claros:** salud, hambre/temperatura, inventario simple y legible.

## 2. Construcción (con el MCP oficial)
1. `get_studio_state`. Trabaja en `Workspace/Survival_<bioma>` (y terreno si aplica).
2. **Mundo:** relieve con `Terrain` o partes, vegetación/rocas/agua, puntos de interés. Tema y luz del bioma. Variedad, no retícula.
3. **Recursos (execute_luau):** nodos recolectables (`.Touched`/herramienta) que dan materiales y reaparecen; inventario simple (leaderstats o folder por jugador).
4. **Crafteo:** estación o menú que convierte materiales en herramientas/estructuras (puedes apoyarte en `/hugoblox:game-ui`).
5. **Amenaza:** ciclo día/noche (`Lighting.ClockTime` animado), y/o stat de hambre/frío que baja y daña si llega a 0, y/o enemigos NPC de noche (`/hugoblox:npc`).
6. **Refugio/fuego:** colocar estructuras y una hoguera que restaura/ahuyenta como recompensa al progreso.

## 3. Checklist técnico (aplica siempre)
- Carpeta nombrada; no borres lo del usuario; ChangeHistory waypoints.
- Stats/inventario/daño en el SERVIDOR.
- Evita z-fighting; `Color3`; mundo con relieve e identidad; escala humana.
- Auto-revisión: `screen_capture`; ¿se siente un mundo con tensión, no un plano vacío?; corrige, repite.
- Considera `start_stop_play` para sentir el ciclo.

## 4. Cierre
Resume mundo, bucle y amenaza. Ofrece: probar con `start_stop_play`, más recursos/crafteos, enemigos (`/hugoblox:npc`), o UI (`/hugoblox:game-ui`).

## Reglas duras
- Bucle de tensión-alivio claro; presión constante pero justa.
- Stats en server; mundo con relieve e identidad, nunca plano vacío.
- Empieza con un bioma pequeño funcional y crece. Si algo falla, sigue sin romper y avísalo.
