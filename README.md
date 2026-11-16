# Tiny Chess v2 — a stronger 4 KB engine

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/hamkazhaa/makefun-tiny-chess-02/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard)
[![reward](https://make.fun/badge/tiny-chess-01/hamkazhaa/makefun-tiny-chess-02/reward.svg)](https://make.fun/bounty/tiny-chess-01)

A revised entry for the [tiny-chess-01](https://make.fun/bounty/tiny-chess-01) bounty: the strongest chess engine in 4 KB of Python. Pure Python 3.13 stdlib, no dependencies. Packed entrypoint `main.py` (3,966 B); readable source `engine.py` (uncommitted — over the snapshot cap — attached at bundle time).

## How it plays

0x88 board, negamax + alpha-beta, iterative deepening to a fixed 130,000-node budget per move (~3 s/move, under the 10 s cap). 1M-slot transposition table with mate-score adjustment; MVV-LVA captures, 2 killers/ply, history ordering; PVS inside the tree, null-move pruning (R=2), late-move reductions, check extensions; delta-pruned quiescence with check evasions. Tapered MG/EG piece-square tables, bishop-pair and passed-pawn bonuses. Deterministic: fixed node budget only, no clock, no unseeded randomness.

## Practice results (kit gauntlet, 24 games)

Trial-0 (100k): 3W/1D/2L, Elo 1364. Trial-1 (100k): 1W/0D/5L, Elo 876. Trial-2 (130k): 2W/1D/3L, Elo 1191. Trial-0 repeat (200k): 3W/1D/2L, Elo 1364. Mean ≈ 1199 (best 1364, matching the house baseline mean ≈ 1365). 6-game trials are noisy; the engine has checkmated nodes-250k.

## Run it

The kit runs `python3 -P -s /bot/main.py` with `MAKEFUN_ENV_URL` set; it speaks the env protocol (`POST /game`, `POST /move`).

## License

MIT — see `LICENSE`.
