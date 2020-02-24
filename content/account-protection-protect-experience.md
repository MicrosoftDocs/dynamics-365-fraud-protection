---
author: kelsiefu
description: This topic provides information about the protect experience in Microsoft Dynamics 365 Fraud Protection.
ms.author: kelsiefu
ms.service: fraud-protection
ms.date: 2/24/2020
ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Account protection protect experience
---

# Account protection protect experience

Dynamics 365 Fraud Protection offers evaluate and protect which are two different ways (modes) of using the same underlying product. There is no difference in the functionality or the feature capability in the two experiences. The Protect experience in Fraud Protection implies that you are using Fraud Protection to impact your final decisions in your production environment. You can take advantage of model scores to decide whether to accept or reject transactions, and adjudicate escalations from.

[!IMPORTANT]
>It is up to you to respect the separation of modes and indicate it to the product via the AssessmentType in the assessment API calls. You are free to choose how you allocate traffic between the Protect and Evaluate modes at any given time.

## Using the protect experience

To get started with Fraud Protection, complete the initial configuration steps that are outlined on the dashboard. Then follow these steps to begin to use the Protect experience:

1. [Integrate the Fraud Protection application programming interfaces (APIs)](integrate-ap-api.md), and pass **'Protect'** for the **AssessmentType** field in **Account Creation** and **Account LogIn** API events. For documentation of all supported events, see see <a href="https://go.microsoft.com/fwlink/?linkid=2084942" target="_blank">Dynamics 365 Fraud Protection API</a>.
2. Honor the decision of Fraud Protection merchant rules to either approve, reject, challenge, or review those same events.

