# Sendrift releases

Public download channel for [Sendrift](https://github.com/stoynov/sendrift) (source is private).
Every release carries the macOS app (zip, dmg, pkg), the Linux packages (deb, rpm, tar.gz),
`SHA256SUMS`, and the update manifest `stable.json` with its minisign signature
`stable.json.minisig`. The app reads

    https://github.com/stoynov/sendrift-releases/releases/latest/download/stable.json

verifies the signature with the public key embedded in the app, and offers the newer build.
Nothing is downloaded without the user's consent; the check sends only a GET with the app's
version in the user agent.
