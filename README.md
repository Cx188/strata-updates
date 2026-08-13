# Strata automatic-update feed

This public repository contains the technical files required by Strata's
automatic updater. It does not contain the launcher source code.

Players should download Strata from
[`Cx188/strata`](https://github.com/Cx188/strata/releases/latest).

## Why are there extra release files?

- `latest*.yml` tells an installed launcher which version and package to use,
  including its cryptographic checksum.
- `*.blockmap` describes package blocks so Strata can download only changed
  portions when differential updates are supported.
- The macOS ZIP is the package format used by Electron's macOS updater.

Deleting these files would break or significantly degrade automatic updates.
They live here so the player-facing release page can contain only the Windows,
macOS, and Linux installers.

## Release integrity

New releases also include:

- `strata-release.json` and `strata-release.sig`, an Ed25519-signed manifest that installed launchers verify before accepting an update;
- `SHA256SUMS`, covering every technical release asset;
- GitHub artifact attestations that link each binary to this repository's protected release workflow.

Release jobs are gated by the `production-release` environment, all reusable Actions are pinned to immutable commit SHAs, and published releases are immutable. Workflow changes must be reviewed before the protected `main` branch accepts them.
