---
author: josaw1
description: This article provides information about reporting and what reports are available in Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 07/29/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Reporting
ms.custom: bap-template
---

# Reporting

[!include[deprecation](includes/deprecation.md)]

Dynamics 365 Fraud Protection includes a suite of fraud analysis reports. The reports provide a historical view of your data, and are designed to enable fraud analysts and fraud managers to conduct fraud analysis, define fraud control strategies, and optimize your business.

The reports are updated every 24 hours, and use the last four months of data. The time stamp on the report shows the time when the report was last updated in Coordinated Universal Time.

For applicable capabilities such as purchases, you can switch between the **Count** view and the **Amount** view on the report. The **Count** view aggregates metrics by transaction count. The **Amount** view aggregates metrics in US dollars. For [Assessments](assessment-create-new.md), the **Amount** view can be configured through the configuration of [assessment reporting settings](assessment-configure-existing.md). Reports can be viewed in different timescales, including a daily view, a weekly view, and a monthly view. If you use multiple capabilities in Fraud Protection, such as purchase and account login, you can switch the capabilities to load different reports.

## Reports
The following interactive reports make up the reporting suite.

  - **Summary report** – This report is designed to show metrics for key performance indicators (KPIs) that are related to fraud. Use this report to learn the statistics of rule decision distributions, fraud rates, and available bank acceptance rates over time for various reporting purposes.
  - **Rule reports** – These reports provide a deep dive into the performance of decision rules and observe rules. Use these reports to optimize your rules based on performance.
  - **Score reports** – These reports analyze Fraud Protection's machine learning (ML) scores. Use these reports to determine the score threshold. The configuration experience tests the risk score threshold, reject rate, fraud rate, and profit margin against historical transactions to estimate the risk impact on the detection rate, the net profit that's achieved, and other values.
  - **Threat report** – This report provides fraud insights on predefined entities, such as payment card type. Use this report to find distribution changes and identify anomalies on the entities. You can also use this tool to define score segments and further optimize your score rules.
  - **Observation event report** – The observation event report showcases insights from observation events or labeled events for [Assessments](assessment-create-new.md) only.
    
## Common filters
Because Fraud Protection offers multiple capabilities, common filters vary, depending on the capability. You can use the drop-down menus and sliders on the report to filter your view of the interactive charts. Here are some of the common filters.

- **Date range** – Filter transaction data by date. You can select dates in the calendar, manually enter dates, or select date ranges.
- **Score range** – Use the text box or the scroll bar to select the desired score range. The score is aggregated in increments of 10. For the digit in the ones place, the lower bound is rounded down to 0 (zero), and the upper bound is rounded up to 9. For example, if you select a score from 35 through 64, the metrics and charts on the report show data that has a score range from 30 through 69.
- **Purchase protection**

    - **Merchant Business Segment** – Filter by business segment.
    - **Merchant Product Category** – Filter by the category of product. If there are multiple products listed in one transaction, the report metrics select the product category of the first product in the transaction.
    - **PI Type** – Filter by payment instrument type, such as CREDITCARD or PAYPAL. If there are multiple payment instruments listed in one transaction, the report metrics select the first payment instrument type of the transaction.
    - **PI Card Type** – Filter by the network that the credit or debit card is issued from.
    - **IP Country/Region** – Filter by country/region, based on IP address.

- **Account protection**

    - **Operating System Family** – Filter by operating system (OS) family.
    - **Operating System** – Filter by OS that contains version information.
    - **Browser Family** – Filter by browser family, such as Edge, Chrome, or Safari.
    - **IP Country/Region** - Filter by country/region, based on IP address.
    - **IP State** – Filter by state/province, based on IP address.
- **Assessments**

    - After you create an assessment, you can set up your own data filters. For more information, see [Configure an existing assessment](assessment-configure-existing.md).

## See also
- [Summary report](summary-report.md)
- [Score reports](score-analyst.md)
- [Rule reports](rule-analyst.md)
- [Threat report](threat-analyst.md)
- [Observation event report](observation-event-report.md)
