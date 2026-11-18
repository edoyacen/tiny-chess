# Tiny chess engine — 4,096 bytes of Python

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/edoyacen/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard)
[![reward](https://make.fun/badge/tiny-chess-01/edoyacen/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01)

An entry for [make.fun](https://make.fun)'s `tiny-chess-01`
([bounty page](https://make.fun/bounty/tiny-chess-01)): a chess engine in at most
4,096 bytes of Python.

## What is in it

`main.py` is a loader and an lzma payload. It decompresses its own source and runs
it, which is how a search this size fits the byte cap.

The engine inside:

- negamax with alpha-beta, and a root that keeps a window across its moves
- iterative deepening over a fixed node budget, never a clock, so a replay of a
  trial plays exactly the same moves
- a transposition table, killers and a history table in the move ordering
- quiescence over captures, so the search does not stop in the middle of an
  exchange
- an evaluation of material, piece squares, the bishop pair, and a king that hides
  in the middlegame and walks out once the queens are gone

It plays the house gauntlet over HTTP at `MAKEFUN_ENV_URL` and reads no other file
of this repository.

## Files

- `main.py` — the whole engine, 3,642 bytes
- `LICENSE` — MIT
- `README.md` — this page

Licensed MIT.
