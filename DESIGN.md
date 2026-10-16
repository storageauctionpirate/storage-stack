# Storage Stack — DESIGN (rough draft v0.1)
By Storage Auction Pirate. Single `index.html`, vanilla JS. Core = `StorageStack` module (`CONFIG` at top, `StorageStack.create(canvas, {onUpdate,onGameOver})` returns `{start, move, rotate, soft, drop, slideRow, slideCol, state, pause}`) so it can be embedded as a mini-game.

## Rules
- Junk enters via the roll-up door; move/rotate it while it falls. Speeds up per line and per level.
- Pieces: box 1x1, TV 2x1, couch 3x1, fridge 1x2, dresser 2x2. Each piece has one of 5 door colors (L1 uses 3 colors, +1 per level).
- Match by COLOR only. Full row of one color = `rowClearCash*W/5`, x2 if all same item type. Horizontal runs of 4+ same color also clear (small cash). Chains multiply.
- Row slide (◀ ▶) wraps the row; column twist (▼) cycles the column's stack. Both re-check matches. Landed items settle per cell (gravity).
- Each level picks a random unit: 5x10→5x9, 10x10→8x8, 10x20→8x11, 10x30→9x12. Clear 6 lines → next random unit.
- Lose when junk can't enter the door.

## CONFIG
colors, startColors, items (emoji, w, h, spawn weight), units, linesPerLevel, startFallMs/minFallMs/speedupPerLine/speedupPerLevel, rowClearCash, typeBonusMult, runMin, runCashPerCell, levelBonus, slideCost.

## Open questions
- Keep the 4-run partial clears, or full-row only (much harder)?
- Should slides cost cash / be limited per piece?
- Should big items stay whole after landing (currently split into 1x1 cells)?
- Column matches too? Real sprite art instead of emoji?
- Do grid layouts stay when moving between units, or fresh unit each level (current)?

## TWIST MODE (hard mode, v0.2)
Title offers CLASSIC (unchanged) and TWIST MODE. In Twist, each cell of a piece has its own door color. Every rotate: shape turns, colors shift one step around the piece's cells (`twistRingShift`), and each advances one step in `twistCycle` red›orange›yellow›green›blue (only colors unlocked this level). Square pieces still twist colors. "↻ TWIST ➜" panel (top right) previews post-rotate colors; driveway shows the cycle. Spin + flash animation (`twistSpinMs`). `twistAutoCycleMs` (default 0 = off) auto-advances colors while falling. No sounds exist, so none added.
