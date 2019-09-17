---
author: jackwi111
description: This topic provides information about how you can boost bank acceptance rates.
ms.author: v-jowigh
ms.service: fraud-protection
ms.date: 09/12/2019

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin

title: Boost bank acceptance rates with the transaction acceptance booster
---

# Boost bank acceptance rates with the transaction acceptance booster

One feature that sets Microsoft Dynamics 365 Fraud Protection apart from other products in the market is the transaction acceptance booster. This feature helps you benefit from higher acceptance rates by sharing trust knowledge with banks. 

You can opt to directly share Dynamics 365 Fraud Protection’s assessments with participating issuing banks and networks through the acceptance booster service. Another option is to receive MID recommendations from Dynamics 365 Fraud Protection and incorporate them into your authorization requests, resulting in a higher overall acceptance rate. While you can use both options on the same transactions where applicable, we recommend that you use the MID recommendation option on transactions from banks who are not participating in the acceptance booster service.

## Acceptance booster service
The acceptance booster service provides a direct communication channel for contextual transaction data, called transaction trust knowledge, with participating issuing banks and networks. This transmission occurs at the time of transaction assessment by Dynamics 365 Fraud Protection. If the payment instrument used in that transaction was issued by a bank or network participating in the program, Dynamics 365 Fraud Protection will transmit transaction trust knowledge to that bank or network. 

To enable this feature, go to the **Configuration section** of the navigation in Dynamics 365 Fraud Protection, then select the **Transaction acceptance booster** page. On the **Opt in** tab, you can select **Acceptance booster service** to consent to share transaction trust knowledge with participating banks and networks. You can review the Consent link on this page for details about terms and a list of participants in the program. Select **Save** to confirm your choice.

### Reports
To view a report of your transaction acceptance booster activity, select the **Report** tab on the **Transaction acceptance booster** page in Dynamics 365 Fraud Protection.

## Program MID

Program MID is a lightweight methodology for passing a transaction-based trust signal to the issuer. To fully benefit from the program and measure the gains, you will need to have two new MIDs in addition to your existing MID. Work with your payment processor to create the new MIDs if you currently only use one. 

It takes time to create MIDs and use them for authorization, but these tasks don't depend on real-time risk evaluation. Therefore, we recommend that you start them with your payment processor at least four weeks before you begin using Dynamics 365 Fraud Protection for decision making. 

To enable this feature, go to the **Configuration** section of the navigation in Dynamics 365 Fraud Protection, then select the **Transaction acceptance booster** page. On the **Opt in** tab, you can select Program MID to receive MID recommendations. **Save** to confirm your choice. 

Once enabled, you will receive a flag in the response payload of a purchase API call that indicates which MID you should use in the call to your bank. The flag will have one of three values: 

- **Standard** – This MID is the MID that currently exists. 
- **Program** – This MID is used for high-confidence transactions that are expected to return a higher acceptance rate. 
- **Control** – This MID provides a representative sample of performance before you start Dynamics 365 Fraud Protection, and it will be used as a baseline to measure overall gain. 

Your existing MID will be the Standard MID. You can choose which MID is the Program MID and which is the Control MID. Once you make this choice, your selection should be fixed and the MIDs should not be interchanged. 

Dynamics 365 Fraud Protection algorithms will run in real time to optimize and maximize your acceptance rate. Therefore, it's important that you follow the recommendation that you receive in the response payload. It's also important that you report back the bank authorization outcome and chargeback in a timely manner. Bank authorization outcomes and chargebacks can be reported via the API or by bulk upload of .csv files. Please refer to the [API documentation](integrate-real-time-api.md) and the [data upload documentation](data-upload.md) for more information on reporting these events.

### Reports
To view a report of your Program MID activity, go to the **Scorecard** and use the Program MID filter.
