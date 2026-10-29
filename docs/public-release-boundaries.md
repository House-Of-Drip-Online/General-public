# Public Release and Disclosure Boundaries

## Purpose

This document defines a conservative review boundary for materials considered for public release in the MAEVN Technologies portfolio. It is process guidance, not legal advice and not a determination of ownership, patentability, or freedom to publish.

## Suitable for public consideration

Subject to ordinary accuracy, rights, and security review, public materials may include:

- High-level project descriptions and intended use cases.
- General engineering principles and documented limitations.
- Public interfaces and specifications intentionally approved for open publication.
- Synthetic examples that do not encode confidential information or reveal protected implementation details.
- Test methodology, reproducible results, and evaluation summaries that do not expose restricted data or sensitive system behavior.
- Contribution guidance, governance notes, and project status descriptions.

## Hold for review

Do not publish without specific authorization and appropriate review:

- Source code or implementation details designated as private.
- Unfiled invention disclosures, enabling technical details, or material prepared for patent evaluation.
- Proprietary algorithms, internal decision rules, private model configurations, or non-public system architecture.
- Credentials, tokens, private keys, internal endpoints, security-sensitive deployment details, or incident data.
- Customer or partner information, personal data, restricted datasets, and media without verified rights and permissions.
- Confidential contracts, pricing, internal financials, or non-public business strategy.
- Third-party material whose license or publication rights are unclear.

## Pre-publication checklist

Before merging a proposed public addition, confirm:

- [ ] The intended audience and publication purpose are clear.
- [ ] The document contains no source code, secrets, private data, or restricted attachments.
- [ ] Potential invention disclosures have been referred for review before public disclosure.
- [ ] Ownership, permissions, and third-party license obligations have been checked.
- [ ] Technical statements are accurate and distinguish proposals from demonstrated capabilities.
- [ ] Examples and metrics include sufficient context to avoid misleading claims.
- [ ] A reviewer has checked links, metadata, commit history implications, and attached files.
- [ ] The repository's license and contribution terms are consistent with the intended release.

## Important limitations

A checklist cannot guarantee that a disclosure contains no intellectual property or that publication has no legal consequences. Public repositories are searchable and may be copied or archived. Removing material later may not remove copies or undo the effects of prior disclosure. Seek qualified legal advice when patent rights, trade secrets, licensing, likeness rights, or ownership are uncertain.

## Default rule

When a proposed change may reveal a non-public method, invention, dataset, or implementation detail, hold it from public release until an authorized review resolves the concern.
