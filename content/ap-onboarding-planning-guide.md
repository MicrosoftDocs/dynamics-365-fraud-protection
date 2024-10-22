---
author: cschlegel2
description: This article describes onboarding planning for Microsoft Dynamics 365 Fraud Protection account protection.
ms.author: cschlegel
ms.date: 04/10/2024
ms.topic: reference
search.audienceType:
  - Admin
  - IT Pro
title: Onboarding planning guide for account protection
ms.custom:

---

# Onboarding planning guide for account protection

This article describes onboarding planning for Microsoft Dynamics 365 Fraud Protection account protection. Onboard planning will help you understand and plan for the project onboarding milestones of Fraud Protection account protection integration and onboarding.

For more information about the integration steps that follow, see [Set up account protection](promocode-set-up-account-protection.md).

## Onboarding milestones

The tables in this section provide details about the onboarding milestones for the environment setup and application programming interface (API) integration, data validation, data accumulation, and protection phases.

> [!NOTE]
> All timeframes that are mentioned in this article are estimates. The actual time that is required can vary, based on client, Microsoft, and authorized partner availability, and also on focus.

### Environment setup and API integration phase

The following table lists the environment setup tasks, owner teams, and estimated times for implementation of the environment setup and API integration phase.

| Task | Owner team | Estimated time |
|------|------------| ---------------|
| Environment setup | Client and Microsoft/authorized partner | One day |
| Device fingerprinting integration (web and/or mobile) | Client and Microsoft/authorized partner | One week |
| Device fingerprinting data validation (web and/or mobile) | Microsoft/authorized partner | One week |
| API integration and validation | Client and Microsoft/authorized partner | Two weeks (This task can be done in parallel with the preceding tasks.) |
| Account creation and/or account sign-in API integration | Client and Microsoft/authorized partner | Two weeks (This task can be done in parallel with the preceding tasks.) |
| Account creation status and/or account sign-in status integration | Client and Microsoft/authorized partner | Two weeks (This task can be done in parallel with the preceding tasks.) |
| Label API integration | Client and Microsoft/authorized partner | Two weeks (This task can be done in parallel with the preceding tasks.) |

### Data validation phase

The following table lists the environment setup tasks, owner teams, and estimated times for implementation of the data validation phase.

| Task | Owner team | Estimated time |
|------|------------| ---------------|
| Data quality validation and bug fixes | Client and Microsoft/authorized partner | Three to four days |
| Start of production traffic | Client | One day |

> [!NOTE]
> Microsoft does the data validation, but the client must first enable the API calls and start to send a small percentage of production traffic. After validation is completed, the client can send all traffic that will help the project move to the next step.

### Data accumulation phase

No actions are required for the Microsoft/authorized partner during the data accumulation phase. Accumulation begins immediately after data quality is signed off on during the API integration phase. You exit this phase after the criterion of at least 1,000 transactions is reached.

### Protection phase

The following table lists the environment setup tasks, owner teams, and estimated times for implementation of the protection phase.

| Task | Owner team | Estimated time |
|------|------------| ---------------|
| Model score calibration | Microsoft | One  week |
| Rule suggestion (if needed) | Microsoft | One week |
| Go-live | Microsoft | One day |

#### Advanced protection and fraud ops task

The following table lists the environment setup tasks, owner team, and estimated time for implementation for the advanced protection and fraud ops phase.

| Task | Owner team | Estimated time |
|------|------------| ---------------|
| Score analysis and rule adjustment to optimize key performance indicators (KPIs) | Client | Ongoing |

## Resources 

The following resources provide more information about the integration steps that are referenced in this article:

- [Dynamics 365 Fraud Protection overview](/dynamics365/fraud-protection/)
- [Create and provision your Azure tenant](promocode-set-up-dfp-purchased-version.md)
- [Set up a trial instance of Dynamics 365 Fraud Protection](promocode-set-up-dfp-trial-version.md)
- [Set up a purchased instance](promocode-set-up-dfp-purchased-version.md)
- [Configure user access and assign roles](configure-user-access.md)
- [Set up account protection](promocode-set-up-account-protection.md)
- [Configure Dynamics Fraud Protection with Microsoft Entra ID B2C](/azure/active-directory-b2c/partner-dynamics-365-fraud-protection)
- [Set up device fingerprinting](device-fingerprinting.md)
- [Integrate account protection APIs](integrate-ap-api.md)
- [Integrate purchase APIs schema documentation](https://dfpswagger.azurewebsites.net/index.html)
- [Integration training modules](/training/paths/deploy-work-account-purchase-protection/)
- [Account protection manage lists and rules](rules.md)
- [Account protection schemas](ap-schema.md)
- [Account protection threat vulnerability analyzer tool](threat-vulnerability-analyzer.md)
