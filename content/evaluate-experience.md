---
author: jegrif
description: This topic provides information about the Evaluate experience in Microsoft Dynamics 365 Fraud Protection.
ms.author: v-jegrif
ms.service: fraud-protection
ms.date: 09/12/2019
ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Evaluate experience
---

# Evaluate experience

Microsoft Dynamics 365 Fraud Protection's *Evaluate experience* lets you use your real-time transactional traffic to compare Dynamics 365 Fraud Protection with your existing fraud solution. You can send transactions through real-time application programming interfaces (APIs) to get an inline evaluation, and you can upload historical and asynchronous data to tune the model to your business scenarios. You can then use Dynamics 365 Fraud Protection to gain deeper insights into your data, tailor your risk management strategies, and support your customers.

## Using the Evaluate experience


Get started with Dynamics 365 Fraud Protection by completing the initial configuration steps outlined on the **Dashboard**. Then follow these steps to begin using the Evaluate experience:

- [Integrate the Dynamics 365 Fraud Protection APIs](integrate-real-time-api.md) and pass 'Evaluate' for the AssessmentType field in Purchase, Signup, and CustomFraudEvaluation API events. For documentation about all supported events, see <a href="https://go.microsoft.com/fwlink/?linkid=2084942" target="_blank">Dynamics 365 Fraud Protection API</a>.
- Observe, but don't necessarily honor, the Dynamics 365 Fraud Protection merchant rule decisions to either approve or reject those same events.
- Evaluate your current fraud protection strategies by [uploading historical data](data-upload.md) and learn about Dynamics 365 Fraud Protection's performance via the [scorecard](scorecard.md).

## Features

The Evaluate experience in Dynamics 365 Fraud Protection provides the features that are described in the following topics:


- [Purchase protection](purchase-protection.md)
- [Artificial intelligence (AI) and insights from the fraud protection network](fraud-protection-network.md)
- [Send real-time data using the Dynamics 365 Fraud Protection API](send-real-time-api.md)
- [Visually explore your data](graph-explorer.md)
- [Implement device fingerprinting](device-fingerprinting.md)
- [Support your customers](risk-support.md)

The Protect experience is differentiated from Evaluate by additional features as described on [Protect experience](protect-experience.md), and becomes your real-time risk decision tool in your full production environment.
