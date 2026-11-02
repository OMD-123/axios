# Pre-Release Changelog

## Unreleased

## Features

## Bug Fixes

- **Fetch response-stream capability probe:** Cancelled the `ReadableStream` created by the `supportsResponseStream` capability probe in the fetch adapter. The probe body was left uncancelled, so its pull promise stayed pending for the lifetime of the module realm and leaked one async resource per realm. This is the sibling of the request-stream probe leak fixed in v1.14.0, which did not cover the response probe. The cleanup is best-effort and shared by both probes: a probe body whose `cancel()` throws or rejects no longer downgrades the detected stream capability, and a rejected cancellation no longer surfaces as an unhandled rejection. No public API, type, or configuration changes. (closes [#11240](https://github.com/axios/axios/issues/11240))

## Documentation

- **README sponsor name:** Corrected sponsor name typo `BSAP SE` → `SAP SE` in the README sponsor listing. This updates sponsor recognition only, with no runtime, public API, or type compatibility changes. ([#11373](https://github.com/axios/axios/pull/11373))
- **Error identification:** Corrected the error `name` description in the README and English, French, Spanish, and Chinese error-handling guides. Cancellation errors use `CanceledError`, and wrapped errors may retain their original name, so the guides now recommend `axios.isAxiosError(error)` for identifying Axios errors and `axios.isCancel(error)` for detecting cancellations instead of comparing `name`. Documentation only; no runtime, public API, or type changes. ([#11374](https://github.com/axios/axios/pull/11374))
- **v1.21.0 release notes and docs:** Added the published v1.21.0 release notes to `CHANGELOG.md`. Applied the 13 pending `PRE_RELEASE_DOCS.md` entries from v1.20.0 and v1.21.0 to the English, Spanish, French, and Chinese docs site, including upgrade-guide sections for both releases. Cleared the released entries from `PRE_RELEASE_CHANGELOG.md`, and reduced `PRE_RELEASE_DOCS.md` to the README updates that remain pending for those entries. No runtime, public API, or type compatibility changes.

## Maintenance

<!-- Record test-only changes, internal refactors, tooling, dependency updates, and CI changes without a user-visible behavior change here. -->

- **CI runners:** Switched GitHub Actions jobs from GitHub-hosted `ubuntu-latest` runners to the `namespace-profile-axios` Namespace runner profile. The npm publish job stays on `ubuntu-latest` because npm provenance and trusted publishing require GitHub-hosted runners. CI only; no runtime, public API, or type compatibility changes.
