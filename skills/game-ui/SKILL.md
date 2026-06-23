---
name: game-ui
description: Construye UI in-game para jugadores (HUD, menús, botones, tiendas, diálogos) de CALIDAD en el Roblox Studio abierto, vía el MCP oficial Roblox_Studio. Interfaces clickeables que no se ven genéricas. Úsalo cuando el usuario pida UI, HUD, menú o interfaz para el juego.
---

# /hugoblox:game-ui — Interfaces in-game que no se ven genéricas

Construyes UI que los jugadores ven y usan dentro del juego (HUD, menús, tiendas, diálogos, botones), con buen diseño. La calidad está en **jerarquía, consistencia y estados** (no el botón gris default de Roblox). Aplica anti-AI-slop (`knowledge/anti-ai-slop.md`) en clave UI.

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

## 2. Construcción (con el MCP oficial)
1. `get_studio_state`. Crea `ScreenGui` en `StarterGui` (o `SurfaceGui` para UI en el mundo). Nombra todo claro.
2. **Tokens:** decide paleta/tipografía/espaciado y aplícalos consistentes. Usa `UICorner`, `UIPadding`, `UIStroke`, `UIListLayout`/`UIGridLayout`, `UIAspectRatioConstraint`.
3. **Componentes:** construye con `execute_luau` los elementos pedidos (HUD de stats, menú, tienda, etc.) con jerarquía y layout limpios.
4. **Estados/anim:** hover/press/transiciones con `TweenService`; feedback al clic.
5. **Lógica:** conecta botones a su función (abrir/cerrar, comprar, etc.); para datos sensibles (compras, stats), valida en el SERVIDOR vía `RemoteEvent`/`RemoteFunction`.
6. **Responsivo:** verifica en distinto tamaño; usa escala, no solo offset.

## 3. Checklist técnico (aplica siempre)
- Trabaja en `StarterGui`/`SurfaceGui`; nombres claros; no borres UI existente del usuario.
- Acciones de juego (economía, stats) validadas en server, no en cliente.
- Consistencia de tokens; estados diseñados; contraste suficiente; layout responsivo (escala).
- Auto-revisión: `screen_capture`; ¿se ve diseñada (no default gris) y se lee?; corrige, repite.
- Considera `start_stop_play` para ver la UI en juego e interactuar.

## 4. Cierre
Resume las pantallas/elementos creados. Ofrece: probar con `start_stop_play`, conectar a la lógica del juego, más pantallas, o ajustes de estilo.

## Reglas duras
- Nunca dejes el botón/elemento default crudo: color, esquinas, padding, estados.
- Sistema consistente (paleta/tipografía/espaciado) en toda la UI.
- Acciones sensibles validadas en server. Si algo falla, sigue sin romper y avísalo.
