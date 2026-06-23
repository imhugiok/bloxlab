---
name: backrooms
description: Construye un nivel tipo Backrooms (liminal, infinito, inquietante) de CALIDAD en el Roblox Studio abierto, vía el MCP oficial Roblox_Studio. Sin look de IA. Úsalo cuando el usuario pida backrooms, espacios liminales o pasillos infinitos.
---

# /bloxlab:backrooms — Nivel liminal de Backrooms

Construyes un espacio liminal (vacío, repetitivo, "mal") que da desasosiego, en el Studio abierto, vía el MCP oficial `Roblox_Studio`. El miedo aquí es la **monotonía inquietante y la desorientación**, no los sustos. Aplica los principios anti-AI-slop (en `knowledge/anti-ai-slop.md`): escala humana, color con intención, auto-revisión.

## 0. Pregunta primero (SIEMPRE, antes de construir)
NO empieces a construir. Pregunta qué quiere, con estas opciones:
1. **Ya tengo algo en mente** — que describa nivel/tema/tamaño; aterrízalo.
2. **Un tema específico** — pregunta cuál "level" o vibe (oficinas amarillas clásicas, almacén, piscina liminal, estacionamiento) y propón.
3. **Lluvia de ideas** — propón 2-3 variantes liminales cortas; deja que elija/mezcle.
4. **Sorpréndeme** — elige TÚ una variante fuerte y específica y dilo en 1 línea.
5. **Solo estoy probando** — una sección pequeña (un sector laberíntico) rápida.
6. **Planear primero** — plan SIN construir; espera su OK.
Confirma en 1 línea antes de arrancar. Si dice "hazlo ya", asume Sorpréndeme.

## 1. Lo que hace que "se sienta backrooms"
- **Color enfermizo y uniforme:** el clásico es amarillo apagado (mono-amarillo de paredes/alfombra) bajo fluorescente. Define una paleta enferma (amarillo mostaza sucio, beige, verdoso) y mantenla.
- **Iluminación fluorescente plana y zumbante:** muchas luces de techo regulares, luz fría-verdosa, alguna parpadeando/muerta. Aquí la uniformidad de luz SÍ se busca (es lo inquietante), pero deja zonas muertas oscuras.
- **Repetición + desorientación:** módulos de cuarto/pasillo que se repiten, sin landmarks claros, con bucles y callejones. Que se sienta infinito y "ya pasé por aquí".
- **Vacío:** casi sin props. Lo que sobra (humedad, manchas, un cable suelto, una silla volcada solitaria) pega más por contraste con el vacío.
- **Texturas:** alfombra vieja, paredes con humedad/manchas. Usa `generate_material` para una alfombra/empapelado sucio si ayuda.

## 2. Construcción (con el MCP oficial)
1. `get_studio_state` para confirmar Studio. Trabaja en `Workspace/Backrooms_<variante>`.
2. **Módulos repetibles:** define 2-3 piezas (cuarto, pasillo, intersección) y repítelas en una retícula GRANDE con giros, para sensación de laberinto infinito. Techo bajo (~10-12 studs), pasillos angostos.
3. **Atmósfera:** `Lighting` con tinte verdoso-amarillo, `Atmosphere` con haze leve, fluorescentes (muchos `PointLight`/`SurfaceLight` regulares, color frío), 1-2 parpadeando. Mantén legible (sube Ambient).
4. **Materiales/manchas:** alfombra y paredes con material y color sucios; añade decals de humedad/manchas solo con IDs válidos (si no, omite).
5. **Detalle escaso:** 1-3 objetos solitarios por sector (silla, cono, charco) con `search_asset`/`insert_asset`, sin saturar.
6. **Sonido:** zumbido fluorescente en loop si hay ID válido; si no, omite.

## 3. Checklist técnico (aplica siempre)
- Carpeta nombrada; no borres lo del usuario; usa ChangeHistory waypoints.
- Evita z-fighting: sube el piso (~y=0.5) si hay baseplate, o construye lejos del origen.
- `Color3` (no BrickColor); paleta acotada; escala humana (personaje ~5 studs, puertas ~7-10).
- Sombras: casi todas las luces sin sombra; 1-2 con sombra para drama.
- Auto-revisión: `screen_capture`, critica vs anti-slop (¿se siente liminal y legible?), corrige, repite (2-4 pasadas).

## 4. Cierre
Resume qué construiste y dónde. Ofrece: probar con `start_stop_play`, ampliar el laberinto, o añadir una entidad/persecución (con `/bloxlab:key-door-monster` o `/bloxlab:npc`).

## Reglas duras
- Una sección/sector a la vez, no un nivel infinito de un tiro (usa repetición modular para dar esa ilusión).
- Nunca borres el trabajo del usuario. Si un asset/generación falla, sigue sin romper y avísalo.
- Calidad > cantidad: el vacío bien iluminado y repetido vale más que llenar de cosas.
