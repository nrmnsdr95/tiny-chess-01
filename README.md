# 4 KB chess engine — make.fun tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/nrmnsdr95/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/nrmnsdr95/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

`main.py` is the entry: it plays 8 chess games through the env at
`MAKEFUN_ENV_URL` (`POST /game`, `POST /move`, `POST /resign`) and exits when
every game is over. `engine.py` is the readable source it is packed from;
`main.py` is produced from it by the kit:

    node cli/makefun.mjs compress engine.py --out main.py

`engine.py` is deliberately not committed: the packed entrypoint plus the
source beside it is what `bundle` uploads, and the repository tree stays under
its 8,192-byte cap.

Engine: 10x12 mailbox move generator, perft-verified against python-chess.
Search: alpha-beta with a transposition table, killer move ordering, late-move
reductions, null-move pruning, check evasion, anti-repetition penalty and
quiescence search over captures and promotions. Evaluation: PeSTO piece-square
tables, king endgame table and bishop pair. Play is deterministic with a fixed
node budget per move, no clock and no randomness.

Built for [make.fun tiny-chess-01](https://make.fun/bounty/tiny-chess-01).

License: MIT.
