---
author: kelsiefu
description: This topic provides information about the evaluate experience in Microsoft Dynamics 365 Fraud Protection.
ms.author: kelsiefu
ms.service: fraud-protection
ms.date: 07/07/2020
ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Account protection evaluate experience
---

# Account protection evaluate experience

Microsoft Dynamics 365 Fraud Protection offers two operating modes: evaluate and protect. These operating modes provide two ways of using the same underlying product (that is, they provide two *experiences*). The same functionality and feature capabilities are available in both experiences.

In evaluate mode, you can "shadow" your existing solution without affecting its operation. In protect mode, you can compare the analysis performance by switching the value of **AssessmentType** field (e.g. from 'protect' to 'evaluate'). The values in the scorecard will reflect your changes. You can send transactions through real-time application programming interfaces (APIs) to get an inline evaluation. You can then use Fraud Protection to gain deeper insights into your data, customize your risk management strategies, and support your customers.

> [!IMPORTANT]
> You're responsible for respecting the separation of modes. You're also responsible for indicating the operating mode to the product via the **AssessmentType** field in assessment API calls. You can choose how you want to allocate traffic between the protect and evaluate modes at any time.

## Using the evaluate experience

To get started with Fraud Protection, complete the initial configuration steps that are outlined on the dashboard. Then follow these steps to begin to use the evaluate experience.

1. [Integrate the Fraud Protection APIs](integrate-real-time-api.md), and pass **'Evaluate'** for the **AssessmentType** field in **AccountCreation** and **AccountLogIn** API events. For information about all supported events, see [Dynamics 365 Fraud Protection API](https://go.microsoft.com/fwlink/?linkid=2084942).
2. Observe, but don't necessarily honor, the decisions that Fraud Protection merchant rules make about whether those events should be approved, rejected, challenged, or reviewed.
