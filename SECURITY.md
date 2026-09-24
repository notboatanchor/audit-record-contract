# Security Policy

## Supported Versions

| Version | Supported            |
| ------- | --------------------- |
| 1.x     | :white_check_mark:   |
| < 1.0   | :x:                   |

`< 1.0` covers pre-release drafts.

## Reporting a Vulnerability

**Do not file a public GitHub issue for security vulnerabilities.** Use the
private channel below so the issue can be triaged and patched before public
disclosure.

Email: **security@notboatanchor.com**

Please include:

- A description of the vulnerability and its impact
- Steps to reproduce (proof-of-concept code, configuration, or commands)
- The affected version (tag, branch, or commit SHA)
- Your name and any disclosure preferences (credit / anonymous)

GitHub's [private vulnerability reporting](https://docs.github.com/en/code-security/security-advisories/guidance-on-reporting-and-writing-information-about-vulnerabilities/privately-reporting-a-security-vulnerability)
is also enabled on this repository if you prefer that channel.

## Scope

In scope: defects in the normative text that let a non-conforming record verify, or a conforming record fail, on the reference verifier; defects in `vectors/` (a vector that passes a broken verifier). Out of scope: the reference implementation — report those to the gif repository's `SECURITY.md` (https://github.com/notboatanchor/gif).

## Response Timeline

This project is currently maintained by a solo maintainer. Best-effort response
targets:

- **Acknowledgement:** within 5 business days
- **Triage and severity assessment:** within 10 business days
- **Patch landed (or detailed mitigation):** depends on severity and
  complexity; communicated during triage

Coordinated disclosure is preferred. We aim to publish a fix and advisory
together, with credit to the reporter if they want it.
