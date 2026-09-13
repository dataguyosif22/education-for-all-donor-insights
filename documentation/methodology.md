# Methodology

## 1. Business question

How can Education for All increase the number of donors, the frequency of donations, and the total donation amount, using the donor and donation data already available to the organization?

## 2. Data source

Two datasets were provided by the 10Alytics team as part of an internship project:

- `Donation_Data` — donation records, including donor ID, donation amount, gender, and state.
- `Donor_Data` — donor biodata, including donor ID, job field, donation frequency, car, and second-language ability.

Both datasets share a common `ID` field, used to join them. The provenance of the underlying data (real vs. synthetic/sample) is not documented in the original report; it is treated here as internship/training data rather than a verified live charity dataset.

## 3. Data preparation

Data was imported into a SQL environment (sqliteonline.com, using a Postgres IDE). No cleaning or transformation steps beyond the SQL queries themselves are documented in the original report.

## 4. Data modelling

The two tables were joined on `"Donation_Data".id = "Donor_Data".id` (or `.ID = .ID`, per the original queries) wherever a query needed both donation values and donor attributes, for example when relating donation totals to job field, car, or donation frequency.

## 5. KPI definitions

- **Total donation amount**: `SUM(donation)` across all rows in `Donation_Data`.
- **Donation count**: `COUNT(donation)` — number of donation records, used as a proxy for donor count within a segment.
- **Segment totals** (by gender, state, job field, car, frequency): `SUM(donation)` grouped by the relevant column, generally combined with `COUNT(donation)`.
- **High/low-value donor split**: donors grouped by whether `donation > 200`, `donation < 200`, or `donation = 200`.
- **Second-language signal**: `COUNT("Donor_Data".second_language)` grouped by `donation_frequency`, joined to `SUM("Donation_Data".donation)` for the same group.

## 6. Analysis

Queries were run individually for each segment (gender, state, job field, donation frequency, donation-size threshold, car brand, second-language ability), then compared across segments to identify which contributed the most or least to total donations. The second-language / donation-frequency cross-tabulation was the key analytical step behind the report's central finding.

Example query (total donation and count by gender):

```sql
SELECT gender, SUM(donation), COUNT(donation)
FROM "Donation_Data"
GROUP BY gender;
```

The full set of queries used is documented in `Education_For_All_Donor_Insights_Report.docx` and `Education_For_All_Original_Report.md`.

## 7. Dashboard design

No interactive dashboard (e.g. Power BI) was built for this project. Results were presented as SQL query output tables within a written report.

## 8. Validation

No independent validation of the underlying data or query results is documented in the original report. Totals were cross-checked internally (e.g. male + female donation sums equal the reported total of $249,085).

## 9. Limitations

- Data provenance (real vs. sample/synthetic) is not documented.
- No raw dataset files are available in this repository, only query logic and reported result values.
- No automated testing or validation of the SQL queries beyond what is shown in the original report.
- Analysis is a single snapshot, not a refreshed or monitored pipeline.
