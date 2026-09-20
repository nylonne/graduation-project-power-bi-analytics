# Power Query Transformation Steps

This document records the Power Query M transformations supplied from the report’s Advanced Editor. The query names were not included with the pasted code, so the descriptions below identify each query by its output and transformation pattern rather than inventing a name.

## Shared source and preprocessing

The supplied queries combine the following eight project queries into one table:

1. One Kattameya Compound
2. Zahra North Coast
3. Degla Landmark
4. Skyline Katamya Compound
5. Degla Palms 6 October Compound
6. Lake Front 6
7. Crystal Plaza Maadi Compound
8. Rihana

The shared preprocessing sequence is:

1. Combine the eight project tables with `Table.Combine`.
2. Remove rows whose every field is blank or null.
3. Apply data types:
   - `رقم الهوية` and `رقم الوحدة` as text.
   - `سعر الوحدة`, `مجموع الدفعات المستحقة`, and `مجموع الدفعات المدفوعة` as whole numbers.
   - `نسبة الانجاز من الاستشاري الهندسي` and `POC` as percentages.
   - `Date` as a date.
   - `Project Name` as text.
4. Standardize four bank-name variants in the `البنك` column:

| Source value | Standardized value |
| --- | --- |
| `EGBANK - البنك المصري الخليجي` | `EGBANK` |
| `إي جي بنك (EGBANK)` | `EGBANK` |
| `البنك التجاري الدولي CIB` | `CIB` |
| `البنك التجاري الدولي (CIB)` | `CIB` |
5. Rename source columns for analysis:

| Source column | Output column |
| --- | --- |
| `اسم العميل` | `Customer Name` |
| `رقم الهوية` | `Customer ID` |
| `رقم الوحدة` | `Unit` |
| `كود الوحدة` | `Unit ID` |
| `سعر الوحدة` | `Price` |
| `جدول الدفعات` | `Installments` |
| `الدفعة 1` through `الدفعة 7` | `Installment 1` through `Installment 7` |
| `تاريخ عقد البيع` | `Contract Date` |
6. Remove `نسبة الانجاز من الاستشاري الهندسي`.

## Installment cleansing and status columns

For every installment column from `Installment 1` to `Installment 7`, the queries add a matching status field using these rules:

| Source text condition | Status |
| --- | --- |
| Contains `تم السداد` | `PAID` |
| Contains `غير مستحقة` | `NOT DUE` |
| Any other value | `NOT PAID` |

After the status fields are created, the transformations:

1. Replace `تم السداد` with an empty string in all seven installment fields.
2. Replace `غير مستحقة` with `0` in all seven installment fields.
3. In the supplied preprocessing variant, trim whitespace from all seven installment fields.
4. Convert all seven installment fields to whole numbers.

The status is calculated before the original Arabic status text is removed, preserving its meaning for analysis.

## Cleaned sales and installment dataset

One query continues from the shared preprocessing to produce the main cleaned dataset:

1. Rename `البنك` to `Bank` and `رقم عقد البيع` to `Contract Number`.
2. Standardize additional payment values in `Bank`:

| Source value | Standardized value |
| --- | --- |
| `كاش` | `Cash` |
| `البنك الأهلي المصري` | `NBE` |
| `QNB مصر` | `QNB` |
| `بنك الإسكندرية` | `ALEXBANK` |
| `كريدي أجريكول مصر` | `CAE` |
| `بنك القاهرة` | `BDC` |
| `البنك العربي الأفريقي الدولي` | `AAIB` |
| `بنك مصر` | `BM` |
| `بنك التعمير والإسكان` | `HDB` |
3. Rename `مجموع الدفعات المدفوعة` to `Paid Installments` and `مجموع الدفعات المستحقة` to `Remaining Installments`.
4. Apply the installment cleansing and status-column steps above.
5. Reorder the output into customer, unit, price, installment/status, payment, contract, date, and project fields.

## Payment-type lookup

One query starts from the same cleaned and bank-standardized data, then:

1. Keeps only `Bank`.
2. Removes duplicate bank values.
3. Adds `Payment Type`: `Cash` when `Bank` equals `Cash`; otherwise `Bank`.
4. Sets `Payment Type` as text.

This creates a reusable payment-method classification table rather than repeating the logic in visuals.

## Project-units lookup

Another query starts from the shared preprocessing, then:

1. Keeps only `Project Name` and removes duplicate values.
2. Left-joins the distinct project list to `MorshedyAdvertisedUnitsTable` on `Project Name`.
3. Expands `Adopted Total Units` from the joined table.
4. Renames the expanded field to `Units`.

This produces a project-level lookup for advertised total units.

## Query variations supplied

The pasted code also contains a shared preprocessing variant that ends after installment cleanup and numeric conversion. It follows the same source combination, blank-row removal, type assignment, four initial bank normalizations, field renaming, progress-column removal, installment-status creation, paid/not-due replacements, whitespace trimming, and numeric conversion. It does not include the later bank renaming, payment-type classification, or advertised-units merge.

## Maintenance notes

- Keep all eight project queries structurally aligned before they are combined.
- Add an eighth installment transformation only if the source model adds an eighth installment field; update its status rule, text cleanup, and type conversion together.
- When a new bank spelling appears, add it to the existing standardization sequence and document the mapping above.
- `MorshedyAdvertisedUnitsTable` must retain a compatible `Project Name` key and `Adopted Total Units` field for the project-units lookup to expand correctly.
- The raw source workbooks are local-only and remain excluded from Git; see [DATA_SOURCES.md](DATA_SOURCES.md).
