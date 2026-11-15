# Build and run from source

This repository is intended to be built from source. Do not deploy prebuilt
binaries from forks, release archives, or older bundles.

## Prerequisites

- Linux x86_64
- Go 1.22.x (tested with `go1.22.12`)
- `git`
- Free TCP ports `80` and `443` (and `53` if using the built-in DNS server)

## Build

```sh
cd evilginx2

CGO_ENABLED=0 GOTOOLCHAIN=local \
  go build -mod=vendor -trimpath -buildvcs=true \
  -ldflags "-s -w" -o build/evilginx2 .
```

`build/` is ignored by git. The resulting binary is static and stripped.

## Verify

```sh
file build/evilginx2
sha256sum build/evilginx2
go version -m build/evilginx2
./build/evilginx2 -v
```

The embedded `vcs.revision` should match the commit you built from and
`vcs.modified` should be `false` for a clean tree.

## Run (authorized lab only)

```sh
./build/evilginx2 -p ./phishlets -c "$HOME/.evilginx" -developer
```

Use self-signed certificates only in an isolated lab. For any real engagement,
use infrastructure and domains explicitly authorized in the rules of engagement.

## Scope

Only the Microsoft 365 phishlets are shipped in this repository. See
`docs/PHISHLETS.md` before adding or enabling anything else.
