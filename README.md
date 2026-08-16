# noclip-releases

Release artifacts for NOCLIP. **Binaries only — the source lives in the private
`noclip` repository.**

This repository exists so the update token can be handed out safely.

The daemon fetches its own updates from GitHub, which means a token has to sit
in `config.toml` on whatever PC the daemon runs on. A token scoped to the
source repository would let anyone who can read that file clone the entire
codebase. Scoped to *this* repository, the worst it can do is download the same
installers the holder was given anyway.

So: the token in a daemon's config should have **read-only Contents on this
repository and nothing else**.

## What is in a release

| Asset | For |
|---|---|
| `app-release.apk` | The phone app. The daemon downloads this and hands it to the phone via Panel → About. |
| `noclip-windows-vX.Y.Z.zip` | The Windows daemon, its installer, and the browser extension. Installed by hand. |

Only the `.apk` is fetched automatically — the daemon selects it by suffix.
The Windows zip is always a manual install, because nothing in this product
updates the daemon for you.

## Publishing

Built from the `noclip` repository at the matching tag. Versions in
`pubspec.yaml` and `daemon/Cargo.toml` are kept in lockstep with the tag here.

Releases must be published, not draft, and not marked prerelease — the daemon
picks the first release matching that filter, so a draft or a prerelease is
invisible to it.
