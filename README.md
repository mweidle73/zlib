# Abuild zlib archive

This repository preserves the historical zlib source revision formerly used
by [Abuild](https://github.com/mweidle73/abuild). The authoritative project is
maintained by Mark Adler in the
[official zlib repository](https://github.com/madler/zlib); its original
documentation remains available in the [upstream README](README).

The long-lived branches have deliberately separate roles:

- `master` mirrors the authoritative upstream `develop` branch;
- `abuild` is the exact upstream `v1.2.11` revision formerly pinned by
  Abuild; and
- `abuild-gh` adds only this maintenance README and files below `.github/`
  to `abuild`.

The `abuild` branch points directly at upstream commit `cacf7f1d`, the
dereferenced target of the signed `v1.2.11` tag. Abuild carried no source
patches on top of that revision. It stopped building vendored zlib sources in
2026 and now uses the distribution development library. This repository is
retained for provenance and reproducibility, not as a recommended zlib
version for new deployments.

## Continuous integration

Run the same Trixie check locally with Docker:

```sh
.github/ci/run .github/ci/check
```

The check copies the preserved source into a private writable directory,
configures and builds it, runs the upstream test target, and verifies a
compression round trip. The build executes as the invoking non-root user in a
read-only container without network access or Linux capabilities.

The weekly upstream monitor checks whether `master` still matches upstream
`develop` and whether all versioned release-tag refs are mirrored exactly. It
reports drift but never updates branches or tags automatically.
