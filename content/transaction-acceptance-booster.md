---
author: jackwi111
description: Boost bank acceptance rates
ms.author: v-jowigh
ms.date: 02/25/2019
ms.service:
 - d365-fraud-protection
ms.topic: conceptual
title: Boost bank acceptance rates
---


# Boost bank acceptance rates

Dynamics 365 Fraud Protection offers a market differentiating feature, called *transaction acceptance booster*, that enables you to benefit from higher acceptance rates by sharing trust knowledge with banks. Initially, this is achieved using a Program Merchant ID (MID) program. 

## Program MID

Program MID is a lightweight methodology for passing a transaction-based trust signal to the issuer. To fully benefit from the program and measure the gains, we require two new MIDs in addition to your existing MID. You will work with your payment processor to create these two new MIDs, and email them to the Dynamics 365 Fraud Protection team at dfpissuersupport@microsoft.com. Microsoft representatives will work with participating banks and issuers to enroll these new MIDs into the transaction booster acceptance program. Because MID creation and communication with banks requires time and is not dependent on real-time risk evaluation, we advise that you start the process with your payment processor at least four weeks before using Dynamics 365 Fraud Protection for decisioning. 

When you are ready for live production using the Protect experience and the transaction acceptance booster, you must pass a flag to send the Protect assessment type in your Purchase API call. Do not send the Evaluate assessment type. To determine the appropriate flag, the attribute name in the Purchase API is identified as AssessmentType with either value:

- Evaluate for the Evaluate assessment type
- Protect for the Protect assessment type

Only the purchase event is an assessment API, whereas all the other event APIs are not.

In the response payload, you will receive a flag indicating which MID is to be used in the call to your bank. The flag will contain one of three values:

- Standard: Currently existing.
- Program: Used for high-confidence transactions expected to return a higher acceptance yield.
- Control: Provides a representative sample of performance before you start Dynamics 365 Fraud Protection, and will be used as baseline for measuring overall gain. 

Your existing MID will be the Standard. The Dynamics 365 Fraud Protection team will notify you which MID is the Program and which one is the Control. Dynamics 365 Fraud Protection algorithms will be running in real time to optimize for maximizing your acceptance rate. Consequently, it is important that you comply with the flag received in the response payload, and report back the bank authorization outcome and chargeback in a timely manner.
