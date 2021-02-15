---
author: yvonnedeq
description: This topic provides information about how you can boost bank acceptance rates.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 07/09/2020
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin

title: Boost bank acceptance rates

---

# Boost bank acceptance rates

One feature that sets Microsoft Dynamics 365 Fraud Protection apart from other products in the market is the transaction acceptance booster. This feature helps you benefit from higher acceptance rates by sharing trust knowledge with banks. 

You can opt to directly share Fraud Protection's assessments with participating issuing banks and networks through the acceptance booster service. Another option is to receive MID recommendations from Fraud Protection and incorporate them into your authorization requests, resulting in a higher overall acceptance rate. While you can use both options on the same transactions where applicable, we recommend that you use the MID recommendation option on transactions from banks who are not participating in the acceptance booster service.

## Acceptance booster service
The acceptance booster service provides a direct communication channel for contextual transaction data, called transaction trust knowledge, with participating issuing banks and networks. This transmission occurs at the time of transaction assessment by Fraud Protection. If the payment instrument used in that transaction was issued by a bank or network participating in the program, Fraud Protection will transmit transaction trust knowledge to that bank or network. 

#### To enable the acceptance booster service:

1. Select **Settings**, and then select **Transaction acceptance booster**. 
1. On the **Opt in** tab, select **Acceptance booster service** to consent to share transaction trust knowledge with participating banks and networks. 
1. Select **Consent** to review details about the terms and a list of participants in the program. 
1. Select **Save** to confirm your choice.

### Reports

To view a report of your transaction acceptance booster service, select **Settings**, select **Transaction acceptance booster**, and then select the **Report** tab.

## Program MID

Program MID is a lightweight methodology for passing a transaction-based trust signal to the issuer. To fully benefit from the program and measure the gains, you will need to have two new MIDs in addition to your existing MID. Work with your payment processor to create the new MIDs if you currently only use one. 

It takes time to create MIDs and use them for authorization, but these tasks don't depend on real-time risk evaluation. Therefore, we recommend that you start them with your payment processor at least four weeks before you begin using Fraud Protection for decision making. 

#### To enable Program MID: 

1. Select **Settings**, and then select **Transaction acceptance booster**.
1. On the **Opt in** tab, select **Program MID** to 
receive MID recommendations. 
1. Select **Consent** to review details about the terms and a list of participants in the program. 
1. Select **Save** to confirm your choice. 

Once enabled, you will receive a flag in the response payload of a purchase API call that indicates which MID you should use in the call to your bank. The flag will have one of three values: 

- **Standard** – This MID is the MID that currently exists. 
- **Program** – This MID is used for high-confidence transactions that are expected to return a higher acceptance rate. 
- **Control** – This MID provides a representative sample of performance before you start Fraud Protection, and it will be used as a baseline to measure overall gain. 

Your existing MID will be the Standard MID. You can choose which MID is the Program MID and which is the Control MID. Once you make this choice, your selection should be fixed and the MIDs should not be interchanged. 

Fraud Protection algorithms run in real time to optimize and maximize your acceptance rate. Therefore, it's important that you follow the recommendation that you receive in the response payload. It's also important that you report back the bank authorization outcome and chargeback in a timely manner. Bank authorization outcomes and chargebacks can be reported via the API or by bulk upload of .csv files. 

See the [API documentation](integrate-real-time-api.md) and the [data upload documentation](data-upload.md) for more information on reporting these events.

### Reports
To view a report of your Program MID activity, select **Scorecard** and then select the **MID classification** filter.


[!INCLUDE[footer-include](includes/footer-banner.md)]