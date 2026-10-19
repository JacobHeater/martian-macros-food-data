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
| `generic-<date>.pack.gz` | Common foods with household measures: USDA Foundation Foods, SR Legacy and, since 2026-10-19, FNDDS (foods as eaten: mixed dishes, restaurant-style foods). About 13,000 foods. |
| `barcode_us-<date>.pack.gz` | Packaged products sold in the United States, found by barcode or by name (USDA Branded Foods and Open Food Facts). About 521,000 products. |
| `manifest.json` | Each pack's size and SHA-256, which the app checks before installing. |
| `report.txt`, `coverage.txt` | What the build read, wrote and dropped per source, and the share of foods stating each nutrient. |

A pack is a gzip-compressed, read-only SQLite file (format version 3 since
2026-10-19, defined by `apps/mobile/src/foodCatalog/FoodPackFormat.ts` in the
app repository; format 1 packs carried calories, the macros, fiber, sodium and
alcohol, format 3 adds thirteen more nutrients and sugar alcohols). Each food records which source
it came from and its id there. Foods the sources disagree about are marked for
the user to check; no food is described as verified.

## Where the data comes from

- **Open Food Facts** (<https://world.openfoodfacts.org>), a collaborative
  database. Its database is available under the
  [Open Database License (ODbL) 1.0](https://opendatacommons.org/licenses/odbl/1-0/),
  and its individual contents under the Database Contents License. See
  [ATTRIBUTION.md](ATTRIBUTION.md).
- **USDA FoodData Central** (<https://fdc.nal.usda.gov>), published by the US
  Department of Agriculture: Foundation Foods, SR Legacy, Branded Foods and
  the Food and Nutrient Database for Dietary Studies (FNDDS). We understand
  it to be in the public domain (CC0 1.0), and have not yet checked that
  against USDA's own statement.

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
(`apps/mobile/src/foodPipeline`; the build needs the DuckDB command-line
tool). Each release names the commit it was built from.
The same sources give byte-identical packs.
