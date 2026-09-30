# Operational Risk Analytics Dashboard

A Power BI portfolio project for analyzing operational-risk events, loss concentration, process exposure, severity, frequency, and contextual risk indicators.

## Project Objective

The goal of this project is to transform an operational-risk event dataset into a management-style dashboard that answers practical questions such as:

- How many operational-risk events are present?
- What is the total and average loss exposure?
- Which event types contribute the most loss?
- Which process areas experience the highest event concentration?
- How do severity and frequency differ across event types and process areas?
- What additional contextual indicators are present in the dataset?

The dashboard is designed as a portfolio project for risk-controlling, data-analytics, and business-intelligence roles.

## Dataset

The dataset contains 2,147 operational-risk observations.

Main fields include:

- Scenario ID
- Date
- Event Type
- Process Area
- Loss Amount (kUSD)
- Frequency (Nk)
- Severity (Xi)
- OpVar (%)
- ML
- GDP (%)
- VIX
- Target

### Important Data Note

The original `Date` column contains both normal calendar dates and the literal value `Synth-2022`.

To handle this cleanly in Power BI, two additional fields were created:

- `Record Type` — identifies rows as `Synthetic` or `Dated Event`
- `Event Date` — converts valid dates into a true Power BI date field while leaving synthetic-labelled rows blank

The dataset includes synthetic-labelled observations, so this project should be treated as an educational and analytical portfolio project rather than a production banking system.

## Data Preparation

Power Query was used to create the following fields.

### Record Type

```powerquery
if [Date] = "Synth-2022" then "Synthetic" else "Dated Event"
```

### Event Date

```powerquery
try Date.FromText([Date]) otherwise null
```

This approach preserves the original data while creating analysis-ready fields.

## Dashboard Structure

### Page 1 — Operational Risk Overview

The overview page provides a high-level picture of the operational-risk portfolio.

Main KPIs:

- Total Events
- Total Loss
- Average Loss
- Average Severity
- Average Frequency

Main visuals:

- Total Loss by Event Type
- Event Count by Process Area
- Event Type × Process Area matrix
- Event Type slicer
- Process Area slicer

This page is designed to answer where losses and events are concentrated.

### Page 2 — Risk Drivers & Analysis

The second page focuses on deeper comparisons across the dataset.

Main visuals:

- Total Loss by Process Area
- Average Loss by Event Type
- Average Severity by Process Area
- Average Frequency by Event Type

Context indicators:

- Average VIX
- Average GDP (%)
- Average OpVar (%)

These contextual variables are used descriptively and should not be interpreted as proving causal relationships with operational losses.

## Example DAX Measures

```DAX
Total Events =
COUNTROWS('Operational_Risk_Events')
```

```DAX
Total Loss (kUSD) =
SUM('Operational_Risk_Events'[Loss Amount (kUSD)])
```

```DAX
Average Loss (kUSD) =
AVERAGE('Operational_Risk_Events'[Loss Amount (kUSD)])
```

```DAX
Average Severity =
AVERAGE('Operational_Risk_Events'[Severity (Xi)])
```

```DAX
Average Frequency =
AVERAGE('Operational_Risk_Events'[Frequency (Nk)])
```

## Design Decisions

Several decisions were made deliberately:

- Event Type and Process Area were used as the main analytical dimensions because they make operational-risk concentration easy to understand.
- The dashboard separates high-level monitoring from deeper analysis across two pages.
- The unexplained `Target` field was not used in the final dashboard because the meaning of values `0`, `1`, and `2` was not verified.
- Synthetic-labelled rows were not assigned artificial dates.
- The final report uses a 16:9 layout with aligned KPI cards and grouped slicers to keep the dashboard easy to scan.

## Key Lessons

This project helped demonstrate:

- Power Query data cleaning
- Handling mixed date/text fields
- Power BI data modelling
- DAX measures
- KPI design
- Bar, column, matrix, and slicer visuals
- Risk-event concentration analysis
- Dashboard layout and visual hierarchy
- Data-quality awareness
- Avoiding unsupported interpretations of undocumented fields

## Tools Used

- Microsoft Power BI Desktop
- Power Query
- DAX

## Portfolio Positioning

This project is suitable for demonstrating skills relevant to:

- Risk Controlling
- Operational Risk Analytics
- Business Intelligence
- Data Analytics
- Financial Risk Reporting
- Management Reporting

## Limitations

- The dataset contains synthetic-labelled observations.
- Some source variables are not fully documented.
- The dashboard is exploratory and educational.
- VIX, GDP, and OpVar are treated as contextual indicators only.
- No causal inference or regulatory-model validation is claimed.

## Future Improvements

Possible next steps include:

- Add a proper calendar/date dimension
- Create dedicated DAX measures for all KPIs
- Add high-severity thresholds with clearly documented assumptions
- Add drill-through event-detail pages
- Add tooltips and richer conditional formatting
- Add data-quality KPIs
- Compare synthetic and dated observations explicitly
- Add trend analysis only after date handling is fully validated

## Author

Pratik Prakash Gawde  
MSc Data Analytics, Berlin
