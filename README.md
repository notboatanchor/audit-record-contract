# Tamper-Evident Audit Record Contract

A canonical byte form, an append-only SHA-256 hash chain, and a verification
procedure for audit records, with a typed extension mechanism so that different
governance layers attach their own context under one integrity construction.
What must agree across implementations is the bytes, not the semantics.

- **Specification:** [`spec/audit-record-contract.md`](spec/audit-record-contract.md)
- **Conformance vectors + reference verifier:** [`vectors/`](vectors/) (26 vectors, zero dependencies)
- **Canonical form identifier:** `audit-record-contract/1`
- **Status:** 1.0.0-draft.1. Successor home of MCP SEP-3004 (PR #3004, closed 2026-09-22 under a process change; spec Appendix A). The normative text is carried unchanged in substance.

## Run the vectors against your implementation

```
node --experimental-strip-types vectors/run.ts     # Node 22.6+
# or
npx tsx vectors/run.ts
```

Expected: `26 vectors — 26 passed, 0 failed`.

The vectors are record/verifier vectors evaluated over an exported record set,
not wire-protocol scenarios. To check your own emitter, reproduce the two
known-answer digests from the spec's Conformance section with nothing but your
canonicalizer and `sha256sum`:

```
printf '%s' '<canonical preimage from the spec>' | sha256sum
# single-extension record -> d494769c1ae442ea88dd190068747abf63c0568a3b856f85791b1a50a99d48b4
# two-extension record    -> f733fed9cc757165f810b778e4baba1f51a45504988e937707aaab4361b2f064
```

If your bytes land on those digests, your canonical form agrees with every other
conforming implementation. If they do not, the C-REC-2 vectors will tell you
which rule diverged (key sort, value types, NFC, U+0020 trim, control
characters, unpaired surrogates, literal non-ASCII, null vs empty string).

## What the contract fixes, and what it leaves open

Fixed by the contract (§2.1–§2.7, §2.9):

- a minimal protected core (`event_id`, `occurred_at`, `principal_id`,
  `event_type`, `tool_name`, `outcome`, `previous_hash`, `event_hash`);
- a type-keyed `extensions` object, canonicalized into the same preimage, so
  extension data is protected by the same chain and a type cannot be swapped;
- the canonical form: sorted keys at every level, string/boolean/null values
  only (no bare numbers), NFC, U+0020-only trim, control characters and unpaired
  surrogates rejected, minimal escaping, UTF-8;
- the chain: `event_hash = SHA-256(canonical form)`, `previous_hash` threading
  within a segment;
- a verification procedure any third party can run over an exported record set;
- a structured attestation manifest for the one property that is not observable
  in the records: append-only enforcement at the store.

Left to the implementation: storage engine, wire protocol, which layer authors
the record, retention, export format, and every extension beyond the registered
ones.

## Registered extensions

| Type id | Registered by | Status |
|---|---|---|
| `caller-governance` | this specification (§2.2) | fully specified |
| `runtime-security` | its implementer, text folded into §2.2 | fully specified |
| `admission-control` | ATSA (MCP PR #2809), in its own text | by reference |

To register a new extension, open an issue with the §2.2 checklist: type id,
REQUIRED and OPTIONAL fields with types, the `event_type` vocabulary it
recognizes, and how its decision evidence binds to the core `outcome`. New
extensions never change §2.1, §2.3, or §2.4.

## Implementations

- **Reference implementation:** [Governed Intelligence Framework (gif)](https://github.com/notboatanchor/gif),
  Apache-2.0. Implements the core, the chain, and the `caller-governance`
  extension, enforces append-only at the storage layer, and mirrors `vectors/`
  verbatim. It does strictly more than this contract requires; the contract
  admits other implementation paths.
- Independent implementations of the same construction under other extensions
  exist (spec, Reference Implementation and Appendix A).

## Versioning

The document carries a semantic version. The canonical form carries its own
identifier (`audit-record-contract/1`), declared in every attestation manifest.
A change that alters what the vectors pin is a new canonical-form version, never
a patch; chains produced under an earlier form stay verifiable under it.

## Contributing and security

See [`CONTRIBUTING.md`](CONTRIBUTING.md) (DCO sign-off, AI-assisted
contribution policy, no response SLA) and [`SECURITY.md`](SECURITY.md)
(`security@notboatanchor.com`).

## License

Apache-2.0. Copyright 2026 Notboatanchor Labs LLC. See [`LICENSE`](LICENSE)
and [`NOTICE`](NOTICE).
