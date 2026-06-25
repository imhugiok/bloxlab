---
name: game-ui
description: Construye UI in-game para jugadores (HUD, menús, botones, tiendas, diálogos) de CALIDAD en el Roblox Studio abierto, vía el MCP oficial Roblox_Studio. Interfaces clickeables que no se ven genéricas. Úsalo cuando el usuario pida UI, HUD, menú o interfaz para el juego.
---

# /bloxlab:game-ui — Interfaces in-game que no se ven genéricas

Construyes UI que los jugadores ven y usan dentro del juego (HUD, menús, tiendas, diálogos, botones), con buen diseño. La calidad está en **jerarquía, consistencia y estados** (no el botón gris default de Roblox). **Antes de construir, lee y aplica** `${CLAUDE_PLUGIN_ROOT}/knowledge/anti-ai-slop.md` en clave UI: jerarquía, sistema de tokens (paleta/tipografía/espaciado), estados diseñados, y auto-revisión vía `screen_capture`. Si no puedes abrir el archivo (p. ej. en modo prueba local), aplica ese núcleo de memoria.

## 0. Pregunta primero (SIEMPRE, antes de construir)
NO empieces a construir. Pregunta qué quiere:
1. **Ya tengo algo en mente** — que describa qué UI y para qué juego; aterrízalo.
2. **Un tema/elemento específico** — pregunta qué pieza (HUD de stats, menú principal, tienda, inventario, diálogo, popup) y el estilo/colores, y propón.
3. **Lluvia de ideas** — propón 2-3 direcciones visuales cortas; deja que elija/mezcle.
4. **Sorpréndeme** — elige TÚ un estilo fuerte y coherente con el juego y dilo en 1 línea.
5. **Solo estoy probando** — un HUD simple o un botón/panel de muestra.
6. **Planear primero** — describe la UI (pantallas, jerarquía) SIN construir; espera su OK.
Confirma en 1 línea antes de arrancar. Si dice "hazlo ya", asume Sorpréndeme acorde al juego.

## 1. Principios de buena UI in-game (no slop)
- **Jerarquía:** lo importante grande y con contraste; lo secundario discreto. No todo del mismo tamaño/peso.
- **Sistema, no piezas sueltas:** define paleta (2-4 colores + neutros), tipografía (1-2 fuentes), radios, espaciado y úsalos consistentes en toda la UI.
- **Nada de defaults crudos:** evita el `TextButton` gris plano. Da color, esquinas redondeadas (`UICorner`), padding (`UIPadding`), borde/sombra sutil, íconos.
- **Estados:** hover/press/seleccionado/deshabilitado deben sentirse diseñados (cambio de color/escala suave con `TweenService`).
- **Legibilidad y contraste:** texto que se lee sobre cualquier fondo del juego; tamaños cómodos; respeta accesibilidad (contraste).
- **Responsivo:** usa `UDim2` con escala y `UIAspectRatioConstraint`/`UIListLayout`/`UIGridLayout` para que se vea bien en distintas pantallas (PC/móvil).
- **Diegético cuando aporta:** si encaja, integra UI en el mundo (`SurfaceGui` en pantallas/letreros) para inmersión.

## 2. Dirección de UI por género (el vibe correcto, NO el look de IA)
**El tell de IA en Roblox NO es feo: es el look limpio-minimalista corporativo** (mucho aire, un solo acento, trazos finos, gris/blanco "tasteful"). Eso se ve vacío y genérico en un juego de Roblox. La mayoría de los juegos quieren lo contrario: CHUNK con personalidad. Match el estilo al género del juego:

- **Juguetón / arcade (obby, simulator, tycoon, pet, brainrot)** — el look dominante de Roblox. Maximalista y "gomoso":
  - **Outline gruesa oscura en TODO** (`UIStroke` ~2-4px, color casi negro/marrón muy oscuro, `Transparency` ~0.1). Es LA firma del estilo.
  - **Esquinas muy redondeadas** (`UICorner` ~10-20).
  - **Drop shadow real**: un duplicado oscuro detrás con offset (o `ImageLabel` de sombra), no una sombra tímida.
  - **Fills saturados** + `UIGradient` vertical leve (más claro arriba → base abajo) para dar volumen.
  - **Color por categoría/rareza**: cada card/botón con su color fuerte (rojo, verde, azul, morado, amarillo).
  - **Fuentes pesadas**: `GothamBlack`/`FredokaOne`/`Bangers`/`Luckiest Guy` para títulos; `GothamBold` para botones. Texto con su propio `UIStroke` oscuro.
  - **Componentes típicos**: pill de moneda con botón `+`, stack de botones laterales (cada uno de color distinto), tabs arriba del panel, grid de cards (`UIGridLayout`) icono+label, barra de progreso, X roja para cerrar.
  - **Botones que saltan**: hover/press con escala y un pelín de overshoot (`TweenService`, `EasingStyle.Back`).
- **Terror / horror (escalofriante, frío)** — lo OPUESTO al juguetón:
  - Minimal, oscuro, **desaturado**. Outlines finas o ninguna; esquinas rectas o radio pequeño.
  - Paleta fría y apagada (grises, azul muerto, un acento enfermo). Transparencias, grano sutil.
  - Tipografía condensada o serif inquietante; nada redondeado-feliz. Transiciones lentas, flicker, sin "bounce".
  - **Diegético** cuando se pueda: integra la UI en el mundo (`SurfaceGui` en pantallas/letreros sucios) para inmersión.
- **Competitivo / moderno (FPS, racing HUD, fighting)** — limpio PERO con intención (no default):
  - Angular, alto contraste, acentos neón sobre oscuro; números grandes y legibles (munición, vueltas, vida). Aquí sí cabe el minimal, pero con tensión y un acento fuerte, no bland.
- **Cute / pastel (cooking, pet care, café roleplay)** — tipo "DNA Shop":
  - Pastel (rosas, menta), bordes dobles o punteados (`UIStroke` + frame interno), todo muy redondeado y suave, fuentes redondas. Tierno, no oscuro.

Si no sabes el género, **pregúntalo o asume juguetón** (es lo que más juegos de Roblox quieren) antes de caer en el limpio-AI.

## 3. Construcción (con el MCP oficial)
1. `get_studio_state`. Crea `ScreenGui` en `StarterGui` (o `SurfaceGui` para UI en el mundo). Nombra todo claro.
2. **Tokens (según la dirección del género, §2):** decide paleta/tipografía/espaciado/grosor de outline. Usa `UICorner`, `UIPadding`, `UIStroke`, `UIGradient`, `UIListLayout`/`UIGridLayout`, `UIAspectRatioConstraint`. Para el look juguetón: `UIStroke` gruesa oscura + esquinas muy redondeadas + `UIGradient` vertical + sombra offset + fuente pesada, en TODO elemento.
3. **Componentes:** construye con `execute_luau` los elementos pedidos (HUD de stats, menú, tienda, etc.) con jerarquía y layout limpios.
4. **Estados/anim:** hover/press/transiciones con `TweenService`; feedback al clic.
5. **Lógica:** conecta botones a su función (abrir/cerrar, comprar, etc.); para datos sensibles (compras, stats), valida en el SERVIDOR vía `RemoteEvent`/`RemoteFunction`.
6. **Responsivo:** verifica en distinto tamaño; usa escala, no solo offset.

## 4. Checklist técnico (aplica siempre)
- Trabaja en `StarterGui`/`SurfaceGui`; nombres claros; no borres UI existente del usuario.
- Acciones de juego (economía, stats) validadas en server, no en cliente.
- **`WaitForChild` solo a lo que de verdad va a existir** (RemoteEvents en `ReplicatedStorage`, `leaderstats`): esperar un hijo que NO existe **yieldea indefinidamente y cuelga el script** (los botones dejan de responder en silencio). Para elementos ya presentes en la GUI usa `FindFirstChild(name, true)`. Verifica en `start_stop_play` que los botones responden y revisa `get_console_output`.
- Consistencia de tokens; estados diseñados; contraste suficiente; layout responsivo (escala).
- Auto-revisión: `screen_capture`; ¿se ve diseñada (no default gris) y se lee?; corrige, repite.
- Considera `start_stop_play` para ver la UI en juego e interactuar.

## 5. Cierre
Resume las pantallas/elementos creados. Ofrece: probar con `start_stop_play`, conectar a la lógica del juego, más pantallas, o ajustes de estilo.

## Reglas duras
- Nunca dejes el botón/elemento default crudo: color, esquinas, padding, estados.
- Sistema consistente (paleta/tipografía/espaciado) en toda la UI.
- Acciones sensibles validadas en server. Si algo falla, sigue sin romper y avísalo.
