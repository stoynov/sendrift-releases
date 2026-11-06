# Sendrift releases

Download channel for **Sendrift**, a native desktop app for sending files and folders between
two devices: devices find each other on the local network, identities are verified by the
people involved, every batch needs the recipient's acceptance, data moves over an end-to-end
encrypted QUIC connection, transfers resume after interruptions, and received batches are
published as new folders only after every byte has been verified. No accounts, no cloud
storage, no telemetry.

## Downloads

Every release on the [Releases](https://github.com/stoynov/sendrift-releases/releases) page
carries the following files, each with a detached minisign signature (`.minisig`), plus
`SHA256SUMS` and the update manifest `stable.json`.

| Platform | File | Install |
|---|---|---|
| macOS 15 or later, Apple Silicon | `Sendrift-<version>-macos-arm64.dmg` (or `.zip`) | Open the disk image, drag Sendrift to Applications. Developer ID signed and notarized. Allow the Local Network prompt on first launch. |
| Debian, Ubuntu, Linux Mint, Pop!_OS (x86_64) | `sendrift_<version>_amd64.deb` | `sudo apt install ./sendrift_<version>_amd64.deb` |
| Fedora, RHEL and derivatives (x86_64) | `sendrift-<version>-1.x86_64.rpm` | `sudo dnf install ./sendrift-<version>-1.x86_64.rpm` |
| Other Linux distributions (x86_64, glibc 2.36+) | `sendrift-<version>-linux-x86_64.tar.gz` | Unpack, then `./install.sh` (default prefix `/usr/local`; `PREFIX=~/.local ./install.sh` for a user install). |
| Windows 10/11 (x64) | `Sendrift-<version>-windows-x86_64.zip` | Unpack and run `sendrift-desktop.exe`. Unsigned for now: SmartScreen warns on first run. Not yet exercised on Windows hardware. |

The macOS `.pkg` is provided for managed installs; it is not signed yet, so prefer the `.dmg`.

## Verifying a download

```sh
shasum -a 256 -c SHA256SUMS --ignore-missing
minisign -Vm <file> -P RWR+0TJcmtRKlbpFJ/bxE20CuxxIu0abWpSwO1MG4mGlxBuuQAoNlNbe
```

The public key above is the Sendrift release key; it is also embedded in the app.

## Automatic updates

Sendrift checks this channel once a day (Settings → Updates, default on, one switch) by
fetching `stable.json` from

    https://github.com/stoynov/sendrift-releases/releases/latest/download/stable.json

verifying its signature with the embedded key, and comparing the build number with its own.
A newer build is offered, never installed on its own. Downloads are checked against the
manifest (size, SHA-256, signature); on macOS the new app must also be signed by the same
developer and accepted by Gatekeeper before it replaces the installed one and reopens. Linux
tarball installs in a writable prefix update in place; deb/rpm installs are pointed at the new
package. The only data sent by the check is the app's version in the request's user agent.

## Support

Issues and questions: open a discussion with the maintainer. Logs live in the profile folder
(`~/Library/Application Support/com.sendrift.Sendrift/profiles/<name>/logs` on macOS,
`~/.local/share/sendrift/profiles/<name>/logs` on Linux) and never contain file names,
invitation links or secrets.
