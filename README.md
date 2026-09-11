# cloud-itonami-lei-549300gzkuliz0wow665

> **Independent third-party archive/analysis. Not affiliated with, endorsed by, or sponsored by The Walt Disney Company.**

This repository archives the publicly published Terms of Use / Terms and Conditions of
**The Walt Disney Company**, with source-url and retrieval-date provenance, per
[ADR-2607110300](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607110300-cloud-itonami-lei-corporate-tos-catalog.md)
(`cloud-itonami-lei-corporate-tos-catalog`, `com-junkawasaki/root`). It is a read-only
reference/archive repository — it does not act, propose, or execute anything on the
company's behalf, and is not a governed Advisor/Governor actor.

## Company identity

- **Legal name**: The Walt Disney Company
- **LEI (ISO 17442)**: [549300GZKULIZ0WOW665](https://search.gleif.org/#/record/549300GZKULIZ0WOW665) (GLEIF-verified)
- **Jurisdiction**: US-DE
- **Website**: https://thewaltdisneycompany.com
- **Ticker**: DIS (NYSE)

## Contents

- `80-data/public/tos.journal.edn` — EDN quad-log of archived Terms of Use documents,
  each entry carrying `:tos/full-text`, `:tos/source-url`, `:tos/retrieved-at`,
  `:tos/sha256`, `:tos/doc-type`, and a `:tos/supersedes` chain for future revisions.
- `NOTICE` — copyright/attribution statement for the archived third-party text.
- `blueprint.edn` — machine-readable company identity record.
- `facts.edn` — 20 verified registry facts with per-fact provenance. **Generated** — see below.
- `scripts/verify-facts.cljk` — re-fetches every source `facts.edn` cites and fails if
  the live record disagrees. Vendored from `com-junkawasaki/root`
  (`scripts/lei-verify-facts.cljs`); fix issues in the canonical and re-vendor.

## Verifying the record

The identity table above used to be assertions with nothing in the repository
behind them. `facts.edn` now carries them as data, and every value in it was read
out of a public registry response whose URL and retrieval time sit next to the
value:

```
kbb --backend sci scripts/verify-facts.cljk           # check the recorded facts against the live sources
kbb --backend sci scripts/verify-facts.cljk --write   # re-fetch and rewrite facts.edn
```

Eleven GLEIF/ISO URLs were fetched and 20 facts recorded. The LEI record: legal
name as GLEIF spells it, **`THE WALT DISNEY COMPANY`**, upper case, `en`; entity
**ACTIVE**; registration **ISSUED**, `FULLY_CORROBORATED`, `CONFORMING`;
Delaware file number `6931540` at `RA000602` (Delaware Division of
Corporations); legal form `XTIQ`, resolved via ISO 20275 to "Corporation"
(US-DE); OpenCorporates id `us_de/6931540`, S&P Global id `191564`; no BIC —
the empty list is a measured empty. Two things in this record read differently
from what the company's public history suggests, and both are what GLEIF
actually publishes: the entity creation date is **`2018-06-14`**, not 1923 —
this Delaware corporation is the holding company created for the 21st Century
Fox acquisition restructuring, which took the "The Walt Disney Company" name in
2019; the LEI record itself names no predecessor, so the 1923 studio history is
context here, not a claim this file verifies. And both the legal address *and*
the headquarters address are the registered-agent address (`C/O CORPORATION
SERVICE COMPANY, 251 LITTLE FALLS DRIVE, 19808, WILMINGTON, US-DE, US`) — the
record does not carry the Burbank studio address at all.

The relationship facts: GLEIF maps **166** instrument identifiers (ISINs) to
this LEI, read from `meta.pagination.total` of the cited page — at that volume
the list is counted, not mirrored (each count's `:source/note` says which). No
direct or ultimate parent is reported: GLEIF publishes a
parent-reporting-exception at both consolidation levels, reason
`NON_CONSOLIDATING` — this entity is the top of its own accounting
consolidation tree. **11 direct children** are reported, and all 11 are
mirrored into `facts.edn` with their own LEIs, names, statuses and source URLs
(Disney Enterprises, Inc., LUCASFILM ENTERTAINMENT COMPANY LTD. LLC, and nine
others). The managing LOU is Bloomberg Finance L.P.

The check has three exit codes, not two: `0` when every cited URL answered and
every recorded value still matches, `1` when a citation broke or a value
drifted (each difference is named, with the recorded and live values side by
side), and `3` when the check could not be performed at all — `facts.edn`
missing or empty, or GLEIF unreachable at the transport level — because a check
that could not run must not look like a check that ran and found nothing.
Before this landed, all three were shown against the live API: unmodified →
`0` (`OK all 20 recorded fact(s) still match the live sources`);
`:company/jurisdiction` edited `US-DE` → `FR` → `1`, naming each drifted
entity and `:company/jurisdiction` as `DRIFT`; `facts.edn` removed → `3`
(`INCONCLUSIVE … Refusing to report a pass`). The file was then regenerated
with `--write` and the check run once more → `0`.

## Design rationale

See ADR-2607110300 in `com-junkawasaki/root` (`90-docs/adr/`) for why this repo exists,
why it is keyed by LEI rather than GTIN or ticker, and why full-text archival (with
provenance) was chosen over excerpt-only storage.
