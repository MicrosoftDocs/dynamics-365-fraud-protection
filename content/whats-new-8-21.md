---
author: josaw1
description: This topic explains what's new in the Microsoft Dynamics 365 Fraud Protection October 2021 release.
ms.author: josaw
ms.date: 09/30/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: What's new in Dynamics 365 Fraud Protection October 2021 release
---

# What's new in Dynamics 365 Fraud Protection October 2021 release

[!include [preview banner](includes/preview-banner.md)]

The following features are included in the October 2021 release of Microsoft Dynamics 365 Fraud Protection:

- Payment service provider (PSP) enablement
- Deeper fraud analytics and reporting for purchase and account protection scenarios

## Payment service provider enablement

The October release provides new capabilities that enhance the ability of PSPs to offer Fraud Protection to their merchants as a value-added fraud protection service.

PSPs can integrate Fraud Protection into their existing infrastructure. In that way, they can manage PSP taxonomies that encompass many merchants and multiple hierarchies within each merchant entity. Other PSP-focused scenarios are also supported. Here are some examples:

- Manage the creation and addition of multiple merchants.
- Use artificial intelligence to observe and manage merchant fraud performance across a single merchant, across multiple merchants, and across PSP verticals.

## Fraud analytics and reporting for purchase and account protection

Fraud Protection provides curated data sets, metrics, and Power BI reports for purchase protection and account protection.

- The score rule optimizer, fraud tracker, rule monitor, and monthly business review reports for purchase protection let you complete these tasks:

    - Analyze historical transaction data.
    - Perform operational tasks.
    - Make informed operational decisions. For example, you have access to data that can help you make decisions that are related to the score threshold, rejecting risky transactions, estimating score threshold impact, analyzing fraud trends and performance, and conducting deep-dive analysis that provides a lens on purchase fraud. 

- The threat vulnerability analyzer and threat vulnerability trend reports for account protection let you complete these tasks:

    - Analyze account protection session data.
    - Investigate threat and fraud attacks at the session level.
    - Make informed operational decisions. For example, you gain richer insights that are related to setting the score threshold, segmenting threat traffic, estimating score threshold impact, analyzing abusive traffic patterns, and validating the performance of machine learning scores. The interactive reports provide intelligence about various dimensions, such as geolocation, device configuration, IP address, and reason code.

    > [!NOTE]
    > The report from the tool is updated with the latest account protection sessions every 24 hours. It retains account sign-in and account creation sessions from the previous four weeks. The threat vulnerability trend report retains account sign-in and account creation metrics and data from the previous four months.
