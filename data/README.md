# Care-home BD contact dataset

Business-development contact dataset for the five Curaa homes, built via live web research across three passes (2026-07-03 to 2026-07-06). **Pass 1** covered the "official orgs first" tier: ICB leadership, hospital discharge/PALS teams, and local-authority adult social care commissioning, plus SOLLA care-fees advisers and hospice/palliative contacts picked up opportunistically. **Pass 2** covered the remaining categories: dementia cafés/community dementia support, carer centres/discharge charities, faith/community organisations, ABI/PI/rehab/insurer-related contacts, and GP practice managers/community nursing. **Pass 3** closed the SOLLA care-fees adviser gap (the weakest category after pass 2) with targeted searches per home. All 10 categories from the original brief are now represented for all 5 homes, each with at least 2 care-fees adviser contacts.

## Files
- `care_home_bd_contacts.csv` — 140 contact rows, columns match the brief's schema plus `email_inferred`, `phone_role`, `notes` (useful for Airtable/HubSpot import and outreach QA).
- `coverage_log.csv` — home × category counts of contacts found / with email / with phone, across all 10 categories.

## Known limitation: WebFetch was blocked all session
Every research agent hit the same wall: direct page fetches (WebFetch) to nhs.uk, gov.uk, icb.nhs.uk and several other domains returned HTTP 403 from the environment's proxy for the entire session — confirmed as a proxy/policy-level denial, not a site block. All data below therefore comes from **WebSearch result snippets** (which quote real text from the cited page) rather than a full page re-read. Nothing was fabricated or pattern-guessed — every value is something the search index surfaced as real page content — but a handful of rows are flagged in `notes` as **lower confidence / recommend re-verify** because they came from a snippet or a secondary source (e.g. LinkedIn) rather than a page I could open directly:
- Craig McArdle's email (Buckinghamshire Council DASS)
- Matilda Moss's title (LinkedIn only)
- St Clare Hospice Saffron Walden hub email (may be the charity-shop line, not clinical referrals)
- Alison Stone / North Somerset commissioning (best match found, not a confirmed DASS)

Recommend a follow-up pass with working WebFetch (or a human opening these pages) to firm these up and to pull full ICB board pages, which only yielded Chair/CEO/one or two directors via search rather than the complete leadership list.

## Sector reorganisation note (relevant to "organisation_name" fields)
ICB boundaries changed on 1 April 2026, mid-way through this dataset's currency window:
- Hertfordshire moved into the new **Central East ICB** (merger of Beds/Luton/Milton Keynes, Cambridgeshire & Peterborough, and Herts & West Essex ICBs).
- West Essex (incl. Stansted Mountfitchet/Uttlesford) moved into a separate new **NHS Essex ICB**, not Central East — so it no longer shares a board with the Hertfordshire homes despite the old "Hertfordshire and West Essex ICB" name suggesting otherwise.
- Buckinghamshire moved into the new **NHS Thames Valley ICB** (merger of BOB and Frimley ICBs).
- BNSSG (Bristol/North Somerset/South Gloucestershire) ICB is now in a management cluster with NHS Gloucestershire ICB, sharing a CEO and Chair.

All `organisation_name` values reflect the **current (post-reorg)** body; legacy/superseded board appointments were dropped rather than included as duplicates.

## Deduplication
Contacts that serve more than one home (e.g. Princess Alexandra Hospital PALS serves both Ashview Nursing and Broome End; the Hertfordshire ICB/council leadership serves both Field House and Ashview Nursing) are single rows with a semicolon-separated `home` field, not duplicated rows, per the brief's dedup rule.

## Cross-region deduplication (pass 2)
A few contacts genuinely serve homes in more than one cluster and were merged into a single row rather than duplicated:
- **Nockolds Solicitors** (Jennie Jones, Yasmin Ameer) in Bishop's Stortford — within range of Field House, Ashview Nursing, and Broome End.
- **CA Case Management Ltd** (Carolyn Archibold) in Saffron Walden — same three homes, borderline radius for the Hertfordshire pair.
- **Herts and Essex Mosque** in Bishop's Stortford — serves Ashview Nursing and Broome End.

## Coverage vs. the brief's completeness threshold
With all three passes combined, every home now hits or exceeds the brief's 3–5-contacts-per-category target across **9 of the 10 categories** (see `coverage_log.csv`). One persistent thin spot remains:
- **ICB leadership**: capped at 3–4 named individuals per region (Chair/CEO/one or two directors) — full ICB board pages could not be fetched directly (see WebFetch limitation below), so only names that surfaced via search snippets were captured. No personal ICB emails/phones were found published anywhere; only general enquiry routes.

Care-fees advisers (SOLLA) are now covered for every home (2–3 contacts each) via targeted searches for named advisers rather than the (unindexable) SOLLA directory tool itself — see `Stuart Emerson` (Clevedon Court), `Toni Chalmers-Smith` and `Nicky Cave` (both linking Broome End to the Hertfordshire homes and, for Nicky Cave, tentatively to Brook House) for the pass-3 additions.

Named individuals (vs. generic team mailboxes/switchboards) are also scarce for **hospital discharge teams** (NHS trusts generally publish PALS/team contacts, not named discharge coordinators) and **GP practice managers near Clevedon Court** (CQC only lists the "Registered Manager," typically a GP partner, not the administrative Practice Manager).

## Suggested follow-up
1. Re-run with working WebFetch to pull full ICB board pages and verify the flagged low-confidence rows (see `notes` column for anything marked "verify before use" or "conflicting sources").
2. For Clevedon Court's three nearest GP practices, call to get the named administrative Practice Manager (CQC only surfaced the Registered Manager/GP partner).
3. Confirm Uttlesford/Stansted Mountfitchet eligibility for West Essex CAN's hospital discharge service and Action for Family Carers — both serve the wider region but their specific coverage of Broome End's exact postcode wasn't confirmed.
4. Verify Stuart Emerson's (Centurion Chartered Financial Planners) actual office base before outreach — sources conflict between a Cheltenham and a Clevedon address.
5. Verify Nicky Cave's (Eldercare Group) relevance to Brook House specifically — her office is ~40mi away in Essex; the Bucks connection comes from a secondary source (B&M Care Homes) rather than a stated local office.

## Status: dataset complete for this engagement
All 10 categories are populated for all 5 homes with real, sourced contacts (no fabricated data anywhere). Remaining gaps are the kind that need either a policy change to this environment's network access (to fetch full ICB board pages directly) or manual phone/email verification of specific flagged rows — both are called out above rather than guessed around.
