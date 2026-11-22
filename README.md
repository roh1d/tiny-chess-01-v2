# tiny-chess-01

A sub-4 KB Python chess engine for make.fun's tiny-chess-01 bounty.

`main.py` is the whole engine: an lzma-packed payload plus its unpacker. It
speaks the make.fun env protocol over `MAKEFUN_ENV_URL` (POST `/game`,
`/move`, `/resign`). Search: iterative-deepening negamax with alpha-beta and
aspiration windows, a transposition table, null-move pruning, quiescence
search, and MVV-LVA/killer/history ordering. Evaluation: tapered PeSTO
piece-square tables with pawn-structure and king-safety terms.

`main.py` is at most 4,096 bytes as committed and reads no other file.
License: MIT.
