# Contributing to audit-record-contract

## Maintainer Note

This specification is currently maintained by one person. There is no response SLA on issues or pull requests. PRs will be reviewed when time allows. If you submit something, it may sit for a while — that is not a signal that it is unwanted.

Issues, pull requests, and comments written with AI tools are held to the [AI-Assisted Contributions](#ai-assisted-contributions) policy below. Undisclosed or unverified AI-generated submissions are closed without review.

---

## AI-Assisted Contributions

This project is itself developed with AI assistance, and says so — its commits carry co-author trailers naming the tool. AI-assisted contributions are welcome on the same terms. This policy covers issues, pull requests, and comments.

- **Disclose it.** If an AI tool wrote or substantially shaped your submission, say so in the issue or PR description: one line naming the tool and what it did. A co-author trailer on the commits does not replace the line in the description.
- **A human is accountable.** Whoever submits is the author. You have read and understood every line, you have run it yourself (for a PR, the vector set: `node --experimental-strip-types vectors/run.ts`), and you can answer review questions in your own words. "The model wrote that part" is not an answer.
- **No autonomous submissions.** An issue, PR, or comment filed by an agent without a human who asked for that specific submission and reviewed its content is not accepted.
- **Verify before you claim.** A bug report is reproduced by you against the actual code, not inferred by a model. A claim that the code is broken, drifts, or mismatches cites the file and line, or the spec section, the same rule this repository applies to itself. Suspected vulnerabilities follow `SECURITY.md` and the same bar: reproduced, not model-inferred.

**What happens otherwise.** A submission that is undisclosed AI output, that its submitter cannot explain, that was not run, or that is low-effort or bulk-generated (drive-by refactors, unreproduced "vulnerability" reports, documentation churn) is closed without review. The call is the maintainer's judgment and is not debated in the thread. A close under this policy is not a verdict on the person — the same change may be resubmitted with disclosure and verification. Repeated submissions of this kind may lead to a block.

Nothing here changes the Maintainer Note above: there is still no response or triage commitment, for AI-assisted submissions or any others.

---

## What Changes Need

- A change to the normative text in `spec/` that alters what the vectors pin is a new canonical-form version, not a patch. Open an issue first.
- A new vector must name the C-REC requirement it exercises and must pass on the reference verifier.
- An extension registration request opens an issue using the checklist in the spec's §2.2: type id; REQUIRED/OPTIONAL fields and types; `event_type` vocabulary; outcome binding.

---

## Sign-off

Contributions use the Developer Certificate of Origin: sign commits with `git commit -s` (https://developercertificate.org/).

---

## Running the Vectors

    node --experimental-strip-types vectors/run.ts

or

    npx tsx vectors/run.ts
