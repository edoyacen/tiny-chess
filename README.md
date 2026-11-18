# Tiny chess engine — 4 KB of Python

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/edoyacen/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard)
[![reward](https://make.fun/badge/tiny-chess-01/edoyacen/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01)

An entry for [make.fun](https://make.fun)'s `tiny-chess-01`
([bounty](https://make.fun/bounty/tiny-chess-01)): a chess engine in at most 4,096 bytes of Python.

`main.py` is a loader and an lzma payload: it decompresses its own source and runs it. The engine
inside is a negamax search with alpha-beta at the root, iterative deepening over a fixed node budget
(no clock, so a replay plays the same moves), a transposition table, killers and history in move
ordering, quiescence over captures, and an evaluation of material, piece squares, the bishop pair and
a king that hides in the middlegame and walks out in the endgame. It talks to the env over HTTP and
draws nothing from the network.

Built as an entry, not as a library: `main.py` reads no other file of this repository.

Licensed MIT.
