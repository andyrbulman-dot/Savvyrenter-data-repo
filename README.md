# Savvy Renter — data

Open government housing data, cut into small files so a web page can fetch the
one piece it needs instead of a whole database.

Served from **https://data.savvyrenter.co.uk/** and used by
[savvyrenter.co.uk](https://www.savvyrenter.co.uk/). There is no server and no
API: every file is static JSON, fetched straight from the browser.

Anyone else is welcome to use it. See [licence](#licence) below.

---

## What is in here

| Path | What it holds | Size |
|---|---|---|
| `/v1/outcodes/<OUTCODE>.json` | Every live UK postcode in that outcode, with its local authority, police force and coordinates | ~16 KB each, 2,976 files |
| `/v1/outcodes-index.json` | A list of every outcode that exists | small |
| `/v1/rents/<AREA CODE>.json` | Average private rent by month for one local authority, January 2015 onwards | ~5 KB each, 350 files |
| `/v1/rents-index.json` | Area code to area name | small |
| `/v1/lha-rates.json` | Local Housing Allowance rates for all 192 Broad Rental Market Areas, by year | ~52 KB |

---

## How a lookup works

Three fetches at most, and the last two are cacheable forever.

1. Take the postcode, split it at the space: `PL4 6JJ` → outcode `PL4`, unit `6JJ`.
2. Fetch `/v1/outcodes/PL4.json` and read the entry for `6JJ`. That gives the
   local authority code and the coordinates.
3. Fetch `/v1/rents/<local authority code>.json` for the rent history, and
   `/v1/lha-rates.json` for the housing allowance rates.

### The outcode file

```json
{
  "lad": ["E06000026"],
  "pfa": ["E23000035"],
  "p": {
    "6JJ": [0, 0, 50.3841, -4.1401]
  }
}
```

`lad` and `pfa` are lookup tables for that file: local authority codes and police
force codes, listed once and referred to by position. Each postcode entry is
`[index into lad, index into pfa, latitude, longitude]`. Coordinates are to four
decimal places, about 11 metres — the accuracy of a postcode centroid, not of a
building.

Only **live** postcodes are included. Terminated ones are dropped.

### The rent file

```json
{
  "code": "E06000026",
  "name": "Plymouth",
  "months": [["2015-01", 595, 450, 575, 675, 895]]
}
```

Each month is `[month, all properties, 1 bed, 2 bed, 3 bed, 4+ bed]`, in pounds
per month. A `null` means ONS did not publish a figure for that series.

### The LHA file

```json
{
  "years": ["2022", "2023", "2024", "2025", "2026"],
  "brma": {
    "PLYMOUTH": {
      "name": "Plymouth",
      "nation": "E",
      "rates": { "2026": [325.0, 450.0, 575.0, 695.0, 895.0] }
    }
  }
}
```

Each year is `[shared accommodation, 1 bed, 2 bed, 3 bed, 4 bed]`, monthly, in
pounds. The year is the April the rate takes effect. Keys are normalised names
(uppercase, "and" spelled out); `name` is the published spelling.

Finding the right BRMA for a postcode needs the BRMA lookup, which is a separate
dataset — see [ATTRIBUTION.md](ATTRIBUTION.md).

---

## Building it

The scripts that produce these files live alongside the site. They read the
published source files and write this repository's contents. Nothing is
hand-edited: if a figure here is wrong, it is wrong in the source or wrong in the
script, and either way re-running the build fixes it.

Rebuild when a new source release comes out:

- **Postcode lookup** — ONS publish a new NSPL a few times a year
- **Rent index** — ONS publish monthly; each release contains the whole history,
  so only the newest file is needed
- **LHA rates** — DWP publish annually, effective each April

---

## Versioning

Everything lives under `/v1/`. If the shape of a file has to change, the new
shape is published under `/v2/` and `/v1/` is left alone until nothing is using
it. That way a data rebuild can never break a page that is already live.

---

## Licence

Two licences, because there are two kinds of thing here.

- **The data**, everything under `/v1/` — Open Government Licence v3.0.
  See [DATA-LICENCE.md](DATA-LICENCE.md).
- **The code** — MIT. See [LICENSE](LICENSE).

If you reuse the data you must carry the attribution for whichever source it came
from. They are all set out in [ATTRIBUTION.md](ATTRIBUTION.md), and each JSON
file repeats its own source and licence internally so it stays attributed even on
its own.

None of this is legal or financial advice, and none of it is a substitute for the
original publications, which are linked for every dataset.

---

## Contact

Suggestions, corrections, or a dataset worth adding: there is a feedback button
on [savvyrenter.co.uk](https://www.savvyrenter.co.uk/).
