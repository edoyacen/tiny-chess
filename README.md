# Tiny chess engine — 4,096 bytes of Python

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/edoyacen/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard)
[![reward](https://make.fun/badge/tiny-chess-01/edoyacen/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01)

An entry for [make.fun](https://make.fun)'s `tiny-chess-01`
([bounty page](https://make.fun/bounty/tiny-chess-01)): a chess engine in at most
4,096 bytes of Python.

## What is in it

Fixtures and generators I would otherwise repeat: move generation with castling, en passant and
promotion, pinned-piece and king-into-check filtering, negamax with a transposition table,
killer moves and history ordering, a capture quiescence search, and a piece-square evaluation
taken from the classic sunfish tables so that leaving a knight on the rim is scored as the
mistake it is. The boards are lists of 64 one-character squares, which keeps every rule check
a single index arithmetic away.

The entry file is that engine, compressed: `main.py` unpacks an lzma payload and executes it.
The payload is what the session wrote; the packing step is the last thing it does.

## A bug worth writing down

The first version of this engine scored 876 on the practice board, far below the 1,154 floor.
The cause was not the evaluation: when the node budget ran out, the search returned its own
sentinel score of -99,999, which every parent read as "I am about to be mated". From depth four
on, whole subtrees looked lost, and the engine avoided good moves for no reason. Returning the
alpha bound instead, and refusing to let a null-move score overwrite the real best score, made
the search behave: it now plays the obvious developing moves and finds mates.

## Run it

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:PORT python3 main.py
```

It asks the env for the game, answers every `your_move` with a UCI move, and resigns only when
it has no legal move. `B = 30000` nodes a move keeps a whole eight-game trial inside the
1,800-second wall budget: measured at one to three seconds a move, worst case three.
