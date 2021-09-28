---
author: josaw1
description: This topic explains how payment service providers (PSPs) can manage environments in Dynamics 365 Fraud Protection.  
ms.author: josaw
ms.date: 09/30/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Manage environments (PSPs)
---

# Manage environments (PSPs)

[!include [preview banner](includes/preview-banner.md)]

By creating new environments for their merchants, PSPs can better manage their merchants' fraud operations, their data, and their user access. 
For example, if you are a PSP who manages two merchants, you can create two different environments, one for each of your merchants. That way, user access, data, and fraud operations for each of the merchants can be hosted and managed within these dedicated environments. 

## Create a new environment

To create a new environment, select **New environment** under the environment picker on the top right of the Fraud Protection portal page. The following information is needed to create an environment: 

1. **Data storage geography** - Select EU, US, or Canada. 

1. **Name of environment** - The name should be the name of the merchant you will onboard to that environment. 

1. **Description (optional)** - Add some information to help identify the environment. 

1. **Tags (optional)** - You can use tags to specify any generic information related to this environment, such as industry vertical.  

## Display environments

To display a list of all of the environments under your tenant, select **Manage environment** under the environment picker. 

## Additional resources

[Payment service provider enablement (preview)](psp-overview.md)

[Integrate purchase protection APIs](integrate-real-time-api.md)  

[Labels API](labels-api.md) 

[Set up device fingerprinting](device-fingerprinting.md) 

[View purchase protection schemas](view-purchase-protection-schemas.md) 

[Manage rules](rules.md)  

[Fraud tracker tool](fraud-tracker.md)  
