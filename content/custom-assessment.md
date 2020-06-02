---
author: yvonnedeq
description: This topic provides information about creating and defining custom assessments.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 06/02/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Custom Assessment


---

# Custom Assessment

## Overview

Effectively managing fraud is a multi-tiered strategy. In order to effectively maximize fraud detection and minimize customer friction, interactions at various phases of a user’s journey must be assessed and decisions must be made whether to allow, challenge, or block the user from proceeding further. Each business model is different and so are the associated user interactions that transmit signals about potential fraud. Profile updates such as address change or payment information change may be a key event for an e-commerce business while submission of reviews might be for another. Updating a seat preference on a travel site, adding family and friends on a subscription or gaming service, raising a support ticket, or submitting a complaint are other examples of user events which are specific to each business model.
Microsoft Dynamics 365 Fraud Protection understands the importance of including these types of business-specific events to help you in the overall fraud management strategy, and now offers the ability to add *custom assessments* in addition to the common assessment events such as account creation, account login, and purchase protection.
With custom assessments, you can create and define an assessment, including its name, the API path, and a payload that is appropriate to the specific event. You can then use the same assessment to make decisions on other events.
