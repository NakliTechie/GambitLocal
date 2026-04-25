# GambitLocal

**Play chess in your browser — offline, private, no account needed.**

🎮 **[Play now →](https://naklitechie.github.io/GambitLocal)**

GambitLocal is part of the [NakliTechie](https://github.com/NakliTechie) series of browser-native tools: single-file apps that run entirely on your device. No server. No API keys. No data leaving your machine.

---

## Features

- **vs Engine** — Play against Stockfish, a world-class chess engine, running entirely in your browser via WebAssembly. Adjustable difficulty from Beginner to Max.
- **Correspondence mode** — Play a slow game with a friend over WhatsApp, email, or any messenger. The full game state is encoded in a URL — share a link after each move, no app or account needed on either side.
- **Mobile friendly** — Tap to select a piece, tap to place it. Works on any touchscreen browser; no app required.
- **Legal move hints** — Hover (desktop) or select (mobile) a piece to see all valid squares highlighted. Toggle hints on/off.
- **Opening detection** — Recognises ~40 openings automatically as you play.
- **Move history** — Full algebraic notation, scrollable.
- **Captured pieces** — Displayed per player.
- **Time controls** — Bullet (1 min) through Classical (30 min), or unlimited.
- **PGN export** — Copy the full game in standard notation.
- **Flip board**, **Undo move**, result detection (checkmate, stalemate, draws).
- **Hints toggle** — Turn move hints on or off (default on).
- Works offline after the first load — the engine is cached by your browser.

---

## How correspondence mode works

The entire game lives in the URL hash:

```
https://naklitech.github.io/GambitLocal/#pgn=…
```

1. Switch to the **Correspondence** tab and click **New Game**.
2. Make your move on the board.
3. Click **🔗 Share Position** — the link is copied to your clipboard.
4. Send it to your opponent (WhatsApp, iMessage, email — anything).
5. They open the link in any browser. The board loads at your move.
6. They reply, click **🔗 Share Position**, send the new link back.
7. Repeat until checkmate.

No login. No account. No data stored anywhere. Just a URL.

---

## Tech stack

| Concern | Solution |
|---|---|
| Chess rules & move validation | [chess.js](https://github.com/jhlywa/chess.js) v0.10.3 |
| Board rendering & drag-and-drop | [chessboard.js](https://chessboardjs.com) v1.0.0 |
| Chess engine | [Stockfish.js](https://github.com/nmrugg/stockfish.js) v10 — Stockfish compiled to JavaScript |
| Engine isolation | Web Worker (blob URL — avoids cross-origin restrictions) |
| Game state sharing | PGN encoded as Base64 in the URL hash (`#pgn=…`) |
| Hosting | GitHub Pages — single static file |
| Dependencies | jQuery (required by chessboard.js), everything else vanilla JS |

### Why a blob Worker for Stockfish?

Stockfish runs in a [Web Worker](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API) so the engine can think without freezing the UI. Loading a cross-origin script directly as a Worker is blocked by browsers. Instead, GambitLocal fetches the Stockfish script from jsDelivr, wraps it in a `Blob`, and creates the Worker from a local `blob://` URL — no CORS restriction, no server required.

---

## Running locally

No build step. Open the file directly:

```bash
open index.html
# or
python3 -m http.server 8080
```

---

## Palette

Coloured with **`iran-02 · خشت KHESHT`** — Yazd mud-brick (UNESCO 2017), the homeland of shatranj where chaturanga became chess. Warm clay body, royal-blue command accent, brick-red brand mark.

Palette pulled from [**Rangrez**](https://github.com/NakliTechie/rangrez), the global colour-palette library that backs all NakliTechie projects.

---

## Deployment

Hosted on GitHub Pages from the `main` branch. Any push to `main` automatically updates the live site.

---

## Part of the NakliTechie series

| Tool | What it does |
|------|--------------|
| [**BabelLocal**](https://github.com/NakliTechie/BabelLocal) | Offline translation — 200 languages, NLLB model |
| [**StripLocal**](https://github.com/NakliTechie/StripLocal) | EXIF metadata stripper — nothing leaves the browser |
| **GambitLocal** | Chess vs Stockfish — correspondence mode via URL |
| [**VoiceVault**](https://github.com/NakliTechie/VoiceVault) | Audio transcription — Whisper, offline-first |
| [**KingMe**](https://github.com/NakliTechie/KingMe) | English draughts — custom minimax AI, zero deps |
| [**SnipLocal**](https://github.com/NakliTechie/SnipLocal) | Background remover — RMBG-1.4, passport mode |
| [**Clacker**](https://github.com/NakliTechie/Clacker) | Split-flap display — browser-native, offline |
| [**Strait Command**](https://github.com/NakliTechie/strait-command) | Mine-clearing game in strategic waterways |
| [**Chokepoint**](https://github.com/NakliTechie/chokepoint) | Maritime tower defense — hold the strait |
| [**PredictionMarket**](https://github.com/NakliTechie/PredictionMarket) | Prediction market simulator — Parimutuel & LMSR |
| **PDFLOcal** | PDF editor — merge, split, rotate, annotate |
| **RangeLocal** | Missile range simulator — interactive globe & map |
| [**3D Tic-Tac-Toe**](https://github.com/NakliTechie/3d-tic-tac-toe) | 3D tic-tac-toe — 3×3×3 to 5×5×5, minimax AI |

---

**Built by [Chirag Patnaik](https://github.com/NakliTechie)**
