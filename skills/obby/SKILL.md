---
name: obby
description: Construye un obby (carrera de obstáculos/parkour) de CALIDAD en el Roblox Studio abierto, vía el MCP oficial Roblox_Studio. Dificultad justa, checkpoints, sin look de IA. Úsalo cuando el usuario pida un obby, parkour o curso de obstáculos.
---

# /bloxlab:obby — Carrera de obstáculos justa y divertida

Construyes un obby con **game feel justo**: retador pero nunca tramposo, con progresión clara y checkpoints. Aplica anti-AI-slop (`knowledge/anti-ai-slop.md`): nada de retícula plana y gris; tema, color y ritmo intencionales.

## 0. Pregunta primero (SIEMPRE, antes de construir)
NO empieces a construir. Pregunta qué quiere:
1. **Ya tengo algo en mente** — que describa tema/dificultad/largo; aterrízalo.
2. **Un tema específico** — pregunta el tema (lava, cielo/nubes, neón, jungla, hielo, candy) y propón.
3. **Lluvia de ideas** — propón 2-3 temas+gimmicks cortos; deja que elija/mezcle.
4. **Sorpréndeme** — elige TÚ un tema fuerte y específico y dilo en 1 línea.
5. **Solo estoy probando** — un tramo corto (5-8 obstáculos + 1 checkpoint).
6. **Planear primero** — plan SIN construir; espera su OK.
Confirma en 1 línea antes de arrancar. Si dice "hazlo ya", asume Sorpréndeme.

## 1. Lo que hace un buen obby (no slop)
- **Dificultad progresiva:** empieza fácil para enganchar, sube gradual. Alterna picos de tensión con descansos.
- **Justo, no tramposo:** saltos siempre alcanzables (separación ~ jugador salta ~ varios studs; deja margen). Nada de saltos a ciegas o de fe sin pista visual.
- **Checkpoints:** cada N obstáculos un checkpoint (SpawnLocation o pad) que reposiciona; sin esto frustra. Numera las etapas.
- **Variedad de gimmicks:** plataformas que desaparecen, móviles (TweenService), kill-bricks (lava/Touched → reset), trampolines, paredes giratorias, tirolesas. No repitas el mismo obstáculo.
- **Lectura visual:** color codifica peligro (rojo = mata, verde = seguro/checkpoint). El camino correcto debe leerse a primera vista.
- **Tema y composición:** no una línea recta gris flotando; dale tema, fondo, niveles de altura, vistas. Skybox/atmósfera acorde.

## 2. Construcción (con el MCP oficial)
1. `get_studio_state`. Trabaja en `Workspace/Obby_<tema>`.
2. **Ruta:** define una línea jugable con altura variada (no todo plano), agrupada por etapas. Plataformas `Anchored`, tamaños cómodos (no pixel-perfect).
3. **Obstáculos con scripts (execute_luau):** kill-bricks (`.Touched` → `Humanoid.Health=0` o teleport a último checkpoint), plataformas móviles (`TweenService`), desaparecedoras (transparencia/CanCollide por tiempo). Scripts limpios y comentados.
4. **Checkpoints:** `SpawnLocation` por etapa o un sistema que guarde el último pad tocado y reposicione al morir.
5. **Tema:** material/color por tema (Neon para peligro/decoración), skybox y `Lighting` acorde, props de fondo con `search_asset`/`insert_asset`, o piezas con `generate_mesh`.
6. **Game feel:** prueba mentalmente cada salto; deja márgenes. Considera `start_stop_play` para verificar.

## 3. Checklist técnico (aplica siempre)
- Carpeta nombrada; no borres lo del usuario; ChangeHistory waypoints.
- Evita z-fighting con el baseplate (sube el build o constrúyelo en el aire/lejos del origen).
- `Color3`; color semántico (rojo=mata, verde=seguro); escala humana.
- Saltos verificados y alcanzables; siempre con checkpoint reciente.
- Auto-revisión: `screen_capture`, ¿se lee la ruta y el peligro?, corrige, repite (2-4 pasadas).

## 4. Cierre
Resume etapas/gimmicks y dónde quedó. Ofrece: probar con `start_stop_play`, añadir más etapas, o una meta/recompensa final.

## Reglas duras
- Justo siempre: cada salto alcanzable, cada muerte con checkpoint cerca.
- Variedad: no repitas el mismo obstáculo seguido.
- Una sección de etapas a la vez. Si un asset/script falla, sigue sin romper y avísalo.
