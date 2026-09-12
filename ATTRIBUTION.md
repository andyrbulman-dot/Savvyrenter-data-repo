# Attribution

Each dataset below is published under the Open Government Licence v3.0 and
carries a required acknowledgement. If you reuse any of this data, reproduce the
statement for whichever source it came from.

---

## Postcode lookup — `/v1/outcodes/`

Derived from the **National Statistics Postcode Lookup (May 2026)**, Office for
National Statistics.

> Contains OS data © Crown copyright and database right 2026
> Contains Royal Mail data © Royal Mail copyright and database right 2026
> Source: Office for National Statistics licensed under the Open Government Licence v.3.0

All three lines are required — Ordnance Survey and Royal Mail both hold rights in
the underlying data, not only ONS.

Source: <https://geoportal.statistics.gov.uk/>

What was changed: terminated postcodes removed; only the postcode, local
authority code, police force code and coordinates retained; coordinates rounded
to four decimal places; split into one file per outcode.

---

## Rent index — `/v1/rents/`

Derived from the **Price Index of Private Rents**, Office for National Statistics.

> Source: Office for National Statistics licensed under the Open Government Licence v.3.0

Source: <https://www.ons.gov.uk/economy/inflationandpriceindices/bulletins/privaterentandhousepricesuk/latest>

What was changed: the average rent series extracted from the published
spreadsheet for each local authority and split into one file per area. Index
values, monthly change and annual change columns were not carried over; only the
rental price figures, overall and by bedroom count.

---

## Local Housing Allowance rates — `/v1/lha-rates.json`

**Local Housing Allowance rates**, Department for Work and Pensions.

> Source: Department for Work and Pensions licensed under the Open Government Licence v3.0

Source: <https://www.gov.uk/government/publications/understanding-local-housing-allowance-rates>

What was changed: the annual rate tables for England, Scotland and Wales
combined into one file keyed by Broad Rental Market Area. Area names were
normalised where the published spelling varied between years (for example
"Crawley & Reigate" and "Crawley and Reigate", "Weston-S-Mare" and
"Weston-Super-Mare", "Flint" and "Flintshire"). The published spelling for the
most recent year is kept as the display name.

---

## Postcode to Broad Rental Market Area lookup

Bailey, N. (2025) *Postcode to Broad Rental Market Areas (BRMAs) Lookup v2.2*.
Urban Big Data Centre, University of Glasgow. doi:10.20394/mu6lw0x9

> Contains data from the Postcode to BRMA Lookup v2.2, Urban Big Data Centre,
> University of Glasgow, licensed under the Open Government Licence v3.0

Source: <https://data.ubdc.ac.uk/datasets/postcode-to-broad-rental-market-areas-brmas-lookup-v2-2-2025>

BRMA boundaries originate from Valuation Office Agency material obtained under
Freedom of Information and published by Owen Boswarva.

---

## Licence

Open Government Licence v3.0 —
<https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/>
