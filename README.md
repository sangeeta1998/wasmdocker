```
curl -fsSL https://developer.fermyon.com/downloads/install.sh | bash -s -- -v v2.4.2
```

```
spin new
```
Choose http-rust, name the app "anyname", and set the following options:

HTTP base: /
HTTP path: /

Can make changes to lib.rs 

Save  changes and run spin build to build the app as a Wasm app.

```
spin build
spin up
```

# With docker

Dockerfile
```
FROM scratch
COPY /target/wasm32-wasi/release/dockercon.wasm .
COPY spin.toml .
```

The wasm module is available in the src directory after wasm build.
Therefore, edit spin.toml and replace 
```
source = "dockercon.wasm"
```

# Build 
```
docker buildx build \
  --platform wasi/wasm \
  --provenance=false \
  -t wasmdocker .
```

#Run

```
docker run -d \
  --runtime=io.containerd.spin.v2 \
  --platform=wasi/wasm \
  -p 3000:80 \
  wasmdocker /
```

# For more runtimes

https://docs.docker.com/desktop/wasm/
