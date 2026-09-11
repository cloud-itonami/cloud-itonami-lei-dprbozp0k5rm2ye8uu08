# cloud-itonami-lei-dprbozp0k5rm2ye8uu08

> **Independent third-party archive/analysis. Not affiliated with, endorsed by, or sponsored by Lockheed Martin Corporation.**

This repository archives the publicly published privacy-policy of
**Lockheed Martin Corporation**, with source-url and retrieval-date provenance, per
[ADR-2607110300](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607110300-cloud-itonami-lei-corporate-tos-catalog.md)
(`cloud-itonami-lei-corporate-tos-catalog`, `com-junkawasaki/root`). It is a read-only
reference/archive repository — it does not act, propose, or execute anything on the
company's behalf, and is not a governed Advisor/Governor actor.

## Company identity

- **Legal name**: Lockheed Martin Corporation
- **LEI (ISO 17442)**: [DPRBOZP0K5RM2YE8UU08](https://search.gleif.org/#/record/DPRBOZP0K5RM2YE8UU08) (GLEIF-verified)
- **Jurisdiction**: US
- **Website**: https://www.lockheedmartin.com
- **Ticker**: LMT (NYSE)

## Contents

- `80-data/public/tos.journal.edn` — EDN quad-log of archived legal documents,
  each entry carrying `:tos/full-text`, `:tos/source-url`, `:tos/retrieved-at`,
  `:tos/sha256`, `:tos/doc-type`, and a `:tos/supersedes` chain for future revisions.
- `NOTICE` — copyright/attribution statement for the archived third-party text.
- `blueprint.edn` — machine-readable company identity record.
- `facts.edn` — 11 verified registry facts with per-fact provenance (9 about the
  entity itself, 2 about its directly consolidated subsidiaries). **Generated** —
  see below.
- `scripts/verify-facts.cljk` — re-fetches every source `facts.edn` cites and fails if
  the live record disagrees. Vendored from `com-junkawasaki/root`
  (`scripts/lei-verify-facts.cljs`); fix issues in the canonical and re-vendor.

## Verifying the record

The LEI claims above used to be assertions with nothing in the repository behind
them. `facts.edn` now carries them as data, and every value in it was read out of
a public registry response whose URL and retrieval time sit next to the value:

```
kbb --backend sci scripts/verify-facts.cljk           # check the recorded facts against the live sources
kbb --backend sci scripts/verify-facts.cljk --write   # re-fetch and rewrite facts.edn
```

Eleven GLEIF/ISO requests back the file (`CHECKED 11` when it was written,
2026-08-23T03:48Z, golden copy 2026-08-22T16:00Z) — the LEI record (legal name
`LOCKHEED MARTIN CORPORATION`, jurisdiction `US-MD`, entity **ACTIVE**,
registration **ISSUED** with the next renewal due 2027-05-29, last updated
2026-05-06, `FULLY_CORROBORATED`, conformity flag `CONFORMING`; entity status
and registration status are different fields and are recorded separately), its
**44 ISINs**, read from `meta.pagination.total` of the first of 3 pages — the
count is recorded, the list is deliberately not mirrored, because at this
issuer's volume instruments mature and are issued often enough that a mirrored
list would go red for reasons that are not "the citation broke"; walk the cited
URL's page range to enumerate them — its managing LOU and LEI-issuer
accreditation (Bloomberg Finance L.P., LEI `5493001KJTIIGC8Y1R12`, accredited
2017-04-13), registration authority `RA000614` (Business Services, Maryland
Department of Assessments and Taxation, registration number `D03964756`),
ISO 20275 legal form `HLR4` (`Stock Corporation`, US-MD), reporting exceptions
at both consolidation levels (`NON_CONSOLIDATING` — GLEIF records no parent,
direct or ultimate, because this entity is the top of its own consolidation),
and **2 direct children**, read from `meta.pagination.total` of a 15-per-page
request and each mirrored as its own `:direct-child` entity: Lockheed Martin
TAS International Corporation (`5493000MTGV3EJXEFM23`, US-TX) and LOCKHEED
MARTIN INVESTMENT MANAGEMENT COMPANY (`X2RCP68VSVZIHLC2RN17`, US-DE). The
`direct-parent` and `ultimate-parent` endpoints answered `404` because GLEIF
publishes the exception side of that pair for this entity, which the checker
treats as a fact rather than a failure.

The checker's exit codes are three, not two: `0` every recorded fact matches the
live sources, `1` a citation broke or a fact drifted, `3` the check could not be
performed at all — an absent `facts.edn`, or every request failing at the
transport level. A check that could not run must not be indistinguishable from a
check that ran and found nothing, so it refuses to report a pass rather than
exiting 0. All outcomes were exercised before this landed: unmodified `0`;
`:registration/next-renewal-date` edited one year forward → `1` naming
`DRIFT gleif-lei-record :registration/next-renewal-date`; the `gleif-isins`
entity deleted → `1` naming `ADDED gleif-isins`; a direct child's
`:company/legal-name` shortened → `1` naming
`DRIFT gleif-direct-child-x2rcp68vsvzihlc2rn17 :company/legal-name`; the GLEIF
host in the checker rewritten to an unresolvable name → `3` (`INCONCLUSIVE …
refusing to report a pass`). Rewriting the host only inside `facts.edn` is *not*
the transport case: the live URLs are derived from `blueprint.edn`, so that edit
reports as 11 `DRIFT … :source/url` findings (`1`) — a recorded citation that no
longer names its source is drift, not an outage.

## Design rationale

See ADR-2607110300 in `com-junkawasaki/root` (`90-docs/adr/`) for why this repo exists,
why it is keyed by LEI rather than GTIN or ticker, and why full-text archival (with
provenance) was chosen over excerpt-only storage.
