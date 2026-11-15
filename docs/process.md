# Engineering and Release Process

All GitHub issues, pull requests, code reviews, discussions, commit messages,
and documentation across the `totaldrop-app` organization are conducted **100% in
English** ([0019](decisions/0019-english-by-default.md)) so our growing
international team collaborates on a single source of truth.

## 1. Workflow & Mandatory Co-Maintainer Review

TotalDrop is maintained jointly by Core Maintainers **[@ozdil](https://github.com/ozdil)**
and **[@sadikkuzu](https://github.com/sadikkuzu)**
([`GOVERNANCE.md`](https://github.com/totaldrop-app/.github/blob/main/GOVERNANCE.md)).

1. **Issue First:** Every non-trivial change starts with an English GitHub issue
   in the target repository (`totaldrop-core`, `totaldrop-linux`, etc.) linked
   to a milestone (`Now`, `Next`, `Later`, `1.0`) and labeled by area and
   architecture (`arch:x86_64`, `arch:arm64`, `arch:riscv64`, `area:l10n`, etc.).
2. **Short-Lived Branch:** Branch names state intent (`feat/ring-mailbox`,
   `fix/linux-quit-portmap`, `pkg/linux-deb-riscv64`, `gov/co-maintainer-review`).
   Direct pushes and force-pushes to `main` are disabled (`bypass_actors: []`).
3. **Pull Request & CI Gate:** Every PR links its issue (`Closes #...`) and
   passes the required `CI` gate job (formatting, `clippy -- -D warnings`, unit
   & integration tests, cross-target checks, `cargo-deny`, `REUSE 3.3`, and
   `gitleaks` secret scan). Red checks are never bypassed.
4. **Mandatory Co-Maintainer Approval (`.github/CODEOWNERS`):** Every file in
   every `totaldrop-app` repository is owned by `* @sadikkuzu @ozdil`. Every PR
   touching code, cryptography, protocol, CI workflows, packaging recipes,
   localization, governance, or security documents must be reviewed by a party
   that did not author the diff **and explicitly approved (`APPROVED`) by the
   other Core Maintainer** (`@sadikkuzu` approves PRs opened under `@ozdil` —
   including AI coding sessions — and `@ozdil` approves PRs opened under
   `@sadikkuzu`). Self-merging without co-maintainer approval is prohibited.
5. **Linear History:** Approved pull requests merge exclusively via **rebase**
   onto `main`.

## 2. Definition of Done

A change is complete only when all of the following hold:
- Behavioral tests cover both happy paths and specific error variants (no
  fixed-sleep flaky assertions; use bounded condition polling).
- State machines use explicit typed `enum` states and generation counters across
  `await` boundaries — never implicit boolean pairs.
- Every new parser of untrusted bytes/JSON/IPC frames has a `cargo-fuzz` target
  in `totaldrop-formal-fuzz`.
- Untrusted peer text (filenames, device names, error details) is sanitized
  against terminal/UI control and invisible Bidi characters in a single pass.
- Protocol changes update [protocol-v0.1-notes.md](protocol-v0.1-notes.md);
  architectural changes add or update a record in [decisions/](decisions/README.md).
- User-facing string changes update `totaldrop-core/l10n/` (`en` template first,
  respecting `l10n/status.json` critical security string gates; see
  [translation.md](translation.md)).
- Any change to what servers observe updates the 35-language privacy policy in
  `totaldrop-site` **before** release.

## 3. Sub-Platform × Architecture Releases

Each sub-platform × CPU unit (`subplatforms/<format>/<arch>/`) builds in an
isolated container/VM with `SOURCE_DATE_EPOCH`, verifies package contents and
smoke startup, generates `SHA256SUMS`, and attaches a keyless Sigstore build
provenance bundle (`*.sigstore.json`) verifiable via `gh attestation verify`.
Release tags (`<platform>-<format>-<arch>-v*`, `server-v*`, `core-v*`) are
protected by the `release tags` repository ruleset.
