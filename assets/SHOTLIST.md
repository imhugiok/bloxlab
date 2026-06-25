# Shot list — README hero + gallery

Capturas para el README. **Claude prepara cada escena** (lighting correcto, cámara, oculta spawns) justo antes de que captures; tú tomas la captura en Studio (mejor resolución) y guardas el PNG con el nombre exacto de abajo en `assets/`. Luego Claude cablea el README y commitea imágenes + README juntos.

Para que Claude prepare una escena, dile: "prep metro", "prep backrooms", "prep obby", o para las UI "prep ui <nombre>".

## Cómo capturar limpio en Studio
- Ocultar gizmos: View → desmarca los overlays, o captura en modo Play (las UI van en Play sí o sí).
- Resolución: ventana lo más grande posible; recorta después si hace falta.
- Mundos: en modo Edit con la cámara colocada; UI: en Play.

## Hero
| Archivo | Qué es |
|---|---|
| `assets/hero.png` | (definir estilo: screenshot fuerte / banner diseñado / montaje) |

## Worlds (la capa de calidad)
| Archivo | Escena | Encuadre (cámara aprox. que usó Claude) |
|---|---|---|
| `assets/world-horror-metro.png` | `Workspace/HorrorMap_Metro` | andén → túnel; cam pos `[277,22,-5]` look `[348,17.5,8]` |
| `assets/world-backrooms.png` | `Workspace/Backrooms_L0` | pilares + paneles, sensación infinita; cam pos `[-555,26,-6]` look `[-458,23,-95]` |
| `assets/world-obby.png` | `Workspace/Obby_Neon` | secuencia de plataformas neón; cam pos `[188,60,318]` look `[260,50,305]` |

## UI por género (el diferenciador)
Todas en modo Play. Claude activa solo el ScreenGui correcto antes de cada una.
| Archivo | UI | Nota |
|---|---|---|
| `assets/ui-before-after.png` | limpio-AI vs juguetón | montaje lado a lado (las dos versiones del shop) |
| `assets/ui-shop-playful.png` | `ShopHUD` (juguetón) | pet shop chunky con cards por rareza |
| `assets/ui-shop-splash.png` | `ShopHUD` + "+75" | el splash de dinero (juice) |
| `assets/ui-horror-dialogue.png` | `HorrorUI` | caja de diálogo + prompt de objeto, frío |
| `assets/ui-fps.png` | `FPS_HUD` | crosshair, vida/munición/minimapa/killfeed |
| `assets/ui-brainrot.png` | `Brainrot_HUD` | caos meme: multi, RARE!!, cash |
| `assets/ui-coop.png` | `Coop_HUD` | party frames + objetivo + revivir |

## README gallery (markdown listo para cablear cuando existan los PNGs)
```md
## Gallery

### Worlds — the quality layer
| Horror | Backrooms | Obby |
|---|---|---|
| ![Abandoned metro horror map](assets/world-horror-metro.png) | ![Backrooms liminal level](assets/world-backrooms.png) | ![Neon obby](assets/world-obby.png) |

### UI, matched to the genre (not generic AI UI)
| Playful shop | Horror dialogue | FPS HUD |
|---|---|---|
| ![Playful Roblox shop UI](assets/ui-shop-playful.png) | ![Cold horror dialogue UI](assets/ui-horror-dialogue.png) | ![Competitive FPS HUD](assets/ui-fps.png) |

| Brainrot HUD | Co-op party frames | Money splash |
|---|---|---|
| ![Brainrot meme HUD](assets/ui-brainrot.png) | ![Cooperative party HUD](assets/ui-coop.png) | ![Coin gain splash](assets/ui-shop-splash.png) |
```
