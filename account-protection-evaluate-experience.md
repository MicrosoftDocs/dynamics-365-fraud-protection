---
author: kelsiefu
description: This topic provides information about the evaluate experience in Microsoft Dynamics 365 Fraud Protection.
ms.author: kelsiefu
ms.service: fraud-protection
ms.date: 2/25/2020
ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Account protection evaluate experience
---

# Account protection evaluate experience

[!include [banner](includes/preview-banner.md)]

Dynamics 365 Fraud Protection offers evaluate and protect which are two different ways (modes) of using the same underlying product. There is no difference in the functionality or the feature capability in the two experiences. Evaluate mode allows you to “shadow” your incumbent solution without affecting its operation. In protect mode, you can compare the performance in the scorecard experience by toggling on the AssessmentType. You can send transactions through real-time application programming interfaces (APIs) to get an inline evaluation. You can then use Fraud Protection to gain deeper insights into your data, tailor your risk management strategies, and support your customers.

[!IMPORTANT]
> It is up to you to respect the separation of modes and indicate it to the product via the AssessmentType in the assessment API calls. You are free to choose how you allocate traffic between the protect and evaluate modes at any given time.

## Using the evaluate experience

Get started with Fraud Protection by completing the initial configuration steps outlined on the **Dashboard**. Then follow these steps to begin using the evaluate experience:

- [Integrate the Dynamics 365 Fraud Protection APIs](integrate-real-time-api.md) and pass 'Evaluate' for the AssessmentType field in AccountCreation and AccountLogIn API events. For documentation about all supported events, see <a href="https://go.microsoft.com/fwlink/?linkid=2084942" target="_blank">Dynamics 365 Fraud Protection API</a>.
- Observe, but don't necessarily honor, the Fraud Protection merchant rule decisions to approve, reject, challenge, or review those same events.

