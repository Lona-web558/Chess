# Chess

# chess://console

A full single-file HTML chess game — local two-player, complete rules engine, no dependencies, no build step.

## Run it

Just open `chess.html` in any browser. Nothing to install.

## Features

- **Full legal move engine**: every standard chess rule is implemented from scratch in vanilla JS
  - Check, checkmate, and stalemate detection
  - Castling (kingside and queenside, with all legality checks — king not in check, doesn't pass through or land on an attacked square)
  - En passant
  - Pawn promotion (choose queen, rook, bishop, or knight via a popup)
  - Draw by insufficient material (K vs K, K+N vs K, K+B vs K, same-color bishops)
- **Game-over overlay**: a clear banner announces checkmate/stalemate/draw the moment the game ends, with a one-click "new game" button
- **Move log**: algebraic notation with proper disambiguation (e.g. `Nbd2` when two knights could reach the same square), `+` for check, `#` for checkmate
- **Captured piece tray**: shows material taken by each side and the material difference
- **Undo** (rewinds one full ply and replays the game state)
- **Flip board**

## Design

Dark terminal aesthetic — gold vs. cyan pieces, JetBrains Mono for the console/log, Space Grotesk for headings — matching the visual language across Lona's other apps.

## How it's built

- Single HTML file: all CSS and JS inline, no external JS libraries
- Board state: 8x8 array (`rank*8 + file` indexing), pieces as `{type, color}` objects
- Legal moves are generated as pseudo-legal moves per piece, then filtered by simulating each move and checking the mover's own king isn't left in check
- Game state (turn, castling rights, en passant target) is cloned on every move so undo/replay just re-runs the move list from a fresh starting position

## Known limitations

- No AI opponent — this is pass-and-play, two humans at one screen
- No draw by threefold repetition or 50-move rule
- No online multiplayer, no persistence between page reloads
