# Containerd and runwasi

Clone runwasi repo
`https://github.com/containerd/runwasi.git


libseccomp-dev - high level interface to Linux seccomp filter (development files)
libseccomp2 - high level interface to Linux seccomp filter
cargo clean

``` cargo build --target=x86_64-unknown-linux-gnu --target-dir=./target/ -p containerd-shim-wasmtime ```

Server:
Containerd is installed ctr github.com/k3s-io/containerd v1.7.15-k3s1

Installed as part of k3s and the configuration file is here: /var/lib/rancher/k3s/agent/etc/containerd/config.toml.

Create a file config.toml.tmpl in the same directory and add the configuration needed for runwasi there once you have installed the wasmtime shim
 

