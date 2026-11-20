# zkir-v3 for compactf

This branch is the tag `zkir-3.2.1` with faster key generation. It is the
`zkir-v3` that compactf runs. The keys it writes are the same as the ones stock
`zkir-3.2.1` writes.

The changes to midnight-proofs 0.8.2, midnight-circuits 7.3.0 and
midnight-zk-stdlib 2.4.0 are on branch `compactf` of
[faculerena/midnight-zk](https://github.com/faculerena/midnight-zk/tree/compactf).
`[patch.crates-io]` in `Cargo.toml` pins that branch by revision.

## Build

Built with rustc/cargo 1.88.0 on x86-64 Linux:

```sh
git clone -b compactf https://github.com/faculerena/midnight-zkir
cd midnight-zkir
cargo build --release --locked -p midnight-zkir --features binary
# -> target/release/zkir, installed as `zkir-v3`
```

## Checks

```sh
# the fast path against stock keygen: same k, same key bytes
# (needs the public parameters, e.g. ~/.cache/midnight/zk-params)
MIDNIGHT_PP=~/.cache/midnight/zk-params \
  cargo test --release --locked -p midnight-zkir --test proofs \
  test_write_only_keys_match_keygen
```

With `ZKIR_TIMING` set to any value, timings and resident memory are printed
to standard error. Nothing else changes.
