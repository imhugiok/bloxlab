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
