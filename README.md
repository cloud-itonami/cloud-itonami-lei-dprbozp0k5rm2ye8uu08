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

## Design rationale

See ADR-2607110300 in `com-junkawasaki/root` (`90-docs/adr/`) for why this repo exists,
why it is keyed by LEI rather than GTIN or ticker, and why full-text archival (with
provenance) was chosen over excerpt-only storage.
