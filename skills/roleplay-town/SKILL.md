---
name: roleplay-town
description: Construye un mundo de roleplay/town (pueblo o ciudad habitable estilo Brookhaven/Bloxburg) de CALIDAD en el Roblox Studio abierto, vía el MCP oficial Roblox_Studio. Lugares con vida, sin look de IA. Úsalo cuando el usuario pida roleplay, town, ciudad o mundo social.
---

# /hugoblox:roleplay-town — Pueblo/ciudad habitable para roleplay

Construyes un mundo social: casas, tiendas, calles y puntos de interés donde la gente "vive" y juega roles. La calidad está en que se sienta **un lugar real y acogedor con vida**, no edificios-caja repetidos. Aplica anti-AI-slop (`knowledge/anti-ai-slop.md`).

## 0. Pregunta primero (SIEMPRE, antes de construir)
NO empieces a construir. Pregunta qué quiere:
1. **Ya tengo algo en mente** — que describa el lugar/época/tamaño; aterrízalo.
2. **Un tema específico** — pregunta el tipo (pueblo costero, ciudad moderna, far west, suburbio, fantasía medieval) y propón.
3. **Lluvia de ideas** — propón 2-3 conceptos de town cortos; deja que elija/mezcle.
4. **Sorpréndeme** — elige TÚ un concepto fuerte y específico y dilo en 1 línea.
5. **Solo estoy probando** — un bloque pequeño (plaza + 2-3 edificios + 1 tienda).
6. **Planear primero** — plan SIN construir; espera su OK.
Confirma en 1 línea antes de arrancar. Si dice "hazlo ya", asume Sorpréndeme.

## 1. Lo que hace un town con vida (no slop)
- **Variedad de edificios:** distintas alturas, anchos, estilos y colores; nada de el mismo cubo-edificio clonado en grid. Fachadas con detalle (ventanas, puertas, letreros, toldos).
- **Calles y plazas con jerarquía:** una calle/plaza principal y secundarias; banquetas, cruces, mobiliario urbano (bancas, faroles, árboles, autos estacionados). Composición editorial, no retícula muerta.
- **Puntos de interés (roles):** lugares que invitan a jugar: casa, tienda, café, hospital, escuela, comisaría, parque. Interiores mínimos amueblados donde tenga sentido.
- **Escala y caminabilidad:** calles y puertas a escala humana; el jugador debe poder recorrer y entrar.
- **Ambiente acogedor:** luz cálida agradable (no terror), cielo bonito, algo de vegetación; sensación de comunidad.
- **Detalle de vida:** pequeñas escenas (mesas de café puestas, un puesto, ropa tendida) que sugieren que alguien vive ahí.

## 2. Construcción (con el MCP oficial)
1. `get_studio_state`. Trabaja en `Workspace/Town_<tema>`.
2. **Trazado:** calle/plaza principal + lotes; varía orientación y tamaño de lotes para evitar grid perfecto.
3. **Edificios:** construye 3-5 edificios distintos (varía altura/estilo/color/material) con fachadas detalladas; interiores mínimos donde aporte. Usa `generate_mesh`/`generate_material` para piezas/materiales y `search_asset`/`insert_asset` para mobiliario y props.
4. **Mobiliario urbano y vegetación:** faroles, bancas, árboles, autos, letreros; colócalos con variación (no clonados parejos).
5. **Puntos de rol:** marca/equipa al menos un par (tienda con mostrador, casa amueblada).
6. **Ambiente:** `Lighting` cálido agradable, skybox bonito, atmósfera ligera; spawn en la plaza.

## 3. Checklist técnico (aplica siempre)
- Carpeta nombrada; no borres lo del usuario; ChangeHistory waypoints.
- Evita z-fighting; `Color3`; paletas por edificio coherentes pero variadas; escala humana y caminable.
- Variación obligatoria: nada clonado en grid perfecto.
- Auto-revisión: `screen_capture` a nivel de calle; ¿se siente un lugar con vida, no cajas?; corrige, repite.
- Considera `start_stop_play` para caminarlo.

## 4. Cierre
Resume el town y sus puntos de interés. Ofrece: probar con `start_stop_play`, más edificios/interiores, NPCs que lo habiten (`/hugoblox:npc`), o sistemas/UI (`/hugoblox:game-ui`).

## Reglas duras
- Variedad sí o sí: edificios y props distintos, composición con jerarquía, nunca grid de clones.
- Escala humana y caminable; ambiente acogedor (no terror salvo que se pida).
- Empieza con un bloque pequeño con vida y crece. Si un asset falla, sigue sin romper y avísalo.
