# Changelog

All notable changes to this project are documented in this file. The format
is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [1.0.0] — 2026-09-30

- Version 1.0.0; spec status moves from Draft to Stable. No rule in §2.1–§2.9 changed; the canonical form stays `audit-record-contract/1`; no digest changed.
- Vector set extended from 26 to 30 (PR #2): `V-REC3-kat-core-altered`, `V-REC3-kat-extension-altered`, `V-REC5-emission-incomplete`, `V-REC5-emission-unlinked`. C-REC-3 and C-REC-5 had accepting cases only, so a verifier that always returned `ok` passed both; each new vector is the rejecting half of an existing one.
- §2.2: one dated sentence added to the `admission-control` registration. As of 2026-09-30, `enclawed/omcp` also publishes an ATSA text that it marks Final (extension version 1.0), with the same profile; MCP PR #2809 remains the registration's origin, and the canonical form is unaffected.
- Reproduction record: both known-answer digests were reproduced by an independently written canonicalizer (ATSA's) over the published records (2026-09-29), and earlier by an implementation written from the specification text alone in a second language (2026-07-29).
- `V-REC2-astral-literal`: the comment now shows the escape sequence it names (`\uD83D\uDD12`) instead of the literal character. Comment only.
- Appendix A.1: one sentence added recording the 1.0.0 changes against the carried text.

## [1.0.0-draft.1] — 2026-09-24

- Initial standalone publication. Text carried from MCP SEP-3004 at commit `9405ba2f`; normative sections §2.1–§2.9 unchanged in substance.
- Vector set extended from 23 to 26: `V-REC2-c1-control`, `V-REC2-unpaired-surrogate`, `V-REC2-astral-literal` (C-REC-2 coverage the text already claimed).
- `canonical_form_version` value pinned: `audit-record-contract/1` (spec §2.3, §2.7).
- Informative Privacy Considerations section added after Security Implications: the contract has no accepted-break or redaction mechanism; personal data stays outside the protected bytes (pseudonymous identifiers, ciphertext values, off-record commitments); payload commitments follow the same pattern. No rule or digest changed.
- String-rule negative vectors (`V-REC2-control-char` and the two new controls) now re-seal the mutated record with the verifier's own canonicalizer before verifying, so a verifier that lacks the rule accepts the record and fails the vector. Previously the fixture's stale `event_hash` caused a hash-mismatch rejection on any verifier, so the vector could not discriminate. No digest changed.
