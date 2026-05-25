# kitepass CLI — public release channel

This repository is the **public distribution channel** for the
`kitepass` command-line tool. The CLI source code lives in the private
monorepo `zfdang/agent-passport-platform`; releases here mirror its
`cli/` directory.

- Pre-built binaries for Linux (x86_64, arm64) and macOS (x86_64, arm64)
  are published to **[Releases](../../releases)**.
- The static site at <https://cli.kitepass.xyz> is built from
  [`webpages/`](./webpages/) via the
  [Pages workflow](./.github/workflows/pages.yaml).

## Install

```sh
curl -fsSL https://cli.kitepass.xyz/install.sh | sh
```

…or fetch a specific tag:

```sh
KITEPASS_VERSION=cli-v0.1.0 sh -c "$(curl -fsSL https://cli.kitepass.xyz/install.sh)"
```

Manual install:

1. Pick the right archive from [Releases](../../releases) for your
   platform — `kitepass-cli-linux-x86_64-<tag>.tar.gz`,
   `kitepass-cli-macos-arm64-<tag>.tar.gz`, etc.
2. Verify the SHA-256 against the `*.sha256` sidecar.
3. Verify the Sigstore signature with `cosign verify-blob` (the
   `.pem` certificate and `.sig` signature are uploaded alongside
   each archive).
4. Extract and put the `kitepass` binary on your `PATH`.

## Reporting issues

Please file issues here. Internal source-level fixes happen in
`agent-passport-platform`; this repo's issue tracker is the canonical
user-facing surface.

## Verifying signatures (cosign)

```sh
cosign verify-blob \
  --certificate kitepass-cli-linux-x86_64-cli-v0.1.0.tar.gz.pem \
  --signature   kitepass-cli-linux-x86_64-cli-v0.1.0.tar.gz.sig \
  --certificate-identity-regexp 'github\.com/zfdang/agent-passport-platform' \
  --certificate-oidc-issuer    https://token.actions.githubusercontent.com \
  kitepass-cli-linux-x86_64-cli-v0.1.0.tar.gz
```
