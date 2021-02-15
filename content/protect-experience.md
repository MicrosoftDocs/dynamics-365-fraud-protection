---
author: yvonnedeq
description: This topic provides information about the protect experience in Fraud Protection.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 07/09/2020
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: The protect experience in Fraud Protection
---

# The protect experience in Fraud Protection

The *protect experience* in Microsoft Dynamics 365 Fraud Protection builds on the features of the evaluate experience by embedding Fraud Protection into your full production environment, where it becomes your real-time tool for fraud protection. You can take advantage of model scores to decide whether to accept or reject transactions, adjudicate escalations from customers, and share relevant information about transaction trustworthiness with participating banks and issuers to help boost their acceptance rates.

## Using the protect experience

To get started with Fraud Protection, complete the initial configuration steps that are outlined on the dashboard. Then follow these steps to begin to use the protect experience:

1. [Integrate the Fraud Protection application programming interfaces (APIs)](integrate-real-time-api.md), and pass **'Protect'** for the **AssessmentType** field in **Purchase**, **Signup**, and **CustomFraudEvaluation** API events. 

    For documentation of all supported events, see <a href="https://go.microsoft.com/fwlink/?linkid=2084942" target="_blank">Dynamics 365 Fraud Protection API</a>.
    
1. Honor the decision of Fraud Protection merchant rules to either approve or reject those same events.

## Features

The Protect experience in Fraud Protection provides the features that are described in the following topics:

- [Purchase protection](purchase-protection.md)
- [Artificial intelligence (AI) and insights from the fraud protection network](fraud-protection-network.md)
- [Integrate Dynamics 365 Fraud Protection real-time APIs](integrate-real-time-api.md)
- [Visually explore your data](graph-explorer.md)
- [Implement device fingerprinting](device-fingerprinting.md)
- [Support your customers](risk-support.md)
- [Boost bank acceptance rates with the transaction acceptance booster](transaction-acceptance-booster.md)


[!INCLUDE[footer-include](includes/footer-banner.md)]