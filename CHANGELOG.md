# Changelog

All notable changes to this project are documented in this file. The format
is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [1.0.0-draft.1] — 2026-09-24

- Initial standalone publication. Text carried from MCP SEP-3004 at commit `9405ba2f`; normative sections §2.1–§2.9 unchanged in substance.
- Vector set extended from 23 to 26: `V-REC2-c1-control`, `V-REC2-unpaired-surrogate`, `V-REC2-astral-literal` (C-REC-2 coverage the text already claimed).
- `canonical_form_version` value pinned: `audit-record-contract/1` (spec §2.3, §2.7).
- Informative Privacy Considerations section added after Security Implications: the contract has no accepted-break or redaction mechanism; personal data stays outside the protected bytes (pseudonymous identifiers, ciphertext values, off-record commitments); payload commitments follow the same pattern. No rule or digest changed.
- String-rule negative vectors (`V-REC2-control-char` and the two new controls) now re-seal the mutated record with the verifier's own canonicalizer before verifying, so a verifier that lacks the rule accepts the record and fails the vector. Previously the fixture's stale `event_hash` caused a hash-mismatch rejection on any verifier, so the vector could not discriminate. No digest changed.
