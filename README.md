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

Bundled plugins: `caddy-dns/{porkbun,cloudflare,route53,digitalocean,godaddy}`,
`caddyserver/jsonc-adapter`. See each release's notes for the exact Caddy
version, build provenance, and rebuild instructions.

Currently published: `linux/amd64`. Other platforms fall back to vanilla
Caddy until built here.
