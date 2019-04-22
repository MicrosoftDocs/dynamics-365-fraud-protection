---
author: jackwi111
description: This topic provides information about how you can boost bank acceptance rates.
ms.author: v-jowigh
ms.service: crm-online
ms.date: 02/25/2019

ms.topic: conceptual
title: Boost bank acceptance rates
---

# Boost bank acceptance rates

One feature that sets Microsoft Dynamics 365 Fraud Protection apart from other products in the market is named the transaction acceptance booster. This feature helps you benefit from higher acceptance rates by sharing trust knowledge with banks. Currently, a Program Merchant ID (MID) program is used to share trust knowledge.

## Program MID

Program MID is a lightweight methodology for passing a transaction-based trust signal to the issuer. To fully benefit from the program and measure the gains, we require two new MIDs in addition to your existing MID. Work with your payment processor to create the new MIDs, and then email them to the Dynamics 365 Fraud Protection team at <dfpissuersupport@microsoft.com>. Microsoft representatives will work with participating banks and issuers to enroll the new MIDs in the transaction booster acceptance program.

It takes time to create MIDs and communicate them to banks, but these tasks don't depend on real-time risk evaluation. Therefore, we recommend that you start them with your payment processor at least four weeks before you start to use Dynamics 365 Fraud Protection for decision making.

When you're ready to use the Protect experience and the transaction acceptance booster in your live production environment, you must pass a flag to send the Protect assessment type in your call to the Purchase application programming interface (API). Don't send the Evaluate assessment type. To determine the appropriate flag, look at the **AssessmentType** attribute in the Purchase event API. It has one of the following values:

- **Evaluate** for the Evaluate assessment type
- **Protect** for the Protect assessment type

Only the Purchase event is an assessment API. No other event API is an assessment API.

In the response payload, you will receive a flag that indicates which MID you should use in the call to your bank. The flag will have one of three values:

- **Standard** – This MID is the MID that currently exists.
- **Program** – This MID is used for high-confidence transactions that are expected to return a higher acceptance rate.
- **Control** – This MID provides a representative sample of performance before you start Dynamics 365 Fraud Protection, and it will be used as a baseline to measure overall gain.

Your existing MID will be the Standard MID. The Dynamics 365 Fraud Protection team will notify you which MID is the Program MID, and which is the Control MID. Dynamics 365 Fraud Protection algorithms will run in real time to optimize and maximize your acceptance rate. Therefore, it's important that you comply with the flag that you receive in the response payload. It's also important that you report back the bank authorization outcome and chargeback in a timely manner.
