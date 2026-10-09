# Martian Macros food data

Offline food databases for the [Martian Macros](https://github.com/JacobHeater/martian-macros)
app: nutrition values per 100 g, barcodes and household servings for foods sold
in the United States. The app downloads them from this repository's
[Releases](../../releases) when the user asks, and reads them without a
connection afterwards.

**Status: provisional.** These files and the licensing notes below were put
together by the Martian Macros project. **No lawyer has reviewed them.** If you
reuse the data, read the licenses yourself.

## What a release contains

| File | What it is |
|---|---|
| `generic-<date>.pack.gz` | Common foods with household measures (USDA Foundation Foods and SR Legacy). About 8,000 foods. |
| `barcode_us-<date>.pack.gz` | Packaged products sold in the United States, found by barcode or by name (USDA Branded Foods and Open Food Facts). About 456,000 products. |
| `manifest.json` | Each pack's size and SHA-256, which the app checks before installing. |

A pack is a gzip-compressed, read-only SQLite file (format version 1, defined by
`packages/food_catalog` in the app repository). Each food records which source
it came from and its id there. Foods the sources disagree about are marked for
the user to check; no food is described as verified.

## Where the data comes from

- **Open Food Facts** (<https://world.openfoodfacts.org>), a collaborative
  database. Its database is available under the
  [Open Database License (ODbL) 1.0](https://opendatacommons.org/licenses/odbl/1-0/),
  and its individual contents under the Database Contents License. See
  [ATTRIBUTION.md](ATTRIBUTION.md).
- **USDA FoodData Central** (<https://fdc.nal.usda.gov>), published by the US
  Department of Agriculture. We understand it to be in the public domain
  (CC0 1.0), and have not yet checked that against USDA's own statement.

The exact source files and versions behind each release are listed in its
release notes and in each pack's header.

## License

The packs in this repository are a database derived in part from Open Food
Facts, and are made available under the **Open Database License 1.0**: see
[LICENSE](LICENSE). In short, if you use them you must credit Open Food Facts
(and USDA FoodData Central), and if you publish a database derived from them
you must offer it under the same license. **Product images are not included**
(Open Food Facts publishes its images under a different license, CC BY-SA).

The software that builds these files is in the app repository and is not
covered by this license.

## How the files are built

`./mm food fetch` and `./mm food build`, then `./mm food package`, in the
[app repository](https://github.com/JacobHeater/martian-macros)
(`packages/food_pipeline`). Each release names the commit it was built from.
The same sources give byte-identical packs.
