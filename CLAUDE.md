# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A collection of browser-based games and web projects, each as a single self-contained HTML file (no build step, no dependencies, no server required). Open any file directly in a browser to run it.

## Running Projects

```bash
open tictactoe.html
open duckshooter.html
```

## Git & GitHub Workflow

Remote: `https://github.com/rehaabseyani/claude-code-projects`
Branch: `main`
Auth: GitHub CLI (`/opt/homebrew/bin/gh`) configured with HTTPS credentials.

```bash
git add <file>
git commit -m "Description"
git push
```

**Commit and push after every meaningful unit of work** — a new file, a completed feature, a bug fix, a significant edit. Never leave completed work uncommitted. Commit messages should name the project and summarize what changed. Push immediately after committing so GitHub always reflects the latest state.

## Architecture

All projects follow the same pattern:
- **Single `.html` file** — HTML, CSS, and JS are all inline. No external files, no frameworks.
- **Canvas-based games** use `requestAnimationFrame` for the game loop with delta-time (`dt`) so speed is frame-rate independent.
- **State machines** drive game flow (e.g. `menu → playing → levelup → gameover`).
- **No assets** — all graphics are drawn with Canvas 2D API primitives (arcs, beziers, fills).

### duckshooter.html
- Game entities: `P` (player), `ducks[]`, `bullets[]`, `particles[]`, `clouds[]`
- Level config array `LEVELS[]` drives spawn rate, speed, and duck movement pattern per level
- Duck patterns: `straight`, `wave`, `swoop`, `zigzag`, `mixed`
- Input via `keys{}` object — keydown sets true, keyup sets false; `onKeyPress` handles one-shot actions (shoot, state transitions)

### tictactoe.html
- `board[]` array (9 cells), `current` player string, `gameOver` flag
- Win checking iterates `wins[]` (8 lines) after each move
- Scores persist across games via `scores` object; `resetGame()` resets board only
