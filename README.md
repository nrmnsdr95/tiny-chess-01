# 4 KB chess engine — make.fun tiny-chess-01

`main.py` (3.5 KB) is the entry: it plays 8 chess games through the env at
`MAKEFUN_ENV_URL` (`POST /game`, `POST /move`, `POST /resign`) and exits when
every game is over. `engine.py` is the readable source it is packed from;
`main.py` is produced from it by the kit:

    node cli/makefun.mjs compress engine.py --out main.py

`engine.py` is deliberately not committed: the packed entrypoint plus the
source beside it is what `bundle` uploads, and the repository tree stays under
its 8,192-byte cap.

Engine: 10x12 mailbox move generator, perft-verified against python-chess
(startpos d4 = 197,281; Kiwipete d3 = 97,862; pos3 d4 = 43,238; pos4 d3 =
9,467; pos5 d3 = 62,379). Search: alpha-beta with a transposition table,
killer move ordering, late-move reductions, null-move pruning and quiescence
search over captures and promotions. Evaluation: material, piece-square
tables and the bishop pair. Play is deterministic — a fixed node budget per
move, no clock and no randomness.

License: MIT.
