author: cschlegel2
description: This article explains Dynamics Fraud Protection 
ms.author: cschlege2
ms.date: 10/12/2022
ms.topic: reference
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - Admin
  - IT Pro
title: Onboarding Planning Guide for Purchase Protection
ms.custom:


**Integration Planning Guide** This guide helps you understand and plan for the project milestones of Dynamics 365 Fraud Protection Purchase Protection integration and onboarding. To understand the integration steps below in more detail, please review the integration guide:  [set up purchase protection](https://learn.microsoft.com/dynamics365/fraud-protection/promocode-set-up-purchase-protection)

**Onboarding Milestones - Integration Breakdown and Approximate Time** 

**Note:** All timeframes below are estimates. Actual time taken can vary based on Merchant, and Microsoft/Authorized Partner availability and focus. 

 

![step1.](media/pp-onboarding-guide-steponeclean.png)


![step2.](media/step2-PP-onboardingguide.png)

**Note:** Microsoft would perform data validation, but merchant needs to enable the API calls and start sending a small percentage of production traffic first. Post validation, merchants can send all traffic which will help the project move to the next step. 


**Step 3. Data Accumulation Phase (Est. 4 weeks)** 

No actions for Merchant and Microsoft/Authorized Partner during this phase. Accumulation starts right after data quality is signed off during API integration phase. Continue forward once the criteria below have been achieved:                                                                                                               

- At least 500 fraudulent transactions                                                                      

- At least 5000 non-fraudulent transactions                                                                    

- At least 4 weeks data with more than 70% label maturity rate 


![step1.](media/step4-PP-onboardingguide.png)


​ 
**Resources:** 

Below are additional resources to help provide more details of the above-referenced integration steps:


- Dynamics 365 Fraud Protection overview: [overview of Dynamics365 Fraud Protection](https://learn.microsoft.com/dynamics365/fraud-protection/)

 
- Create and provision your Azure tenant: [create and provision your Azure tenant](https://learn.microsoft.com/dynamics365/fraud-protection/promocode-set-up-dfp-purchased-version)


- Set up a trial instance: [set up a trial instance - Dynamics 365 Fraud Protection](https://learn.microsoft.com/dynamics365/fraud-protection/promocode-set-up-dfp-trial-version)


 

- Set up a purchased instance: [set up a purchased instance](https://learn.microsoft.com/dynamics365/fraud-protection/promocode-set-up-dfp-purchased-version)

 

- Configure user access and assign roles: [configure user access & roles](https://learn.microsoft.com/dynamics365/fraud-protection/configure-user-access)

 

- Set up purchase protection: [set up purchased protection](https://learn.microsoft.com/dynamics365/fraud-protection/promocode-set-up-purchase-protection)

 

- Set up device fingerprinting: [set up device fingerprinting](https://learn.microsoft.com/dynamics365/fraud-protection/device-fingerprinting)

 

- Integrate purchase protection APIs steps: [integrate purchase protection APIs](https://learn.microsoft.com/dynamics365/fraud-protection/integrate-real-time-api)

 

- **Integrate purchase APIs schema documented at:**  [swagger](https://dfpswagger.azurewebsites.net/index.html)

 

- **Integration Training Modules - deploy and work with Dyanmics 365 Fraud Protection:** [integration training modules](https://learn.microsoft.com/training/paths/deploy-work-account-purchase-protection/)

 
