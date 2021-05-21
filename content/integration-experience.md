---
author: josaw1
description: This topic describes the integration experience functionality in Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 05/20/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Integration experience (preview)

---

# Integration experience (preview)

[!include [banner](includes/preview-banner.md)]

The customer product adoption journey starts with the first touchpoint and continues with consistent, positive experiences from trial to purchase. In this journey, every interaction that customers experience needs to be personalized. The journey starts with a seamless onboarding experience, which plays an important role when it comes to product adoption and usage. Onboarding also helps the product gain valuable information about the customer’s behavior and provides additional insights into the customer journey.

## Integration experience

The integration experience (preview) provides a guided integration process for each product capability, with well-defined start and end points. This is achieved by providing out-of-the-box code snippets and step-by-step instructions that can be started from within the product. The guided processes are interactive and provide clear instructions to customers about what they need to do during integration and why.

The guided processes have been separated by the integration experiences that are required to enable use of the product. For example, Azure Active Directory application integration and device fingerprinting must be enabled for the Account Protection integration and Purchase Protection integration processes.

The real-time API integration experience has been split into two categories, based on which capabilities you are integrating. If you are integrating Purchase Protection, you follow the Purchase Protection API integration steps. If you are integrating Account Protection, you follow the Account Protection API integration steps.

Each integration experience is designed to provide a clear, milestone-based approach. When customers successfully complete an API integration, they are guided to the next integration process so that they are always able to track their progress.

Integration experiences can be launched more than once and can be personalized based on user input. For example, a customer may want to run the steps for integrating the Purchase API twice if they want to integrate both their website and their mobile ecosystem.

There's also an integration wizard that can detect errors during the integration steps and provide guidance regarding what corrective actions may need to be taken. Common errors are often related to authorization, certificate upload, and data quality issues. 

