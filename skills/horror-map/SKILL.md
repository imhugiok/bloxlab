---
name: horror-map
description: Construye una sección de mapa de terror de CALIDAD en el Roblox Studio abierto, usando el MCP oficial Roblox_Studio. Atmósfera real, sin look de IA. Úsalo cuando el usuario pida un mapa/cuarto/nivel de terror.
---

# /horror-map — Mapa de terror de calidad

Construyes terror que da miedo de verdad y NO parece hecho con IA, dentro del Roblox Studio abierto del usuario, usando las herramientas del MCP oficial `Roblox_Studio`.

Sigue SIEMPRE los principios de `knowledge/anti-ai-slop.md` y el intake de `knowledge/intake.md`: mata la uniformidad, atmósfera primero, color con intención, escala humana, imperfección, auto-revisión. El miedo viene del **ritmo y la atmósfera**, no de la cantidad de objetos.

## 0. Pregunta primero (SIEMPRE, antes de construir)
Al invocar este skill NO empieces a construir. Primero pregunta qué quiere, con estas opciones:
1. **Ya tengo algo en mente** — que describa tema/referencia/mecánicas/tamaño; aterrízalo.
2. **Un tema específico** — pregunta el setting (hospital, sótano, bosque, instalación) y propón.
3. **Lluvia de ideas** — propón 2-3 conceptos de terror cortos y específicos; deja que elija/mezcle.
4. **Sorpréndeme** — elige TÚ un concepto fuerte y específico (no genérico) y dilo en 1 línea.
5. **Solo estoy probando** — construye una muestra pequeña y rápida (un cuarto + pasillo).
6. **Planear primero** — entrega un plan SIN construir y espera su OK.
Espera la respuesta y confirma en 1 línea qué vas a hacer. Si dice "hazlo ya", asume Sorpréndeme con calidad.

## 1. Verifica el entorno
1. Verifica que hay un Studio conectado: `get_studio_state` (o `list_roblox_studios`). Si no, dilo y para.
2. Tamaño por defecto: una sección jugable (~1-3 cuartos + pasillos), no un mapa entero de golpe.
3. Trabaja dentro de una carpeta nombrada en `Workspace` (ej. `HorrorMap_<setting>`). NO borres nada existente del usuario.

## 1. Diseña el espacio para el miedo (antes de construir)
- **Gradiente seguro→inseguro:** empieza con un punto algo iluminado y lleva al jugador hacia lo oscuro.
- **Pasillos angostos (8-12 studs)** que cortan la línea de visión (esquinas, recodos) para que no se vea lo que viene.
- **Callejones sin salida y bucles** para desorientar. Un landmark memorable para orientarse.
- **Espacios de alivio** ocasionales (un cuarto más abierto) para que el siguiente apretón asuste más.
- Escala humana real (techos 10-14 studs, puertas ~7-10).

## 2. Blockout (con execute_luau)
- Crea piso, muros, techo `Anchored`, con dimensiones reales y paleta oscura coherente en `Color3` (no BrickColor).
- Mezcla materiales (Concrete, Metal, CrackedLava/Wood según setting). Rompe la uniformidad: muros con grosores/alturas ligeramente variados, alguna columna o escombro.
- Ejecuta en pasos verificables; pon waypoints con `ChangeHistoryService:SetWaypoint` para que el undo del usuario funcione.

## 3. Atmósfera (la palanca #1 — no te la saltes)
Con `Technology = "Future"` los interiores quedan NEGROS si el ambient es muy bajo. Valores que SÍ se leen y siguen dando miedo:
- `Lighting`: `Brightness` ~1.4, `Technology = "Future"`, `Ambient` ~rgb(22,22,27) (no negro puro, o no ves las paredes), `OutdoorAmbient` ~rgb(16,16,20), `EnvironmentDiffuseScale` ~0.45-0.5, `ClockTime = 0`.
- Niebla: `FogStart` ~14, `FogEnd` ~110-130, `FogColor` oscuro. O un `Atmosphere` (`Density` ~0.28, `Haze` ~1.3).
- `ColorCorrectionEffect`: `Saturation` ~-0.26, `Contrast` ~0.05, `TintColor` frío (azul/verde) o cálido enfermizo según mood. No exageres el contraste (quema el piso).
- Luces puntuales = **charcos de luz** ESCASOS: la mayoría SIN sombras (`Shadows = false`) y suaves (`Brightness` ~0.6, `Range` ~22), una fila cada ~16-20 studs para que el pasillo se lea con huecos oscuros intencionales. **Como mucho 1-2 luces con `Shadows = true`** para drama; si todas proyectan sombra, el piso se llena de ruido feo.
- **Guarda los valores originales de `Lighting`** antes de cambiarlos (para poder restaurar), y nombra tus efectos (`HorrorMap_*`) para borrarlos fácil. `Lighting` es global: afecta todo el lugar.

## 4. Detallado (set-dressing)
- `search_asset` + `insert_asset` para props coherentes (cajas, tuberías, muebles rotos, barriles). Colócalos con rotación/escala variada y en clusters, NO en grid.
- `generate_mesh` / `generate_material` para piezas hero o materiales custom (ej. una textura de pared sucia, un objeto central inquietante) cuando un asset no alcance.
- Premia mirar de cerca: pequeños detalles (manchas, papeles, sangre seca con decals válidos) en puntos focales.

## 5. Sonido y movimiento (si hay IDs válidos)
- Ambiente en loop (drone/viento) vía un `Sound` en un punto o en `SoundService`. Si no tienes un ID válido, omítelo antes que romper.
- Micro-movimiento: parpadeo de luces, partículas de polvo/niebla (`ParticleEmitter` sutil).

## 6. Auto-revisión OBLIGATORIA
- `screen_capture` desde dentro del mapa. Míralo con ojo crítico contra `anti-ai-slop.md`.
- Corrige al menos: uniformidad sobrante, luz demasiado plana, escala rara, vacío sin foco.
- Repite captura hasta que pasaría por hecho por un humano con buen gusto.

## 7. Cierre
- Resume qué construiste y dónde (ruta en el Explorer).
- Ofrece: probar en juego (`start_stop_play`), añadir mecánicas (llaves/puertas/monstruo), o expandir el mapa.

## Checklist técnico (lecciones de pruebas reales)
Errores que se ven feo y cómo evitarlos a la primera:
- **Z-fighting con el baseplate:** si construyes el piso a `y=0` y el lugar tiene baseplate a `y=0`, las dos superficies parpadean (piso "quemado" con manchas blancas/negras). Construye con el piso un poco por encima (top en ~`y=0.5`) o lejos del origen. Si ves manchas blancas raras en el piso, es esto: súbelo.
- **Todo negro:** subiste poco el ambient. Sube `Ambient` y `EnvironmentDiffuseScale`, y dale `Range` generoso a las luces.
- **Ruido de sombras duro:** demasiadas luces con `Shadows = true`. Déjalas casi todas en `false`.
- **Props que flotan como picos:** cilindros largos y delgados (tubos) en perspectiva se ven como estacas flotando. Hazlos gruesos y pegados a la superficie, y NO los pongas hasta que el espacio ya se lea bien; verifica en captura.
- **Itera con `screen_capture`:** 2-4 pasadas, arreglando UN problema por pasada (lee → ajusta → vuelve a capturar). No declares "listo" sin una captura que pasaría por trabajo humano.

## Reglas duras
- Una sección a la vez, no el mapa entero de un tiro.
- Nunca borres el trabajo existente del usuario.
- Si una generación/asset falla, sigue sin romper y avísalo.
- Calidad > cantidad: mejor poco con atmósfera que mucho plano.
