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
  - **Tycoon en concreto**: el cash MANDA — contador grande y prominente arriba, botón `Rebirth` llamativo, botones de claim/upgrade claros con su costo y jerarquía obvia.
  - **Botones que saltan**: hover/press con escala y un pelín de overshoot (`TweenService`, `EasingStyle.Back`).
- **Brainrot (sim absurdo/meme, Italian brainrot, pet sim extremo)** — juguetón llevado al CAOS:
  - Colores que chocan, saturados al máximo; gradientes arcoíris (`UIGradient` animado); fondos con destellos/estrellitas. Más es más.
  - Números que suben RÁPIDO y enormes; multiplicadores bien visibles (`x2`, `x10`, `MEGA`); contadores de gemas/cash/multi.
  - Fuentes meme (`Bangers`, `Luckiest Guy`) gigantes con stroke grueso, a veces rainbow. Etiquetas absurdas y emojis.
  - Todo se MUEVE: pulsos constantes, wiggle, spin, popups "RARE!!"/"OMG" que estallan, partículas. Sobreestímulo = dopamina.
  - Ojo: lo importante (cash, botón principal) sigue legible entre el caos. El "limpio con gusto" aquí es un error.
- **Terror / horror (escalofriante, frío)** — lo OPUESTO al juguetón:
  - Minimal, oscuro, **desaturado**. Outlines finas o ninguna; esquinas rectas o radio pequeño.
  - Paleta fría y apagada (grises, azul muerto, un acento enfermo). Transparencias, grano sutil.
  - Tipografía condensada o serif inquietante; nada redondeado-feliz. Transiciones lentas, flicker, sin "bounce".
  - **Diegético** cuando se pueda: integra la UI en el mundo (`SurfaceGui` en pantallas/letreros sucios) para inmersión.
- **Competitivo / FPS / racing / fighting** — limpio, angular y de alta legibilidad (NO bland, NO chunky):
  - **Anatomía de HUD FPS**: vida+armadura (barra, abajo-izq), munición grande (abajo-der), crosshair central, minimapa (esquina), killfeed (arriba-der), marcador/timer (arriba-centro), hitmarker al pegar.
  - Esquinas rectas o bisel leve; números condensados/monoespaciados en bold; acentos neón sobre oscuro semitransparente; colores de equipo.
  - Animación seca y rápida (~0.08s), sin overshoot. Daño = flash rojo de borde/viñeta; matar = hitmarker + "+N" seco.
  - Minimal SÍ, pero con tensión y jerarquía clara, no el vacío de IA.
- **Cooperativo (dungeon, co-op survival, party)** — la UI gira en torno al EQUIPO:
  - Party frames: lista de compañeros con vida/estado/clase (esquina), color por jugador.
  - Objetivo compartido visible (progreso, contador), pings/markers, prompts de revivir ("Hold E to revive"), recursos compartidos.
  - Legible y funcional ante todo; el estilo puede ser chunky o limpio según el juego, pero la info de equipo nunca debe estorbar el gameplay.
- **Cute / pastel (cooking, pet care, café roleplay)** — tipo "DNA Shop":
  - Pastel (rosas, menta), bordes dobles o punteados (`UIStroke` + frame interno), todo muy redondeado y suave, fuentes redondas. Tierno, no oscuro.

Si no sabes el género, **pregúntalo o asume juguetón** (es lo que más juegos de Roblox quieren) antes de caer en el limpio-AI.

### Feedback de eventos (la "juice"), por género
Los estados de botón no bastan: cuando pasa algo importante (ganas dinero, encuentras un objeto, subes de nivel), la UI debe REACCIONAR. La intensidad va por género:
- **Juguetón (tycoon, obby, sim, pet):** es LO que engancha a los niños — premia cada logro con juice.
  - **Ganar dinero/puntos:** el contador **rueda** hacia el nuevo valor (tween del número, no salto seco), el pill de moneda da un **punch** de escala (1 → 1.2 → 1 con `Back`), y sale un **popup flotante "+50"** que sube y se desvanece. Opcional: íconos de moneda que estallan y vuelan hacia el pill, y un sonido corto. Color verde/dorado para ganar, rojo para perder.
  - **Logro grande (level up, rebirth, récord):** splash mayor — flash de pantalla, confeti/partículas, escala fuerte. Que se sienta recompensa.
- **Terror/horror:** lo OPUESTO, frío y simple. Recoger un objeto = una sola línea que aparece tenue en una esquina ("Old Key acquired."), fuente fría, SIN movimiento alegre, y se desvanece sola. Pérdida de cordura/vida = viñeta o desaturación sutil, nunca un popup feliz. El silencio incomoda.
- **Competitivo:** punzante pero limpio — hitmarker, "+10" rápido y seco, sin rebote.
- **Cute:** chispitas/sparkle suave, un bounce tierno.

Regla: el feedback debe ser **proporcional** al evento y **coherente** con el tono. Un "+1" no merece confeti; un rebirth sí. Implementa una función reutilizable (ej. `gainSplash(amount)`, `itemFound(name)`) y dispárala desde el evento real.

## 3. Construcción (con el MCP oficial)
1. `get_studio_state`. Crea `ScreenGui` en `StarterGui` (o `SurfaceGui` para UI en el mundo). Nombra todo claro.
2. **Tokens (según la dirección del género, §2):** decide paleta/tipografía/espaciado/grosor de outline. Usa `UICorner`, `UIPadding`, `UIStroke`, `UIGradient`, `UIListLayout`/`UIGridLayout`, `UIAspectRatioConstraint`. Para el look juguetón: `UIStroke` gruesa oscura + esquinas muy redondeadas + `UIGradient` vertical + sombra offset + fuente pesada, en TODO elemento.
3. **Componentes:** construye con `execute_luau` los elementos pedidos (HUD de stats, menú, tienda, etc.) con jerarquía y layout limpios.
4. **Estados/anim (DEBE ser funcional, no un mockup):** cada botón va wired en un `LocalScript` con `MouseEnter`/`MouseLeave` (hover) y `Activated` (click), y el click hace algo real. Intensidad de animación SEGÚN GÉNERO:
   - **Juguetón:** hover = escala +5-8% y brillo; press = escala -6% y rebote de vuelta (`TweenService` con `EasingStyle.Back`). Que se sienta "gomoso". Opcional: idle bounce sutil en el botón principal.
   - **Terror/horror:** SOLO hover sutil (un brillo tenue o un borde que aparece) para que el jugador vea que es clickeable; nada de rebotes ni escala alegre. Recuerda: el terror casi no usa UI — solo diálogos, prompts de objeto/compra, notas/inventario. No metas un HUD lleno donde no toca.
   - **Competitivo:** transiciones rápidas y secas (~0.08s), sin overshoot.
   - **Cute:** squish suave (escala Y leve) en press.
5. **Lógica:** conecta botones a su función (abrir/cerrar, comprar, etc.); para datos sensibles (compras, stats), valida en el SERVIDOR vía `RemoteEvent`/`RemoteFunction`.
6. **Responsivo:** verifica en distinto tamaño; usa escala, no solo offset.

## 4. Checklist técnico (aplica siempre)
- Trabaja en `StarterGui`/`SurfaceGui`; nombres claros; no borres UI existente del usuario.
- Acciones de juego (economía, stats) validadas en server, no en cliente.
- **`WaitForChild` solo a lo que de verdad va a existir** (RemoteEvents en `ReplicatedStorage`, `leaderstats`): esperar un hijo que NO existe **yieldea indefinidamente y cuelga el script** (los botones dejan de responder en silencio). Para elementos ya presentes en la GUI usa `FindFirstChild(name, true)`. Verifica en `start_stop_play` que los botones responden y revisa `get_console_output`.
- Consistencia de tokens; estados diseñados; contraste suficiente; layout responsivo (escala).
- Auto-revisión: `screen_capture`; ¿se ve diseñada (no default gris) y se lee?; corrige, repite.
- Considera `start_stop_play` para ver la UI en juego e interactuar.

## 5b. La UI DEBE ser funcional
Una UI bonita pero estática no sirve. Antes de declarar "listo":
- Cada botón está conectado en un `LocalScript`, con estados (hover/press) y una acción real.
- Pruébala en `start_stop_play`: los botones responden al cursor (hover) y al clic, y el clic hace lo suyo.
- Acciones sensibles (comprar, equipar, stats) van validadas en el SERVIDOR vía `RemoteEvent`/`RemoteFunction`.
Si entregas un mockup que no se puede clickear, no terminaste.

## 5. Cierre
Resume las pantallas/elementos creados. Ofrece: probar con `start_stop_play`, conectar a la lógica del juego, más pantallas, o ajustes de estilo.

## Reglas duras
- Nunca dejes el botón/elemento default crudo: color, esquinas, padding, estados.
- Sistema consistente (paleta/tipografía/espaciado) en toda la UI.
- Acciones sensibles validadas en server. Si algo falla, sigue sin romper y avísalo.
