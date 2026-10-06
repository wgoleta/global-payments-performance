# Global Payments Performance

**An interactive Power BI portfolio project exploring processor performance, payment fees, savings opportunities, and network incentives.**

`Power BI` · `Power Query` · `DAX` · `Data Modeling` · `Power Apps` · `Dataverse` · `Power Automate` · `Desktop + Mobile`

## Open the report

Download the [Power BI report](Global_Payments_Performance_Portfolio_v3.pbix) and open it in Power BI Desktop. The included data is synthetic and illustrative.

> **Portfolio note:** This project uses synthetic, anonymized data. The figures in the report are illustrative and are not client results.

The Processor Reviews page includes a Power Apps visual. Its form and email automation use a separate Dataverse environment and may require access to that environment to work in a downloaded copy of the report.

## Report pages

### Executive Overview
![Executive Overview](Global%20Payments%20Executive%20Overview%20v2.png)

### Processor Performance
![Processor Performance](Global%20Payments%20Processor%20Performance%20v2.png)

### Fee Optimization
![Fee Optimization](Global%20Payments%20Fee%20Optimization%20v2.png)

### Network Incentives
![Network Incentives](Global%20Payments%20Network%20Incentives%20v2.png)

### Processor Reviews
![Processor Reviews report page](Global%20Payments%20Processor%20Reviews%20v2.png)

## The question

Payments teams need to understand more than transaction volume. Are approval rates changing? Which processors or markets warrant a closer look? Where do billed fees differ from expectations, and how much of an identified savings opportunity has been realized? I built this report to bring those questions into one navigable view.

## Explore the report

| Page | What it helps a reader investigate |
| --- | --- |
| **Executive Overview** | Key payment measures and trends, with an interactive metric selector. |
| **Processor Performance** | Volume, approval rates, fees, and invoice variance by processor; a custom tooltip and drillthrough provide more detail. |
| **Fee Optimization** | Expected versus realized savings, initiative status, and fee variance. |
| **Network Incentives** | Qualifying volume versus targets, earned incentives, and qualification status. |
| **Processor Reviews** | Select a processor and submit a variance review through an embedded Power App. |

## How I built it

- Prepared the data with Power Query, including cleaning, merges, appends, and staging queries that do not load into the model.
- Organized transaction, invoice, optimization, and incentive data around shared date, market, processor, and network dimensions.
- Created DAX measures for payment volume, approvals, fees, savings, and incentives, including time-based comparisons.
- Added synced slicers, a dynamic executive trend, a processor tooltip and drillthrough page, and mobile layouts for the four main analytical pages.
- Integrated a Power App to capture processor variance reviews in Dataverse. A Power Automate flow marks newly added reviews with invoice variance of at least $1,000 as High priority and sends an email alert with the review details.
- Tested slicer interactions, the metric selector, tooltip and drillthrough behavior, data refresh, review submission, priority updates, and email delivery.
- Built RLS with a static Asia Pacific role and a dynamic user-to-region role using `USERPRINCIPALNAME()`; tested both in Power BI Desktop, including an unmapped user. These have not been tested with a real Viewer account in Power BI Service and are part of the published v3 report.

### Power Apps and automation

On the Processor Reviews page, a user selects a processor and submits a review through the embedded Power App. The review is saved in Dataverse. When a newly added review has an invoice variance of at least $1K, Power Automate sets its priority to High and sends an email alert. I tested this with a synthetic $1.5K review and confirmed both the High priority value and the delivered email.

The Power App, Dataverse table, and flow are connected services; their configuration is not packaged inside the `.pbix` file.

### Power Apps Processor Variance Reviews

![Power Apps Processor Variance Reviews](Power%20Apps%20Processor%20Variance%20Reviews.png)

### Power Automate Flag High Variance Reviews

![Power Automate Flag High Variance Reviews](Power%20Automate%20Flag%20High%20Variance%20Reviews.png)

### High variance email alert

![High variance email alert](Power%20Automate%20High%20Variance%20Invoice%20Alerts.png)


## Design decisions

After initial feedback on the layout, I reviewed the remaining pages and applied improvements across the visuals myself. I adjusted font sizes, text wrapping, and chart dimensions to make labels more readable on desktop and mobile. I kept detailed tables on the desktop pages and prioritized KPIs and charts in the mobile layouts.

## What I learned

The most useful measures depend on the question being asked and the filters applied. Building this report gave me practice carrying an operations question from data preparation through modeling, DAX, visual design, and validation. It also taught me to test a report as a reader would: change filters, follow a drillthrough, check narrow screens, and confirm that the refreshed report still behaves as intended.

Extending the report with Power Apps and Power Automate showed me how an analytical finding can become a review workflow: capture a record, flag it against a threshold, and notify someone to investigate.

## Key findings from the illustrative data

- **Processor fees:** Processor Beta has the highest invoice variance rate at approximately 0.38%, representing about $5.04K in invoice variance. This makes it the first processor to investigate for billing differences.
- **Savings realization:** Authorization Improvement has the largest gap between expected and realized annual savings: approximately $105K expected versus $24K realized, a gap of about $81K.
- **Network incentives:** At Risk is the largest qualification group, with 159 of 384 records (41.41%). These records warrant investigation to understand which qualification requirements are unmet and whether any can be addressed.

### Power BI Service dashboard

I published the report to Power BI Service and created an executive dashboard with four KPI tiles and a processed-volume trend. Selecting a tile opens the detailed report.

![Global Payments Executive Summary dashboard](power-bi-service-dashboard.png)
