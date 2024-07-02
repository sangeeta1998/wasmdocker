# Containerd and runwasi

Clone runwasi repo
`https://github.com/containerd/runwasi.git`
libseccomp-dev - high level interface to Linux seccomp filter (development files)
libseccomp2 - high level interface to Linux seccomp filter
cargo clean

``` cargo build --target=x86_64-unknown-linux-gnu --target-dir=./target/ -p containerd-shim-wasmtime ```

