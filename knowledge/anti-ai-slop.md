# Anti AI-Slop: principios para que un juego de Roblox NO parezca hecho con IA

Conocimiento compartido que todos los skills deben respetar. Lo que sigue es la diferencia entre "se ve generado automáticamente" y "se ve hecho por alguien con criterio".

## 1. Mata la uniformidad
La señal #1 de IA es la regularidad perfecta: objetos en grid, mismo espaciado, misma rotación, mismo tamaño.
- Varía posición, rotación (Y aleatoria), y escala dentro de un rango.
- Agrupa en clusters irregulares en vez de repartir parejo.
- Rompe las líneas rectas: desalinea, superpone, deja huecos intencionales.

## 2. La atmósfera vende más que los objetos
Un cuarto vacío con buena luz/niebla se ve mejor que uno lleno con luz plana.
- Baja `Lighting.Brightness`, usa `Technology = "Future"`, sube `ShadowSoftness`.
- Agrega `Atmosphere` (Density, Haze, Glare) y/o niebla (`FogEnd`).
- `ColorCorrectionEffect`: desatura un poco (`Saturation` negativo) y tinta sutil según el mood.
- Pocas luces, bien puestas (parpadeo, contraluz, charcos de luz en oscuridad) > muchas luces planas.

## 3. Color con intención (no arcoíris)
- Usa `Color3` (RGB), nunca `BrickColor` por defecto.
- Paleta acotada y coherente (3-5 colores + neutros). Define el mood antes de pintar.
- Evita el gris default y los colores saturados de juguete salvo que el estilo lo pida.

## 4. Jerarquía y foco
- Que haya un punto focal claro y elementos secundarios, no todo con el mismo peso.
- Contraste de escala: algo grande que ancla la vista, detalles pequeños que premian mirar de cerca.

## 5. Escala humana real (en studs)
- Personaje ~5 studs de alto. Puertas ~7-10 studs. Techos de interior ~10-14.
- Pasillos de terror: angostos (8-12 de ancho) para tensión; espacios de alivio más abiertos.
- Nada flotando sin razón; todo `Anchored` salvo lo que deba moverse.

## 6. Imperfección intencional
- Desgaste, manchas, objetos volcados, asimetría. Lo "perfecto y limpio" se siente falso/IA.
- Mezcla materiales (Concrete, Metal, Wood, Grass) en vez de un solo material plano.

## 7. Sonido y movimiento dan vida
- Ambiente (drone, viento, zumbido) en loop. Stingers ocasionales en terror.
- Micro-movimiento: luces que parpadean, partículas de polvo, niebla que fluye.
- (Nota: los IDs de sonido/asset deben ser válidos y verificados; si no, omitir antes que romper.)

## 8. Referencias reales, no genéricas
- Piensa en un referente concreto (una peli, un juego, un lugar real) y aterrízalo, en vez de "un cuarto de terror genérico".

## 9. Auto-revisión obligatoria
- Antes de declarar "listo": `screen_capture`, mírate el resultado con ojo crítico contra esta lista, y corrige al menos una cosa.
- Pregúntate: "¿esto pasaría por hecho por un dev humano con buen gusto?". Si no, itera.

## 10. Seguridad y limpieza
- Construye dentro de una carpeta nombrada (ej. `Workspace/<NombreDelMapa>`).
- No borres el trabajo existente del usuario. Usa waypoints de ChangeHistory cuando se pueda para que el undo funcione.

## 11. Gotchas técnicos de Roblox (probados en build real vía MCP)
Lecciones de correr los skills en Studio. Aplican a CUALQUIER skill que construya con `execute_luau`:
- **`Lighting.Technology` no se puede leer ni escribir** desde `execute_luau` ("lacking capability RobloxScript"); el intento aborta el script. NUNCA la setees por código. Envuelve TODOS los writes de `Lighting` en `pcall` para que un fallo no tumbe el build.
- **Calibra la luz empíricamente y según el MOOD, no por números fijos.** El render depende de la tecnología del lugar (no la controlas) y del ambiente que buscas. Terror oscuro: `Ambient` bajo (~rgb(42,44,52)) + charcos de luz (`PointLight` `Brightness` ~3, `Range` ~36, casi sin sombras). Liminal/brillante (backrooms, oficinas, hospital): `Ambient` ALTO (~rgb(120,120,90) o más), `EnvironmentDiffuseScale` ~1, luz plana y pareja sin sombras. En ambos casos `Brightness` global ~2.2-3, y si sale casi negro SUBE estos valores antes de rendirte. Itera con `screen_capture` hasta que las superficies se lean.
- **`Reflectance` alta = espejo blanco.** `Reflectance` alto + `Glass` refleja el ambiente como un espejo blanco brillante (peor sin `Future`). Para agua/charcos: `Reflectance` ~0.1-0.15, color oscuro, `Transparency` ~0.4, material `SmoothPlastic`; verifica en captura.
- **Z-fighting con el baseplate:** no construyas el piso a `y=0` (parpadeo/manchas). Construye elevado (ej. base en `y=20`) o lejos del origen; eso además te da espacio vertical para capas (trincheras, sótanos).
- **Spawn:** si construyes elevado, agrega una `SpawnLocation` dentro del mapa (sobre el piso) o el jugador aparece en el baseplate vacío. Desactiva (`Enabled=false`) la SpawnLocation default si estorba.

## 12. Protocolo de fallo y rollback (no rompas la escena del usuario)
Cómo comportarte cuando algo sale mal a mitad del build. Aplica a TODOS los skills:
- **Antes de tocar nada:** trabaja SIEMPRE dentro de una carpeta nombrada (`Workspace/<Nombre>`), nunca sueltes partes en la raíz. Pon un `ChangeHistoryService:SetWaypoint("<Nombre> start")` al empezar (en `pcall`) para que el Ctrl+Z del usuario funcione.
- **Aísla el riesgo:** envuelve en `pcall` toda operación que pueda fallar (writes de `Lighting`, `generate_mesh`/`generate_material`, `insert_asset`). Si una falla, NO abortes el resto: registra el fallo y sigue con lo que sí se puede.
- **Construye en pasos verificables** (blockout → atmósfera → detalle), no en un solo script gigante. Así un fallo deja un mapa parcial pero coherente, no un revoltijo a medias.
- **Nunca inventes IDs** de asset/sonido/decal. Si no tienes uno válido y verificado, omite esa pieza antes que romper o meter un ID falso.
- **Nunca borres el trabajo existente del usuario.** Al re-construir, borra solo TU propia carpeta nombrada.
- **Si algo falla:** deja la escena en estado coherente (sin partes huérfanas a medio hacer) y dile al usuario en 1-2 líneas: qué se construyó, qué falló y por qué, y cómo deshacer (Ctrl+Z, o borrar `Workspace/<Nombre>`). No declares "listo" sobre algo roto.
- **Verifica antes de cerrar:** `screen_capture` siempre; si corriste scripts en play, revisa también `get_console_output` por errores de runtime.

## 13. UI in-game: según el género, no limpia-AI
Cualquier HUD/menú/tienda/diálogo que construyas: el look **limpio-minimalista corporativo es el tell de IA** en Roblox (se ve vacío y genérico). Hazlo según el género: por defecto **chunky juguetón** (outline gruesa oscura en `UIStroke`, esquinas muy redondeadas, `UIGradient` vertical, sombra offset, fuentes pesadas con stroke, color por categoría/rareza); frío/minimal/desaturado para terror; pastel y redondo para cute. Nunca dejes el `TextButton` gris crudo. Guía completa por género en el skill `game-ui`.
