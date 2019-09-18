---
author: jegrif
description: This topic provides information about the Protect experience in Microsoft Dynamics 365 Fraud Protection.
ms.author: v-jegrif
ms.service: fraud-protection
ms.date: 09/12/2019

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin

title: Protect experience
---

# Protect experience

Microsoft Dynamics 365 Fraud Protection's *Protect experience* builds on the features of the Evaluate experience by embedding Dynamics 365 Fraud Protection into your full production environment, where it becomes your real-time risk decision tool for fraud protection. You can take advantage of model scores to decide whether to accept or reject transactions, adjudicate escalations from customers, and share relevant information about transaction trustworthiness with participating banks and issuers to help boost their acceptance rates.

## Using the Protect experience
Get started with Dynamics 365 Fraud Protection by completing the initial configuration steps outlined on the **Dashboard**. Then follow these steps to begin using the Protect experience:

- [Integrate with the Dynamics 365 Fraud Protection APIs](integrate-real-time-api.md) and pass 'Protect' for the AssessmentType field in Purchase, Signup, and CustomFraudEvaluation API events.
- Honor the Dynamics 356 Fraud Protection merchant rule decision to either approve or reject those same events.

## Features
The Protect experience in Dynamics 365 Fraud Protection provides the features that are described in the following topics:

- [Purchase protection](purchase-protection.md)
- [Artificial intelligence (AI) and insights from the fraud protection network](fraud-protection-network.md)
- [Integrate with the Dynamics 365 Fraud Protection APIs](integrate-real-time-api.md)
- [Visually explore your data](graph-explorer.md)
- [Implement device fingerprinting](device-fingerprinting.md)
- [Support your customers](risk-support.md)
- [Boost bank acceptance rates with the transaction acceptance booster](transaction-acceptance-booster.md)
