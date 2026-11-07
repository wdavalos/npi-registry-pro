# NPI Registry Pro

Search every US healthcare provider in the CMS NPPES registry: 8.7M+ individual and organizational providers with NPI numbers, specialty taxonomy, addresses, phones and authorized officials. Free government data. No key, no proxies.

**Comparison:** [sourabhbgp/npi-registry-scraper](https://apify.com/sourabhbgp/npi-registry-scraper) (the category leader) returns basic registry rows. NPI Registry Pro adds the specialty filter (Dentist, Internal Medicine, Chiropractor and more), an individual/organization switch, an active-only filter so you never pay for a deactivated record, authorized-official contact details, practice locations and declared EHR endpoints.

## What you get per row

| Field | Example |
| --- | --- |
| npi | 1093655656 |
| name | 32 SMILES DENTAL LLC |
| provider_type | Individual or Organization |
| status | Active |
| primary_specialty | Dentist, General Practice |
| taxonomy_code | 1223G0001X |
| location_address_1, location_city, location_state, location_zip | 10650 CULEBRA RD STE 136, SAN ANTONIO, TX, 782514950 |
| location_phone, location_fax | 210-888-5832 |
| mailing_address_1, mailing_city, mailing_state, mailing_zip | full mailing address |
| authorized_official, authorized_official_title, authorized_official_credential, authorized_official_phone | SIDRA IQBAL, Dr, DDS |
| enumeration_date, last_updated | 2026-03-31 |
| ehr_endpoint_type, ehr_endpoint_url | the provider's declared EHR endpoint, when registered |

## How to search

Combine any of these filters: organization name, provider first/last name, specialty (NUCC taxonomy description, e.g. Dentist or Family Medicine), provider type (NPI-1 individual or NPI-2 organization), and location (state + city, or ZIP). The registry API needs a city or ZIP code together with a state; the actor pages the registry automatically in batches of 200 until it reaches your max results. `only_active` drops deactivated records before they are saved.

## Input

| Field | Type | Description |
| --- | --- | --- |
| organization_name | text | Organization or practice name, e.g. Mayo Clinic |
| first_name / last_name | text | Individual provider name (NPI-1) |
| taxonomy_description | text | Specialty, e.g. Dentist, Internal Medicine, Radiology |
| enumeration_type | select | Any, Individual (NPI-1), Organizations (NPI-2) |
| state / city / postal_code | text | Location filters. ZIP alone also works |
| address_purpose | select | Which address the location filters apply to: primary practice, practice location or mailing |
| max_items | number | Max providers to return (default 10, up to 2,000) |
| only_active | checkbox | Skip deactivated records before they are saved (default on) |
| include_practice_locations | checkbox | Add all additional practice locations to each row |

## Output

A default dataset of provider rows, one row per provider, shaped as the table above.

## Pricing

| Item | Price |
| --- | --- |
| Actor start | $0.005 per run |
| Each provider row | $0.002 ($2.00 per 1,000 providers) |

Compute is minimal: the actor calls CMS's free API over plain HTTP with no proxy, so your cost per 1,000 providers stays close to the listed price.

## Use cases

- **Healthcare lead generation.** Build lists of dentists, primary-care physicians, chiropractors or any specialty by city or ZIP, with phone numbers and authorized officials.
- **Provider verification.** Check an NPI number, confirm active status, specialty and practice address in one call.
- **Recruiting and staffing.** Map providers by state and specialty for placement pipelines.
- **Market analysis.** Count providers by specialty and geography; add practice locations for a full footprint.

## FAQ

**Is this data free?** The source is CMS's NPPES registry, a free public API. You pay only for the run and the rows returned.

**Why can't I search by state alone?** The registry API rejects a state without a city or ZIP. Add a city or ZIP code with your state; ZIP alone works by itself.

**How large can one run be?** Up to 2,000 providers per run. The registry pages results in batches of 200 and the actor pages automatically.

**Do deactivated providers get billed?** No. With `only_active` on, deactivated records are filtered before they are saved, so you never pay for a dead row.

**Can I get group practices only?** Yes. Set provider type to Organizations (NPI-2). Group practices, hospitals and clinics are all NPI-2.

**What are EHR endpoints?** Some providers register FHIR or HL7 endpoints with CMS. The row carries the endpoint type and URL when the provider has one.

**Browse the full catalog:** [ScraperFleet](https://scraperfleet.com/actors/npi-registry-pro/) has this actor plus 113 others, with comparisons and pricing.

Pair it with [B2B Lead Gen Suite MCP](https://apify.com/red.cars/b2b-lead-gen-suite-mcp) to turn provider lists into outreach-ready contacts.
