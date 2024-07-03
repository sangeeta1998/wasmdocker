# Containerd and runwasi

Clone runwasi repo
`https://github.com/containerd/runwasi.git


libseccomp-dev - high level interface to Linux seccomp filter (development files)
libseccomp2 - high level interface to Linux seccomp filter
cargo clean

``` cargo build --target=x86_64-unknown-linux-gnu --target-dir=./target/ -p containerd-shim-wasmtime ```

Check : ``` find ./target -type f -name "containerd-shim-wasmtime" ```

If the binary is found, copy it to /usr/local/bin

``` sudo cp <path_to_binary> /usr/local/bin/ ```

sudo ln -s /usr/local/bin/containerd-shim-wasmtime  /usr/local/bin/containerd-shim-wasmtime-v1

Check if wasmtime is there: ``` ls -l ./target/x86_64-unknown-linux-gnu/debug/

if it is present,

containerd-shim-wasmtime-v1
copy this binary to /usr/local/bin/

```sudo cp ./target/x86_64-unknown-linux-gnu/debug/containerd-shim-wasmtime-v1 /usr/local/bin/```

check if correctly copied:
ls -l /usr/local/bin/containerd-shim-wasmtime-v1


Build and load the test image:

make test-image
make load

Run the test container with Wasmtime:

```sudo ctr run --rm --runtime=io.containerd.wasmtime.v1 ghcr.io/containerd/runwasi/wasi-demo-app:latest testwasm```

or

```sudo ctr image pull docker.io/sangeetakakati/rust_serverless:latest```

Run

```sudo ctr run --rm docker.io/sangeetakakati/rust-serverless:latest rust-serverless-container```




Server:
Containerd is installed ctr github.com/k3s-io/containerd v1.7.15-k3s1

Installed as part of k3s and the configuration file is here: /var/lib/rancher/k3s/agent/etc/containerd/config.toml.

Create a file config.toml.tmpl in the same directory and add the configuration needed for runwasi there once you have installed the wasmtime shim
 

