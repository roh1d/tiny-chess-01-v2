# tiny-chess-01

A 4 KB Python chess engine for make.fun.

## Entry

`main.py` is the whole engine.
It is an lzma-packed payload.
It is 4,076 bytes as committed.
It reads no other repo file.
It uses Python 3.13 stdlib only.
It talks to `MAKEFUN_ENV_URL`.
It posts `/game`, `/move`, `/resign`.
It exits when the trial is done.

## Loop

Start with `POST /game {}`.
Keep the current game id.
Clear repetition state on a new game.
Parse the FEN from the answer.
Choose a move from the position.
Fall back to the first legal move.
Post the move to `/move`.
Resign when no move exists.
Retry `/game` after an error.
Never read the wall clock.

## Search

Iterative deepening one to ten.
Negamax with alpha-beta.
PVS re-search at the root.
Transposition table per move.
Depth, score, bound, best move.
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
Stop at 50,000 nodes.
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
