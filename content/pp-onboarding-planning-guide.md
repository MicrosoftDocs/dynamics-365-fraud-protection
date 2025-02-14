---
author: cschlegel2
description: This article describes onboarding planning for Microsoft Dynamics 365 Fraud Protection purchase protection.
ms.author: cschlegel
ms.date: 04/10/2024
ms.topic: reference
search.audienceType:
  - Admin
  - IT Pro
title: Onboarding planning for purchase protection
---

# Onboarding planning for purchase protection

[!include[deprecation](includes/deprecation.md)]

This article describes onboarding planning for Microsoft Dynamics 365 Fraud Protection purchase protection. Onboard planning will help you understand and plan for the project implementation milestones of Fraud Protection purchase protection integration and onboarding. For more information about the integration steps, see [Set up purchase protection](promocode-set-up-purchase-protection.md).

## Onboarding milestones

The tables in this section provide details about the onboarding milestones for the environment setup and application programming interface (API) integration, protection, data accumulation, and advanced modeling phases.

> [!NOTE]
> - All timeframes that are  mentioned in this article are estimates. The actual time that is required can vary, based on merchant and Microsoft/authorized partner availability and focus.
> - Microsoft does the data validation, but clients must first enable the API calls and start to send a small percentage of production traffic. After validation is completed, clients can send all traffic to help the project move to the next step.

### Environment setup and API integration phase

The following table lists the environment setup tasks, owner teams, and estimated times for implementation of the environment setup and API integration phase.

| Task | Owner team | Estimated time |
|------|------------| ---------------|
| Environment provisioning and setup | Client and Microsoft/authorized partner | One day |
| Device fingerprinting integration (web and/or mobile) | Client and Microsoft/authorized partner | One week |
| Device fingerprinting data validation (web and/or mobile) | Microsoft/authorized partner | One week |
| Purchase API integration and validation | Client and Microsoft/authorized partner | Two weeks (This task can be done in parallel with the preceding tasks.) |
| Bank event APT integration and validation | Client and Microsoft/authorized partner | Two weeks (This task can be done in parallel with the preceding tasks.) |
| Purchase status API integration and validation | Client and Microsoft/authorized partner | Two weeks (This task can be done in parallel with the preceding tasks.) |
| Label and chargeback API integration and validation | Client and Microsoft/authorized partner | Two weeks (This task can be done in parallel with the preceding tasks.) |

### Protection phase

The following table lists the environment setup tasks, owner teams, and estimated times for implementation of the protection phase.

| Task | Owner team | Estimated time |
|------|------------| ---------------|
| Historical data upload (optional) | Client | One day |
| Partner training | Client and Microsoft/authorized partner | One day |
| Transaction acceptance booster (TAB) opt-in | Microsoft/authorized partner | One day |
| Rule creation and migration | Client | Two days |

### Data accumulation phase

No actions are required for the client and Microsoft/authorized partner during this phase. Accumulation begins immediately after data quality is signed off on during the API integration phase. Move on to the next phase after the following criteria have been met:

- At least 500 fraudulent transactions
- At least 5,000 non-fraudulent transactions
- At least four weeks of data that has a label maturity rate above 70 percent

### Advanced modeling phase

The following table lists the environment setup tasks, owner teams, and estimated times for implementation of the advanced modeling phase.

| Task | Owner team | Estimated time |
|------|------------| ---------------|
| Model training | Client | Two weeks |
| Model shadow on production | Client and Microsoft/authorized partner | One week |
| Model switch | Microsoft/authorized partner | Upon notification |

#### Advanced protection and fraud ops tuning

The following table lists the task, owner team, and estimated time for advanced protection and fraud ops analysis and adjustments.

| Task | Owner team | Estimated time |
|------|------------| ---------------|
| Score analysis and rule adjustment to optimize key performance indicators (KPIs) | Client | Ongoing |

## Resources

The following resources provide more information for the integration steps that are referenced in this topic:

- [Fraud Protection overview](/dynamics365/fraud-protection/)
- [Create and provision your Azure tenant](promocode-set-up-dfp-purchased-version.md)
- [Set up a purchased instance of Fraud Protection](promocode-set-up-dfp-purchased-version.md)
- [Configure user access](configure-user-access.md)
- [Set up purchased protection](promocode-set-up-purchase-protection.md)
- [Set up device fingerprinting](device-fingerprinting.md)
- [Integrate purchase protection APIs](integrate-real-time-api.md)
- [Integrate purchase APIs schema](https://dfpswagger.azurewebsites.net/index.html)
- [Integration training modules](/training/paths/deploy-work-account-purchase-protection/)
