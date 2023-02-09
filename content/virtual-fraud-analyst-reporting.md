---
author: yvonnedeq
description: This article explains how the Virtual fraud analyst (VFA) in Microsoft Dynamics 365 Fraud Protection helps you set up and adjust risk score thresholds.
ms.author: kfend
ms.date: 02/08/2023
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Virtual fraud analyst reporting
ms.custom: bap-template
---

# Virtual fraud analyst reporting

Virtual fraud analyst reports are being redesigned to incorporate the great feedback that we received from our customers. In the meantime, the reports provide a unified experience across different capabilities that Microsoft Dynamics 365 Fraud Protection offers.

Dynamics 365 Fraud Protection includes a suite of fraud analysis tools that's named Virtual fraud analyst (VFA). VFA provides a historical view of your data, and is designed to enable fraud analysts and fraud managers to conduct fraud analysis, define fraud control strategies, and optimize your business.

VFA reports are updated every 24 hours by using the last four months of data. The time stamp on the report shows the time when the report was last updated, in Coordinated Universal Time.

For applicable capabilities, such as purchases, you can switch between the Count view and the Amount view on the report. The Count view aggregates metrics by transaction count. The Amount view aggregates metrics in US dollars. Reports can be viewed in different timescales, including a daily view, a weekly view, and a monthly view.

## VFA tools
The following interactive report tools make up the VFA suite:

  - **Summary report** – This tool is designed to show metrics for key performance indicators (KPIs) that are related to fraud. Use this tool to learn the statistics of rule decision distributions, fraud rates, and available bank acceptance rates over time for various reporting purposes.
  - **Rule analyst** – This tool is designed to do a deep dive into the performance of decision rules and observe rules. Use this tool to optimize your rules based on performance.
  - **Score analyst** – This tool is designed to analyze Fraud Protection's machine learning (ML) scores. Use this tool to determine the score threshold. The configuration experience tests the risk score threshold, reject rate, fraud rate, and profit margin against historical transactions to estimate the risk impact on the detection rate, the net profit that's achieved, and other values.
  - **Threat analyst** – This tool is designed to show fraud insights on predefined entities, such as payment card type. Use this tool to find distribution changes and identify anomalies on the entities. You can also use this tool to define score segments and further optimize your score rules.

## Common filters
Because Fraud Protection offers multiple capabilities, common filters vary, depending on the capability. You can use the drop-down menus and sliders on the report to filter your view of the interactive charts. Here are some of the common filters:

- **Date range** – Show transaction data by date. You can select dates in the calendar, manually enter dates, or select date ranges.
- **Score range** – Use the text box or the scroll bar to select the desired score range. The score is aggregated in increments of 10. For the digit in the ones place, the lower bound is rounded down to 0 (zero), and the upper bound is rounded up to 9. For example, if you select a score from 35 through 64, the metrics and charts on the report show data that has a score range from 30 through 69.
- **Purchase protection**

    - **Merchant Business Segment** – Filter by business segment.
    - **Merchant Product Category** – Filter by the category of product.
    - **PI Type** – Filter by payment instrument type, such as CREDITCARD or PAYPAL.	
    - **PI Card Type** – Filter by the network that the credit or debit card is issued from.
    - **IP Country/Region** – Filter by country or region, based on IP address.

- **Account protection**

    - **Enabled JS** – Filter based on whether JavaScript is enabled.
    - **Operating System Family** – Filter by operating system (OS) family.
    - **Operating System** – Filter by OS that contains version information.
    - **Browser Family** – Filter by browser family, such as Edge, Chrome, or Safari.
    - **IP Country/Region and State** – Filter by country/region and state/province, based on IP address.

## See also
- [Summary report](summary-report.md)
- [Score analyst](score-analyst.md)
- [Rule analyst](rule-analyst.md)
- [Threat analyst](threat-analyst.md)
