---
author: jackwi111
description: This topic provides information about how you can boost bank acceptance rates.
ms.author: v-jowigh
ms.service: crm-online
ms.date: 08/22/2019

ms.topic: conceptual
title: Boost bank acceptance rates
---

# Boost bank acceptance rates

One feature that sets Microsoft Dynamics 365 Fraud Protection apart from other products in the market is the transaction acceptance booster. This feature helps you benefit from higher acceptance rates by sharing trust knowledge with banks. Currently, a Program Merchant ID (MID) program is used to share trust knowledge. 

## Program MID

Program MID is a lightweight methodology for passing a transaction-based trust signal to the issuer. To fully benefit from the program and measure the gains, we require two new MIDs in addition to your existing MID. Work with your payment processor to create the new MIDs.

It takes time to create MIDs and use them for authorization, but these tasks don't depend on real-time risk evaluation. Therefore, we recommend that you start them with your payment processor at least four weeks before you start to use Dynamics 365 Fraud Protection for decision making.

In the response payload, you will receive a flag that indicates which MID you should use in the call to your bank. The flag will have one of three values: 

- **Standard** – This MID is the MID that currently exists. 
- **Program** – This MID is used for high-confidence transactions that are expected to return a higher acceptance rate. 
- **Control** – This MID provides a representative sample of performance before you start Dynamics 365 Fraud Protection, and it will be used as a baseline to measure overall gain. 

Your existing MID will be the Standard MID. You can choose which MID is the Program MID and which is the Control MID. Once you make this choice, your selection should be fixed and the MIDs should not be interchanged. 
Dynamics 365 Fraud Protection algorithms will run in real time to optimize and maximize your acceptance rate. Therefore, it's important that you follow the recommendation that you receive in the response payload. It's also important that you report back the bank authorization outcome and chargeback in a timely manner. 
