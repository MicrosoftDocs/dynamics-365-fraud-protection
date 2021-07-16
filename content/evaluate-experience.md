---
author: josaw1
description: This topic provides information about the Evaluate experience in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 04/02/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Evaluate experience overview
---

# Evaluate experience overview

The evaluate experience in Microsoft Dynamics 365 Fraud Protection allows you to use your real-time transactional traffic to compare Fraud Protection with your existing fraud solution. You can send transactions through real-time application programming interfaces (APIs) to get an inline evaluation, and you can upload historical and asynchronous data to tune the model to your business scenarios. You can then use Fraud Protection to gain deeper insights into your data, tailor your risk management strategies, and support your customers.

## Using the evaluate experience

Get started with Fraud Protection by completing the initial configuration steps outlined on the **Dashboard**. Then follow these steps to begin using the evaluate experience:

- [Integrate the Dynamics 365 Fraud Protection APIs](integrate-real-time-api.md) and pass 'Evaluate' for the AssessmentType field in Purchase, Signup, and CustomFraudEvaluation API events. 

    For documentation about all supported events, see <a href="https://go.microsoft.com/fwlink/?linkid=2084942" target="_blank">Dynamics 365 Fraud Protection API</a>.
- Observe, but don't necessarily honor, the Fraud Protection merchant rule decisions to either approve or reject those same events.
- Evaluate your current fraud protection strategies by [uploading historical data](data-upload.md) and learn about Fraud Protection's performance via the [scorecard](scorecard.md).

## Features

The evaluate experience in Fraud Protection provides the features that are described in the following topics:


- [Purchase protection](purchase-protection.md)
- [Artificial intelligence (AI) and insights from the fraud protection network](fraud-protection-network.md)
- [Send real-time data using the Dynamics 365 Fraud Protection API](./integrate-real-time-api.md)
- [Visually explore your data](graph-explorer.md)
- [Implement device fingerprinting](device-fingerprinting.md)
- [Support your customers](risk-support.md)

The protect experience is differentiated from evaluate by additional features as described in the [protect experience](protect-experience.md) topic, and becomes your real-time tool in your full production environment.


[!INCLUDE[footer-include](includes/footer-banner.md)]
