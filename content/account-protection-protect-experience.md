---
author: kelsiefu
description: This topic provides information about the protect experience in Microsoft Dynamics 365 Fraud Protection.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 07/07/2020
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Account protection protect experience
---

# Account protection protect experience

Microsoft Dynamics 365 Fraud Protection offers two operating modes: evaluate and protect. These operating modes provide two ways of using the same underlying product (that is, they provide two *experiences*). The same functionality and feature capabilities are available in both experiences.

In protect mode, you follow the guidance and recommendations from the analysis. These results help you determine whether you should accept or reject transactions, or which escalation path you should take.

> [!IMPORTANT]
> You're responsible for respecting the separation of modes. You're also responsible for indicating the operating mode to the product via the **AssessmentType** field in assessment application programming interface (API) calls. You can choose how you want to allocate traffic between the protect and evaluate modes at any time.

## Using the protect experience

To get started with Fraud Protection, complete the initial configuration steps that are outlined on the dashboard. Then follow these steps to begin to use the protect experience.

1. [Integrate the Fraud Protection APIs](integrate-ap-api.md), and pass **'Protect'** for the **AssessmentType** field in **Account Creation** and **Account LogIn** API events. For information about all supported events, see [Dynamics 365 Fraud Protection API](https://go.microsoft.com/fwlink/?linkid=2084942).
2. Honor the decisions that Fraud Protection merchant rules make about whether those events should be approved, rejected, challenged, or reviewed.


[!INCLUDE[footer-include](includes/footer-banner.md)]