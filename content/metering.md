---
author: yvonnedeq
description: This topic explains how to meter your usage of Microsoft Dynamics 365 Fraud Protection.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 07/07/2020


ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Usage metering
---

# Usage metering

When you purchase Microsoft Dynamics 365 Fraud Protection, you're entitled to a specific number of "assessments" for one or more Fraud Protection capabilities. The **Metering** page provides an overview of your Fraud Protection usage. For example, you can view statistics about different assessment API types, view trends of assessments that have been consumed for loss prevention reports over time, and filter your view to highlight the specific data and date ranges that you're interested in. The data on this page is updated every hour. You can use it to assess whether any adjustments are required to your Fraud Protection subscription. 

On the **Metering** page, the information is divided between two tabs:

- **Summary** – This tab shows a monthly comparison of the number of assessments that you've purchased and the number of assessments that you've used across different Fraud Protection capabilities (for example, loss prevention, purchase protection, and account protection). On this tab, you can view data across different subscription periods.
- **Details** – This tab lets you dive deeper into your assessment usage data. You can select any date range and filter the data by different dimensions.

## Assessments purchased metric

The **Assessments purchased** metric reflects the total number of assessments that is available to you for each capability, based on the Fraud Protection stock keeping units (SKUs) that you purchased. For more information about Fraud Protection SKUs and the number of assessments that they provide access to, see [Dynamics 365 Fraud Protection](https://dynamics.microsoft.com/ai/fraud-protection/).

## Assessments used metric

The **Assessments used** metric reflects your usage of Fraud Protection. The following table shows which activities count toward the assessment that is used for each Fraud Protection capability.

| Fraud Protection capability | What is included in the Assessments used metric? |
|-----------------------------|--------------------------------------------------|
| Account protection | Real-time API calls where a risk assessment or decision is requested (that is, API calls for the AccountCreation, AccountLogin, and CustomAssessments APIs). |
| Loss prevention | The number of transactions that have been processed to generate loss prevention reports.\* |
| Purchase protection | Real-time API calls where a risk assessment is requested (that is, API calls for the Purchase, SignIn, SignUp, and CustomFraudEvaluation APIs). |

\* The number of assessments that you should purchase for the loss prevention capability is determined by the estimated number of in-store transactions that must be protected during the billing cycle. If the data is sampled before it's sent to Fraud Protection for assessment, variance can occur between the **Assessments used** metric and the **Assessments purchased** metric. This result is expected, because the **Assessments used** metric counts the number of transactions from the assessed data only, and the magnitude of the variance depends on the sampling rate. For accurate reporting of the assessments that have been used, and to generate higher-quality loss prevention reports, we recommend that you use a sampling rate of 100 percent. In other words, we recommend that you share all transactions that should be protected.

### Accumulated consumption % metric

The **Accumulated Consumption %** metric shows the ratio of the total number of assessments that have been used to the total number of assessments that have been purchased since the start of a billing cycle, and resets to 0% at the beginning of a new billing cycle. 

> [!NOTE]
> Billing arrangements are made via your Microsoft Account Executive or Microsoft Cloud Solution Provider partner. You will receive notifications from them if your accumulated consumption approaches 100 percent before the end of the current billing cycle. Therefore, you will have an opportunity to adjust your subscription as required.

## Additional notes about assessment usage and metering

- Only activity in the Fraud Protection production environment counts toward the assessments that have been used. Activity in the integration environment doesn't count. Therefore, in the integration environment, the **Metering** page doesn't show the **Summary** tab.
- The calculation of assessments that have been used excludes any assessment API calls that fail because of service issues that are caused by Fraud Protection (HTTP response code 5xx). The calculation includes only successful requests (HTTP response code 2xx) and bad requests (HTTP response code 4xx).
- The **Experience Type** and **Response Type** filters on the **Details** tab of the **Metering** page apply only to the account protection and purchase protection capabilities.
