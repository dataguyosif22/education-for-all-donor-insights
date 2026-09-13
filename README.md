# Education for All: Donor & Donation Analysis

A SQL-driven analysis identifying which donor segments give the most, and why a language and education gap may be suppressing donations for the Education for All charity.

[View original report (Word)](https://github.com/dataguyosif22/education-for-all-donor-insights/blob/main/Education_For_All_Donor_Insights_Report.docx) | [View original report (Markdown)](https://github.com/dataguyosif22/education-for-all-donor-insights/blob/main/Education_For_All_Original_Report.md) | [View portfolio](https://yusuf-data-analytics-portfolio.netlify.app/)

## Project overview

Education for All, a charity organization, provided two datasets, `Donation_Data` and `Donor_Data`, as part of a 10Alytics internship project. The task was to analyze donor and donation records to find practical ways to increase the number of donors, the frequency of donations, and the total amount donated.

The analysis was run in SQL (Postgres, via sqliteonline.com) against the two joined tables, segmenting donations by gender, state, job field, donation frequency, donation size, vehicle brand (used as a lifestyle proxy), and second-language ability.

This project is useful to anyone evaluating whether I can take two related but unlinked datasets, join them meaningfully, define relevant KPIs, and turn query output into a specific, actionable recommendation rather than just a chart.

## Business questions

- Which donor segments (state, job field, donation frequency, lifestyle indicators) contribute the most and least to total donations?
- Does gender affect donation behavior?
- Does a donor's education level or ability to speak a second language relate to how often or how much they give?
- Where should the charity focus outreach to grow total donations?

## Key KPIs

| KPI | What it measures | Why it matters |
|---|---|---|
| Total donation amount | Sum of all donations across the dataset | Baseline figure for measuring the impact of any intervention |
| Donation sum & count by gender | Total given and number of donors, split by gender | Tests whether gender is a meaningful targeting variable |
| Donation sum by state (top/bottom 10) | Geographic concentration of giving | Identifies where outreach is already working vs. underserved regions |
| Donation sum & count by donation frequency | Giving broken into Once, Daily, Weekly, Monthly, Yearly, Seldom, Often, Never | Distinguishes loyal recurring donors from one-off or lapsed donors |
| Donation sum & count by job field | Giving across 12 professional sectors | Flags which professional communities are most and least engaged |
| Donor count above/below/at the $200 threshold | Splits donors into higher- and lower-value givers | Shows how concentrated total donations are among a subset of donors |
| Donation sum by donor vehicle brand | Giving cross-referenced against car ownership | Used in the original analysis as an indirect wealth/lifestyle signal |
| Second-language speaker count by donation frequency | Number of second-language donors within each frequency band | Core signal behind the report's language-barrier hypothesis |

## Key findings

- Total donations reached **$249,085** across 1,000 donors. Giving was almost evenly split by gender (52% from male donors, 48% from female donors), indicating gender is not a useful variable for targeting donors in this dataset.
- Donations were heavily concentrated by state. The top 3 states (California, Texas, Florida) contributed over **$75,000** combined, while the bottom 10 states, led by Wyoming ($258), contributed under **$7,000** combined.
- Donors in Human Resources gave the most among the 12 job fields tracked (**$23,060**), while Legal donors gave the least (**$17,309**), despite Legal having fewer donors (66 vs. 93) rather than a proportionally lower average gift.
- About **59% of donors** (586 of ~1,000) gave more than $200, and this group accounted for the large majority of total donations (**$205,892** of $249,085) — donation value is concentrated in a minority of higher-value donors.
- When donation frequency was cross-referenced with the count of second-language donors, the report's central finding emerged: donors who understand a second language and have lower education levels were disproportionately represented among low-frequency and non-responsive donors, suggesting language and correspondence format play a role in disengagement.
- Vehicle brand, used as a lifestyle/wealth proxy, showed Ford, Chevrolet, and Toyota owners as the top three donor segments by total giving.

## Business recommendations

These are the original report's recommendations, derived from the patterns above. They have not been implemented and there is no evidence of real-world business impact from them:

- **Offer translated correspondence.** Since second-language donors appear underrepresented among frequent givers, the analysis suggests offering translation tools or second-language versions of donation emails could improve response rates for that segment.
- **Increase outreach in low-donation states.** The data suggests more email marketing and physical/in-person representation in the lowest-donating states could help close the gap with high-performing states.
- **Build loyalty programs for recurring donors.** The report recommends appreciation gestures (e.g., gift items) for donors who give daily, weekly, monthly, or yearly, to reinforce and retain that recurring-donor base.

## Dashboard preview

This project's evidence is presented as SQL queries and result tables inside the report rather than an interactive dashboard. See `screenshots/README.md` for how to add the original query-result screenshots to this repo.

## Tools and technologies

- SQL (PostgreSQL dialect, run via sqliteonline.com's Postgres IDE)
- Aggregate functions, `JOIN`, `GROUP BY`, `ORDER BY`, `WHERE` filtering

## Data preparation and methodology

See [`documentation/methodology.md`](documentation/methodology.md) for the full breakdown of data source, joins, and query logic.

## Repository structure

```
/
├── README.md
├── Education_For_All_Donor_Insights_Report.docx   # formatted write-up with all SQL queries
├── Education_For_All_Original_Report.md           # markdown transcript of the original report
├── screenshots/
│   └── README.md
└── documentation/
    └── methodology.md
```

## Business value

A fundraising lead or nonprofit operations manager could use this analysis to decide where to focus limited outreach budget: which states are underperforming, which donor segments are most loyal, and whether a translation/localization investment is justified by the size of the affected donor group.

## Limitations

- **Internship/training data.** The datasets were provided by 10Alytics as part of an internship exercise. There is no evidence this reflects a real charity's actual donor base, and it should not be presented as a live client engagement.
- **No access to raw datasets in this repo.** `Donation_Data` and `Donor_Data` themselves are not included here, only the SQL queries and their result values as documented in the original report.
- **No query-result screenshots yet.** The original report included screenshots of query outputs; those images are not yet in this repository (see `screenshots/README.md`).
- **Single point-in-time snapshot.** The analysis reflects one export of the data, not an ongoing or refreshed reporting process.
