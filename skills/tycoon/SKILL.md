---
name: tycoon
description: Construye un tycoon (compra-y-genera-dinero por droppers/botones) de CALIDAD en el Roblox Studio abierto, vía el MCP oficial Roblox_Studio. Bucle de progresión satisfactorio, sin look de IA. Úsalo cuando el usuario pida un tycoon.
---

# /hugoblox:tycoon — Tycoon con progresión satisfactoria

Construyes un tycoon: el jugador reclama una base, compra mejoras con botones, y un bucle de **dinero → comprar → producir más** lo engancha. La calidad está en que el **bucle se sienta bien** y la base no parezca cubos grises. Aplica anti-AI-slop (`knowledge/anti-ai-slop.md`).

## 0. Pregunta primero (SIEMPRE, antes de construir)
NO empieces a construir. Pregunta qué quiere:
1. **Ya tengo algo en mente** — que describa tema/producto/escala; aterrízalo.
2. **Un tema específico** — pregunta qué produce el tycoon (pizza, autos, lava, dulces, armas, dinero abstracto) y propón.
3. **Lluvia de ideas** — propón 2-3 temas de tycoon cortos; deja que elija/mezcle.
4. **Sorpréndeme** — elige TÚ un tema fuerte y específico y dilo en 1 línea.
5. **Solo estoy probando** — una base mínima (1 dropper + 1 colector + 2 botones).
6. **Planear primero** — plan SIN construir; espera su OK.
Confirma en 1 línea antes de arrancar. Si dice "hazlo ya", asume Sorpréndeme.

## 1. Anatomía de un buen tycoon
- **El bucle:** dropper produce objetos → caen a un colector (conveyor) → suman dinero → con dinero compras botones que mejoran/agregan droppers → produces más. El bucle debe ser claro y recompensar pronto (primera compra barata y rápida).
- **Claim base:** un pad para reclamar la base (uno por jugador). Datos de dinero por jugador (`leaderstats`).
- **Botones de compra:** pads con precio y nombre; al pisar y tener dinero, descuentan y revelan la siguiente parte (dropper mejor, pared, decoración, etc.). Progresión visible: la base "crece".
- **Balance:** precios y producción escalados para que siempre haya una "siguiente meta" alcanzable, sin muros eternos.
- **No-slop:** la base con tema y estilo (no cubos grises): estética del producto, colores de marca, props temáticos, buena luz. Que se vea como un lugar, no un prototipo.

## 2. Construcción (con el MCP oficial)
1. `get_studio_state`. Trabaja en `Workspace/Tycoon_<tema>`.
2. **leaderstats:** script de servidor que crea `leaderstats` con `Cash` (o moneda temática) al unirse el jugador.
3. **Dropper + conveyor + colector (execute_luau):** dropper que `Instance.new` partes cada X seg; conveyor con `AssignVelocity`/`.Velocity` o tween; colector con `.Touched` que suma al `Cash` del dueño y destruye el objeto.
4. **Botones de compra:** pads con `BillboardGui`/`SurfaceGui` mostrando precio; `.Touched` valida dueño y dinero, descuenta y hace `Visible`/`Parent` la parte comprada. Encadena la progresión.
5. **Claim + dueño:** pad de claim asigna la base a un jugador; guarda quién es el dueño para validar compras.
6. **Tema/estética:** materiales y colores del tema, props con `search_asset`/`insert_asset`, piezas con `generate_mesh`, luz agradable. Layout ordenado y legible.

## 3. Checklist técnico (aplica siempre)
- Carpeta nombrada; no borres lo del usuario; ChangeHistory waypoints.
- Scripts de servidor para economía (no cliente) para evitar trampas; valida dueño y fondos en el server.
- Evita z-fighting; `Color3`; escala humana; UI legible en los botones.
- Auto-revisión: `screen_capture` de la base; ¿se ve como un lugar con tema, no cubos?; corrige, repite.
- Considera `start_stop_play` para verificar el bucle de dinero.

## 4. Cierre
Resume el bucle y la base. Ofrece: probar con `start_stop_play`, añadir más niveles de upgrades, rebirth/prestigio, o UI con `/hugoblox:game-ui`.

## Reglas duras
- Economía en el servidor; primera compra barata para enganchar.
- La base debe tener tema y verse intencional, no cubos grises.
- Empieza con el bucle mínimo funcional y crece. Si algo falla, sigue sin romper y avísalo.
