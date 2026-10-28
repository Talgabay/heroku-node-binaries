# heroku-node-binaries

Official Node.js release tarballs, unmodified, mirrored for Heroku builds of `bit-labels-server`.

On 28/10/2026 Heroku's builders downloaded from nodejs.org at ~9 KB/s and builds failed with
"Unable to download Node.js". The Heroku Node.js buildpack reads the `NODE_BINARY_URL` config var
and downloads Node from that address instead; GitHub release assets download from Heroku at ~40 MB/s.

Each release holds one file, copied byte for byte from `https://nodejs.org/download/release/<version>/`.
Before upload its SHA-256 was checked against nodejs.org's `SHASUMS256.txt` and against the checksum in
Heroku's own buildpack inventory (`heroku/heroku-buildpack-nodejs` `inventory/node.toml`). The buildpack
does not verify a checksum when `NODE_BINARY_URL` is set, so the check is done here, at upload time.

To move to a new Node version: download the tarball from nodejs.org, check its SHA-256 against both
sources above, publish it as a new release `v<version>`, then point `NODE_BINARY_URL` at it.
