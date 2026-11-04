# caddy-dns-builds

Plugin-bundled Caddy binaries for `asd-cli`'s native-binary install path
(`modules/core/scripts/binary-installer.ts` in
[asd-engineering/.asd](https://github.com/asd-engineering/.asd)).

Vanilla Caddy releases never include third-party DNS provider plugins, so
`network.tls.acme.dns_provider` (DNS-01 ACME challenges) can't work with a
natively-installed Caddy — only with `.asd`'s Docker-mode build
(`modules/caddy/docker/caddy/Dockerfile`), which already bundles them.
Releases here are built from that same Dockerfile so both distribution
paths carry the identical plugin set, and are consumed directly by
`binary-installer.ts`'s `caddy` entry for platforms this repo has a build
for.

Bundled plugins: `mholt/caddy-l4` (layer4, for `inspect: true` on TCP services),
`caddy-dns/{porkbun,cloudflare,route53,digitalocean,godaddy}`, `greenpau/caddy-security`,
`caddyserver/jsonc-adapter`. See each release's notes for the exact Caddy
version, build provenance, and rebuild instructions.

Currently published (since `v2.11.7-l4dns1`): `linux/{amd64,arm64}`,
`darwin/{amd64,arm64}`, `windows/{amd64,arm64}`. Rebuild with `just caddy-build`
(then `just caddy-build-verify` and `just caddy-build-smoke`) in the `.asd` source;
the build is reproducible, so a rebuild must match the release's `SHA256SUMS.txt`.
