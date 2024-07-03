# Containerd and runwasi

Clone runwasi repo
`https://github.com/containerd/runwasi.git


libseccomp-dev - high level interface to Linux seccomp filter (development files)
libseccomp2 - high level interface to Linux seccomp filter
cargo clean

Build Only the Wasmtime Shim:

``` cargo build --target=x86_64-unknown-linux-gnu --target-dir=./target/ -p containerd-shim-wasmtime ```

After building the shim, you need to install it. The provided Makefile targets might not distinguish between different shims, so we can install the Wasmtime shim manually.

```sudo cp ./target/x86_64-unknown-linux-gnu/debug/containerd-shim-wasmtime /usr/local/bin/```

```sudo ln -s /usr/local/bin/containerd-shim-wasmtime /usr/local/bin/containerd-shim-wasmtime-v1```


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


or

```sudo ctr image pull github.io/sangeetakakati/serwasm:latest```

Run

```sudo ctr run --rm docker.io/sangeetakakati/rust-serverless:latest rust-serverless-container```


ways to build and run:

```docker buildx build --platform wasi/wasm -t username/hello-world .```


```docker run   --runtime=io.containerd.wasmtime.v1   --platform=wasi/wasm   sangeetakakati/serwasm:latest```


Config file in k3s:

```[plugins."io.containerd.grpc.v1.cri".containerd.runtimes.wasmtime]```
  ```runtime_type = "io.containerd.wasmtime.v1"```

  k3s command:

```sudo systemctl restart k3s```
```sudo systemctl status k3s```

Server:
Containerd is installed ctr github.com/k3s-io/containerd v1.7.15-k3s1

Installed as part of k3s and the configuration file is here: /var/lib/rancher/k3s/agent/etc/containerd/config.toml.

Create a file config.toml.tmpl in the same directory and add the configuration needed for runwasi there once you have installed the wasmtime shim
 

