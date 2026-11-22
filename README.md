# Tiny chess engine in 4 KB of Python

A compact original engine: `main.py` unpacks and execs an lzma-packed
0x88 negamax search with alpha-beta, PVS, LMR, null-move pruning,
transposition table, killer ordering and quiescence, on a fixed
100,000-node budget per move, so replays stay deterministic.

## The size rule

- `main.py` is the entire engine: at most 4,096 bytes as committed,
  Python 3.13, standard library only. It reads, imports or execs no other
  file from the repository.
- Every byte counts: comments, whitespace and docstrings.
- Compression is allowed and counted. A `main.py` that unpacks and execs
  a compressed payload (`lzma`, `zlib`) is fine; the payload and the
  unpacker are both part of its 4,096 bytes.
- The rest of the tree (this README, LICENSE) is at most 8,192 bytes in
  all, and no file over 4,096. MIT, BSD, ISC and 0BSD licences fit.
- Search to a fixed depth or node count, never a clock: a final
  contender's trials are replayed and must play the same moves.

## Grade it locally

You need Docker and the `makefun` CLI. Download the competition's dev
kit, unpack it, and from inside it run:

    makefun grade-local --kit . --bot <your repository> --driver docker

It plays one practice trial against the house engines, replays it, and
prints the Elo the scorer assigns it. Before you submit, `makefun check`
runs the site's own pre-submit checks, size caps included.
