---
author: jegrif
description: This topic explains how to meter your usage of Microsoft Dynamics 365 Fraud Protection.
ms.author: v-jegrif
ms.service: fraud-protection
ms.date: 09/16/2019


ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Usage metering
---

# Usage metering

Metering provides an overview of your Microsoft Dynamics 365 Fraud Protection usage. You can view statistics about different API types over time and filter your view to highlight specific data and date ranges as needed. When your billing for Dynamics 365 Fraud Protection begins, you can use this information to assess any impact to your costs. Data on the Metering page is refreshed hourly.

The Metering page breaks out information into four tabs:

- **Consumption %** tracks how many assessments you have purchased that have been used within each billing period. 
- **Assessment APIs** charts the activity of the APIs that return a risk score assessment. These include the APIs for Purchase, SignUp, and CustomFraudEvaluation, which are the real-time APIs that are considered billable in your production environment. Note that successful assessments and bad requests are billed, but any assessments that fail due to service issues on Dynamics 365 Fraud Protection’s part will not be charged to you.
- **Data update APIs** include the APIs that update information but do not return a risk assessment. 
- **Other events** contains additional APIs that help power tools like the graph explorer, risk support, and device fingerprinting.

Each tab shows usage charts and statistics for the APIs represented in that category. You can select specific date ranges, types of APIs, and the specific Dynamics 365 Fraud Protection experience you’re using to filter these charts.

## Consumption
The number of assessments available to you in a month are agreed upon in a subscription model. In the **Consumption %** tab, you can track how many of your purchased assessments have been consumed over time. The **Consumption%** line displays your consumption percentage within a single monthly billing period, while **AccumulatedConsumption%** shows your consumption percentages since the start of billing. 

Billing arrangements are made via your enterprise account (EA) account managers or cloud solution provider (CSP) partners. If your monthly usage reaches or passes the number of assessments you’ve paid for, you will receive notifications from them. This will give you the opportunity to work out any adjustments needed.

## Assessment, Data update, and Other events 
For **Assessment APIs**, **Data update APIs**, and **Other events**, specific statistics appear under **Total API responses**. These include both successful and unsuccessful API responses. The charts illustrate the numbers of successful and unsuccessful calls to the specified API during your selected time period. To view one set or the other individually, select **Success** or **Bad request**. To drill in and view specific data with more granularity, use the controls in the upper right of each chart. [Learn more about PowerBI controls](https://docs.microsoft.com/power-bi/consumer/end-user-drill)
