# dynamic-config-rs.github.io

The organisation's site: four books, built from four repositories and
published together at <https://dynamic-config-rs.github.io/>.

| Path | Book | Source |
|---|---|---|
| `/` | the engine, the macro, the loader, the CLI | [dynamic-config](https://github.com/dynamic-config-rs/dynamic-config) |
| `/remote/` | the eight stores and the config server | [dynamic-config-remote](https://github.com/dynamic-config-rs/dynamic-config-remote) |
| `/python/` | the Python wheels | [dynamic-config-python](https://github.com/dynamic-config-rs/dynamic-config-python) |
| `/node/` | the npm packages | [dynamic-config-node](https://github.com/dynamic-config-rs/dynamic-config-node) |

**No prose lives here.** Every page is in the repository of the code it
documents, which is what keeps a chapter and the change it describes in
one pull request. This repository is the workflow that assembles them.

## Publishing

`.github/workflows/site.yml` checks out the four repositories at `main`,
builds each book with a pinned, digest-verified mdBook, asserts that all
four index pages exist — a missing directory is a 404 on a green build,
which is exactly the failure this project has already shipped once — and
deploys the result to Pages.

It runs every six hours, on a push here, and on demand:

```sh
gh workflow run site.yml --repo dynamic-config-rs/dynamic-config-rs.github.io
```

A book change lands in another repository, so nothing here notices it
immediately. Publishing within a minute instead would mean a token with
write access to this repository stored in all four — four more secrets to
rotate, for prose. The schedule is the trade this project made; the
dispatch above is the answer when it matters.

## The old site

Releases up to 0.6.1 shipped from a single repository, and their
published metadata points at `ctolon.github.io/dynamic-config`. That site
stays up, archived, so nothing already on crates.io, PyPI or npm links
into a 404.
