---
author: cschlegel2
description: This article describes onboarding planning for Microsoft Dynamics 365 Fraud Protection purchase protection. 
ms.author: cschlegel
ms.date: 11/02/2022
ms.topic: reference
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - Admin
  - IT Pro
title: Onboarding planning for account purchase protection

---

# Onboarding planning for account purchase protection

This article describes onboarding planning for Microsoft Dynamics 365 Fraud Protection purchase protection.

**Integration Planning Guide** This guide helps you understand and plan for the project milestones of Dynamics 365 Fraud Protection Purchase Protection integration and onboarding. For more information on the integration steps, see [Set up purchase protection](promocode-set-up-purchase-protection.md).

**Onboarding Milestones - Integration Breakdown and Approximate Time** 

> [!NOTE]
> All timeframes below are estimates. Actual time taken can vary based on Merchant, and Microsoft/Authorized Partner availability and focus. 

![step 1](media/pp-onboarding-guide-steponeclean.png)

![step 2](media/step2-PP-onboardingguide.png)

> [!NOTE]
> Microsoft would perform data validation, but merchant needs to enable the API calls and start sending a small percentage of production traffic first. Post validation, merchants can send all traffic which will help the project move to the next step. 

### Data Accumulation Phase (Est. 4 weeks)
<!--Step 3-->

No actions for Merchant and Microsoft/Authorized Partner during this phase. Accumulation starts right after data quality is signed off during API integration phase. Continue forward once the criteria below have been achieved:                                                                                                               
- At least 500 fraudulent transactions                                                                      
- At least 5000 non-fraudulent transactions                                                                    
- At least 4 weeks data with more than 70% label maturity rate 

![step 4](media/step4-PP-onboardingguide.png)

## Resources 

Below are additional resources to help provide more details of the above-referenced integration steps:

- Dynamics 365 Fraud Protection overview: [overview of Dynamics365 Fraud Protection](/dynamics365/fraud-protection/)

- Create and provision your Azure tenant: [create and provision your Azure tenant](promocode-set-up-dfp-purchased-version.md)

- Set up a trial instance: [set up a trial instance - Dynamics 365 Fraud Protection](promocode-set-up-dfp-trial-version.md)

- Set up a purchased instance: [set up a purchased instance](promocode-set-up-dfp-purchased-version.md)

- Configure user access and assign roles: [configure user access & roles](configure-user-access.md)

- Set up purchase protection: [set up purchased protection](promocode-set-up-purchase-protection.md)

- Set up device fingerprinting: [set up device fingerprinting](device-fingerprinting.md)

- Integrate purchase protection APIs steps: [integrate purchase protection APIs](integrate-real-time-api.md)

- **Integrate purchase APIs schema documented at:** [swagger](https://dfpswagger.azurewebsites.net/index.html)

- **Integration Training Modules - deploy and work with Dyanmics 365 Fraud Protection:** [integration training modules](/training/paths/deploy-work-account-purchase-protection/)

 
