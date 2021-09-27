---
author: josaw1
description: This topic explains functionality to support payment service providers (PSPs) in Dynamics 365 Fraud Protection.  
ms.author: josaw
ms.date: 09/30/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Payment service provider protection (preview) overview
---

# Payment service provider protection (preview) overview

[!include [preview banner](includes/preview-banner.md)]

Microsoft Dynamics 365 Fraud Protection provides merchants the capability to protect e-commerce transactions from fraudulent activity. We are extending product capabilities to provide fraud protection to PSPs. 

A single PSP alone could have hundreds to thousands of merchants who need fraud protection solution to protect their business. These merchants cover numerous industries and verticals, such as retail, gaming, digital goods, and travel. The size, structure and industries served require new fraud protection capabilities that are above and beyond that of an individual enterprise customer. 

## Manage environments

Creating new environments helps PSPs manage their merchant’s’ fraud operations, data and user access.  

For example: If you are a PSP who manages 2 merchants, you can create 2 different environments for each of your merchants. User access, fraud operations and data of each of the merchants can be hosted and managed within these dedicated environments. 

### Create a new environment

You can create a new environment by clicking on the “New environment” option under the environment picker on top right corner of fraud protection portal. The Ffollowing info will be needed to create an environment: 

1. Data Storage Geography: EU, US or Canada. 

1. Name of Environment (Name of the merchant you are trying to onboarding to that environment). 

1. Description (optional) 

1. Tags (optional): You can use tags to specify any generic information related to this environment. Such as industry vertical.  

### View environments

You can view a list of all environments under your tenant by clicking on the “Manage Environment” option under the environment picker. 

