# BermudaPay — Release Artifacts

This repo hosts the Sparkle **appcast** and **release archives** for
[BermudaPay](https://github.com/jbatten0/BermudaPay). It's intentionally
public because:

1. The Sparkle updater in the app needs unauthenticated HTTPS access to the
   appcast and signed zip files.
2. The main BermudaPay repo is private — we keep it that way by isolating
   anything that needs public hosting into this separate repo.

## Contents

- [`appcast.xml`](appcast.xml) — Sparkle feed. The app polls
  `https://raw.githubusercontent.com/jbatten0/BermudaPay-releases/main/appcast.xml`
  when the user clicks **Check for Updates…**
- Release archives live under **[Releases](../../releases)**. Each release
  ships a single `BermudaPay-<version>.zip`, signed with a Developer ID
  certificate, notarized by Apple, and stapled.

Every release archive is also signed with an EdDSA key; Sparkle verifies
that signature against the public key baked into the app's `Info.plist`
before installing. Nothing published here can silently tamper with an
installed app — signatures that don't match the in-app public key are
rejected.

## How releases are cut

See [`RELEASING.md`](https://github.com/jbatten0/BermudaPay/blob/main/RELEASING.md)
in the main repo. The `Scripts/release.sh` script there handles building,
signing, notarizing, uploading to this repo, and updating `appcast.xml`.

## Security

If you find something wrong with a release — a signature mismatch, an
expired certificate, a broken hash — please open an issue on the main repo.
