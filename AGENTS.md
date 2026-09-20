# AGENTS.md

## Overview

Vanilla HTML5 canvas clone of Asteroids. No build system, no dependencies, no tests, no bundler. `index.html` loads `game.js` via a plain `<script src>` tag, so everything lives in global scope — do not convert to ES modules or add `import`/`export` without also changing `index.html`.

## Run / verify

Open `index.html` directly in a browser, or serve locally with `npx serve .`. There is no lint, typecheck, or test command — the only verification is manual play.

## Architecture notes

- Entities (`Bullet`, `Asteroid`, `Ship`, `Particle`) are ES6 classes; game state (score, lives, level, state machine) lives in module-global variables. `state` is one of `'playing' | 'dead' | 'gameover'`.
- Canvas dimensions are duplicated: the `W`/`H` constants at the top of `game.js` must stay in sync with the `width`/`height` attributes of the `<canvas>` in `index.html` (both 800×600).
- Removal idiom: set `entity.dead = true`, then filter arrays by `!dead` (never splice mid-iteration).
- Input uses `e.code` (keyboard-layout independent). `pressed(code)` is edge-triggered and clears the flag on read — call it at most once per frame per code.
- Asteroid sizes 1–3 index parallel arrays `RADII`/`SPEEDS`/`POINTS` (index 0 is a dummy).

## GitHub Actions

- `.github/workflows/opencode.yml` — ejecuta opencode cuando un comentario menciona `/oc` o `/opencode`.
- `.github/workflows/issue-triage.yml` — al crear un issue: asigna labels por palabras clave y pega al final del body un resumen generado con opencode, dejando el texto original del autor intacto (marca HTML `<!-- opencode-triage -->`). Toda la configuración vive dentro del propio workflow.

## Conventions

- All user-facing text is Spanish (`NIVEL`, `PUNTAJE`, `ESPACIO PARA REINICIAR`); keep new UI strings in Spanish.
- Section banners use `// ── Name ─────` comment separators.
