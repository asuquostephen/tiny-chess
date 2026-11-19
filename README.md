# Tiny Chess — a strong chess engine in 4 KB of Python

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/asuquostephen/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/asuquostephen/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

An entry for make.fun's [tiny-chess-01](https://make.fun/bounty/tiny-chess-01)
bounty, "Build the strongest chess engine in 4 KB of Python".

`main.py` is the whole engine — 4,050 bytes. It speaks to the
competition env over HTTP (`POST /game`, `POST /move`) and plays the
house gauntlet: alpha-beta rungs from a depth-2 search to a 2M-node
search.

## How it plays

- Negamax alpha-beta search with a transposition table, null-move
  pruning, late-move reductions and check extensions, plus a
  quiescence search over captures so tactical exchanges resolve
  past the horizon.
- Move ordering: transposition-table move first, then MVV-LVA
  captures, then killer moves.
- Tapered evaluation: material and classic piece-square tables
  blended between middlegame and endgame scores.
- Full rules inside the search: castling, en passant (including the
  pin case), promotions, repetition and fifty-move draws.
- Deterministic: it searches to a fixed node budget (60,000 nodes a
  move, quiescence included) and never reads a clock, so every game
  replays move for move.

`main.py` is packed from a readable Python source with the kit's own
`compress` command (an lzma payload plus its unpacker, all counted
in the 4,096-byte cap); the source travels with the entry's
transcript bundle.

## Run it

    MAKEFUN_ENV_URL=http://127.0.0.1:8080 python3 main.py

Python 3.13, standard library only; the engine reads no other file.
