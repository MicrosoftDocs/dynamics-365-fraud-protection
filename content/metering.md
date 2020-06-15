---
author: yvonnedeq
description: This topic explains how to meter your usage of Microsoft Dynamics 365 Fraud Protection.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 06/15/2020


ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Usage metering
---

# Usage metering

When you purchase Microsoft Dynamics 365 Fraud Protection, you are entitled to a certain number of “assessments” for one or more Fraud Protection capabilities. The **Metering** page provides an overview of your Fraud Protection usage. For example, you can view statistics about different assessment API types, trends of assessments consumed for loss prevention reports over time, and filter your view to highlight the specific data and date ranges you need.  Data on this page is refreshed hourly. This information is useful to assess if any adjustments are required to your Fraud Protection subscription.

The **Metering** page breaks out information into two tabs:

- The **Summary** tab shows a monthly comparison of the number of assessments you've purchased and the number of assessments you've used across different Fraud Protection capabilities. This includes loss prevention, purchase protection, account protection, and so on. You can view data across different subscription periods on this tab.
- The **Details** tab allows you to dive deeper into your assessment usage data. This gives you the flexibility to choose any date range, and the ability to filter the data by different dimensions.

## Assessments purchased

The *assessments purchased* metric reflects the total assessments available to you for each capability based on the Fraud Protection SKUs you've purchased. For more information about Dynamics 365 Fraud Protection SKUs and the number of assessments they provide access to, see [Dynamics 365 Fraud Protection](https://dynamics.microsoft.com/ai/fraud-protection/).

## Assessments used

The *assessments used* metric reflects your usage of Fraud Protection. The table below explains which activities count towards the assessment used for each Fraud Protection capability.

|Fraud Protection capability| Response    |
|---------------------------|-------------|
|Account protection         
|Real-time API calls where a risk assessment or decision is requested, namely: AccountCreation, AccountLogin, and CustomAssessments APIs.       |
|Loss prevention            |The number of transactions processed for generating Loss Prevention reports*             |
|Purchase protection        |Real-time API calls for APIs where a risk assessment is requested, namely: Purchase, SignIn, SignUp, and CustomFraudEvaluation APIs    |         

*The required number of assessments you should purchase for loss prevention capability is determined by the estimated in-store transactions required to be protected during the billing cycle. Sampling the data before sending it to Fraud Protection for assessment may result in variance between the assessments used metric and the asssessments purchased metric. This is expected because the assessments used metric only counts the number of transactions from the assessed data, and the magnitude of variance depends on the sampling rate. 

For accurate reporting of assessments used and to generate higher quality loss prevention reports, we encourage a sampling rate of 100% (i.e., sharing all transactions that should be protected).

> [!NOTE]
> The **Accumulated Consumption %** metric shows a ratio of total assessments used and total assessments purchased since the start of a billing cycle. Billing arrangements are made via your Microsoft Account Executive or Microsoft Cloud Solution Provider partner. You will receive notifications from them if your accumulated consumption approaches 100% before the end of the current billing cycle. This will give you the opportunity to adjust your subscription as necessary.


## Additional notes regarding assessment usage and metering

- Only the activity within the Fraud Protection production environment counts towards the assessments used; activity in the integration environment does not count. This means that in the integration environment, the **Metering** page  does not display the **Summary** tab.
- Any assessment API calls that fail due to service issues caused by Fraud Protection (HTTP response code 5xx) are not included in the calculation of assessments used. Only successful requests (HTTP response code 2xx) and Bad Requests (HTTP response code 4xx) count towards your assessment used calculation.
- The filters named **Experience Type** and **Response Type** on the **Details** tab of the **Metering** page only apply for account protection and purchase protection capabilities.
