---
author: josaw1
description: This article explains how payment service providers (PSPs) can manage environments in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 06/07/2022
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Manage environments
---

# Manage environments


By creating new environments for their merchants, payment service providers (PSPs) can better manage fraud operations, data, and user access for those merchants. For example, if you're a PSP who manages two merchants, you can create two environments, one for each merchant. In that way, each merchant's fraud operations, data, and user access can be hosted and managed in a dedicated environment.

## Create a new environment

To create a new environment, select **New environment** under the environment picker in the upper right of the Microsoft Dynamics 365 Fraud Protection portal page. Then enter the following information:

- **Data storage geography** – Select **EU**, **US**, or **Canada**.
- **Name of environment** – The name should be the name of the merchant that you will onboard into the environment.
- **Description (optional)** – You can add some information to help identify the environment.
- **Tags (optional)** – You can use tags to specify any generic information that is related to the environment, such as the industry vertical.

## View environments

To view a list of all the environments under your tenant, select **Manage environment** under the environment picker.

## Additional resources

[Payment service provider enablement](psp-overview.md)

[Integrate purchase protection APIs](integrate-real-time-api.md)

[Labels API](labels-api.md)

[Set up device fingerprinting](device-fingerprinting.md)

[View purchase protection schemas](view-purchase-protection-schemas.md)

[Manage rules](rules.md)

[Fraud tracker tool](fraud-tracker.md)
