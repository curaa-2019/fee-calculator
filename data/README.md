# Care-home BD contact dataset

Business-development contact dataset for the five Curaa homes, built via live web research (2026-07-03). Covers the "official orgs first" tier the brief prioritised: **ICB leadership, hospital discharge/PALS teams, and local-authority adult social care commissioning**, plus SOLLA care-fees advisers and hospice/palliative contacts picked up opportunistically. Dementia cafés, faith/community organisations, carer centres/discharge charities (beyond Age UK Bucks), ABI/PI/rehab/insurer contacts, and GP practice managers were **not** researched this pass — out of scope for this session, listed as follow-up below.

## Files
- `care_home_bd_contacts.csv` — 44 contact rows, columns match the brief's schema plus `email_inferred`, `phone_role`, `notes` (useful for Airtable/HubSpot import and outreach QA).
- `coverage_log.csv` — home × category counts of contacts found / with email / with phone.

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

## Coverage vs. the brief's completeness threshold
The brief asks for 3–5 contacts per category per home across ICB, hospital discharge, LA commissioning, care-fees advisers, and dementia support. This pass hit or came close on **ICB, hospital discharge, and LA commissioning** for most homes (see `coverage_log.csv`); **care-fees advisers** are thin (0–1 per home — SOLLA's directory is an interactive postcode search tool that isn't indexable by search, so it needs a direct visit); **dementia cafés, faith/community, and carer centres were not attempted** this pass. Named individuals (vs. generic team mailboxes/switchboards) are scarce for hospital discharge teams specifically — NHS trusts generally publish PALS/team contacts rather than named discharge coordinators.

## Suggested follow-up
1. Re-run with working WebFetch to pull full ICB board pages and verify the flagged low-confidence rows.
2. Manually query the SOLLA "Find an adviser" tool (societyoflaterlifeadvisers.co.uk) by postcode for each home — it's a JS search form, not indexable by search engines.
3. Research the remaining categories: dementia cafés/Alzheimer's Society local services, faith/community contacts (A Church Near You + diocesan/mosque directories), carer centres/discharge charities, ABI/PI/rehab/insurer contacts, GP practice managers.
