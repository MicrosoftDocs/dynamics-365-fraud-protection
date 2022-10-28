---
author: cschlegel2
description: This article describes onboarding planning for Microsoft Dynamics 365 Fraud Protection account protection.
ms.author: cschlegel
ms.date: 10/28/2022
ms.topic: reference
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - Admin
  - IT Pro
title: Onboarding planning guide for purchase protection
ms.custom:

---

# Onboarding planning for account protection

This article describes onboarding planning for Microsoft Dynamics 365 Fraud Protection account protection, and will help you understand and plan for the project onboarding milestones of Fraud Protection account protection integration and onboarding. 

For more information on the integration steps below, see [Set up purchase protection](promocode-set-up-purchase-protection.md).

## Onboarding milestones

The tables below provide details on the onboarding milestones for the environment setup and the API integration, data validation, data accumulation, and protection phases.

> [!NOTE]
> All timeframes mentioned in this article are estimates. The actual time taken can vary based on client, Microsoft and authorized partner availability, and focus. 

### Environment setup and API integration phase

The following table lists the environment setup tasks, owner teams, and the estimated times for implementation for the environment setup and API integration phase.

| Task  | Owner team | Estimated time  |
| ----- |------------| ----------------|
| Environment setup | Client and Microsoft/authorized partner | One (1) day |
| Device fingerprinting integration (web and/or mobile) | Client and Microsoft/authorized partner | One (1) week |
| Device fingerprinting data validation (web and/or mobile) | Microsoft/authorized partner | One (1) week |
| API integration and validation | Client and Microsoft/authorized partner | Two (2) weeks (can be done in parallel with the steps above) |
| Account creation and/or account sign-in API integration | Client and Microsoft/authorized partner | Two (2) weeks (can be done in parallel with the steps above) |
| Account creation status and/or account sign-in status integration | Client and Microsoft/authorized partner | Two (2) weeks (can be done in parallel with the steps above) |
| Label API integration | Client and Microsoft/authorized partner | Two (2) weeks (can be done in parallel with the steps above) |

<!--![step1.](media/ap-onboarding-guide-step1.png)-->
### Data validation phase

The following table lists the environment setup tasks, owner teams, and the estimated times for implementation for the data validation phase.

| Task  | Owner team | Estimated time  |
| ----- |------------| ----------------|
| Data quality validation and bug fixes | Client and Microsoft/authorized partner | Three to four (3-4) days |
| Production traffic starts | Client | One (1) day |

> [!NOTE]
> Microsoft performs the data validation, but first the client must enable the API calls and start sending a small percentage of production traffic. After validation, the client can send all traffic that will help the project move to the next step.

<!--![step2.](media/ap-onboarding-guide-step2.png)-->
### Data accumulation phase

No actions are required for the Microsoft/authorized partner during this phase. Accumulation starts immediately after data quality is signed off during the API integration phase. You exit the phase once the criteria of at least 100 transactions is reached.

### Protection phase

The following table lists the environment setup tasks, owner teams, and the estimated times for implementation for the protection phase.

| Task  | Owner team | Estimated time  |
| ----- |------------| ----------------|
| Model score calibration | Microsoft | One (1) week |
| Rule suggestion (if needed) | Microsoft | One (1) week |
| Go live | Microsoft | One (1) day |

#### Advanced protection and fraud ops task

The following table lists the environment setup tasks, owner team, and the estimated time for implementation for the advanced protection and fraud ops phase.

| Task  | Owner team | Estimated time  |
| ----- |------------| ----------------|
| Score analysis and rule adjustment to optimize KPIs | Client | Ongoing |

<!--![step3.](media/ap-onboarding-guide-step34.png)-->
## Resources 

The following resources provide more details on the integration steps referenced above.

- [Dynamics 365 Fraud Protection overview](/dynamics365/fraud-protection/)
- [Create and provision your Azure tenant](promocode-set-up-dfp-purchased-version.md)
- [Set up a trial instance of Dynamics 365 Fraud Protection](promocode-set-up-dfp-trial-version.md)
- [Set up a purchased instance](promocode-set-up-dfp-purchased-version.md)
- [Configure user access and assign roles](configure-user-access.md)
- [Set up account protection](promocode-set-up-account-protection.md)
- [Configure Dynamics Fraud Protection with Azure Active Directory B2C](/azure/active-directory-b2c/partner-dynamics-365-fraud-protection)
- [Set up device fingerprinting](device-fingerprinting.md)
- [integrate account protection APIs](integrate-ap-api.md)
- [Integrate purchase APIs schema documentation](https://dfpswagger.azurewebsites.net/index.html)
- [Integration training modules](/training/paths/deploy-work-account-purchase-protection/)
- [Account protection manage lists and rules](rules.md)
- [Account protection schemas](ap-schema.md)
- [Account protection threat vulnerability analyzer tool](threat-vulnerability-analyzer.md)
