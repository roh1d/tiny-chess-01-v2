# tiny-chess-01

4 KB Python chess engine.

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/roh1d/tiny-chess-01-v2/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/roh1d/tiny-chess-01-v2/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

## Entry

`main.py` is the whole engine.
It is an lzma payload.
It is 3,996 bytes as committed.
It reads no other repo file.
Python 3.13 stdlib only.
Talks to `MAKEFUN_ENV_URL`.
It posts `/game`, `/move`, `/resign`.
Exits when the trial ends.

## Loop

Start with `POST /game {}`.
Keep the current game id.
Clear repetition on a new game.
Parse the FEN.
Choose a move.
Fall back to a legal move.
Post it to `/move`.
Resign if no move exists.
Retry `/game` on error.
Never read a clock.

## Search

Deepen one to ten.
Alpha-beta negamax.
PVS re-search at the root.
Table per move.
Depth, score, bound, move.
Null move at depth three.
No null move in check.
No null move in pawn endings.
Check extension adds one ply.
Quiescence at every leaf.
Quiescence searches captures.
Quiescence searches checks.
Mate scores adjust by ply.
Repetition scores zero.
Fifty-move scores zero.
Stop at 200,000 nodes.
Node limit makes replay exact.
Root reuses prior scores.
Bounds keep the best move.

## Ordering

Table best move first.
Promotions next.
Winning captures by MVV-LVA.
Killer moves by ply.
History for quiet moves.
Deterministic move tie-break.

## Evaluation

Tapered middlegame and endgame.
PeSTO piece values.
PeSTO square tables.
Tables stored as signed bytes.
Seven tables, rest derived.
Passed pawns score by rank.
King shield scores pawns.
Tempo bonus is ten.
Score is for the side to move.
Bishop pair omitted.
Rooks omitted.
Isolated pawns omitted.
Score is in centipawns.
White score is positive.
Black score is negated.

## Moves

Generate all legal root moves.
Filter pseudo-legal by king safety.
Castling checks transit squares.
En passant removes the pawn.
Promotions give queen, rook, bishop, knight.
UCI uses lower-case promotion.
Move code holds from, to, promo.

## Size

Readable source is not committed.
`source_tight.py` is packed source.
It ships beside the transcripts.
`makefun compress` writes `main.py`.
Entrypoint is under 4,096 bytes.
Tree is under 8,192 bytes.
License is MIT with SPDX.

## Verification

Perft on the start position.
Perft on Kiwipete.
Perft on two endgames.
Payload decompressed and run.
Opening move produced.
Beat house depth-2.
Beat house nodes-500k.
No clock in search.
No unseeded randomness.
Replay is deterministic.
Root moves are legal.
Table clears per move.
History clears per move.
Killers clear per move.
Search is deterministic.
FEN parsing handles all fields.
Castling rights are parsed.
En passant square is parsed.

## Files

`main.py` is the entrypoint.
`README.md` is this note.
`LICENSE` is MIT.

## Development

`dev_engine.py` is readable source.
`source_tight.py` is packed source.
`.work/` holds kit and tests.
These are not in the snapshot.
Packed source is sent with transcripts.

## License

MIT.
