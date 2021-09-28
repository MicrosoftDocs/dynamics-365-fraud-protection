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

The following features are included in the October 2021 release of Dynamics 365 Fraud Protection:
- Payment service provider (PSP) enablement.
- Deeper fraud analytics and reporting for purchase and account protection scenarios.

## Payment service provider (PSP) enablement

The October release provides new capabilities to enhance PSPs ability to offer Fraud Protection as a value-added fraud protection service to their merchants.

PSPs can integrate Fraud Protection into their existing infrastructure to manage PSP taxonomies that encompass many merchants and multiple hierarchies within each merchant entity. Other PSP-focused scenarios are supported, including: 
- Manage the creation and addition of multiple merchants.
- Observe and manage merchant fraud performance across a single merchant, multiple merchants, and across PSP verticals using artificial intelligence.

## Fraud analytics and reporting for purchase and account protection 

Fraud Protection provides curated data sets, metrics, and Microsoft Power BI reports for purchase protection and account protection. 

- The score rule optimizer, fraud tracker, rule monitor, and monthly business review reports for purchase protection enable you to:
  - Analyze historical transaction data.
  - Perform operational tasks.
  - Make informed operational decisions. For example, you have access to data to help you make decisions pertaining to the score threshold, rejection of risky transactions, estimating score threshold impact, analyzing fraud trends and performance, and conducting deep dive analysis with a lens on purchase fraud. 

- The threat vulnerability analyzer and threat vulnerability trend reports for account protection enable you to:
  - Analyze account protection session data.
  - Investigate threat and fraud attacks at the session level.
  - Make informed operational decisions. For example, you have richer insights pertaining to setting the score threshold, segmenting threat traffic, estimating score threshold impact, analyzing abusive traffic patterns, and validating machine learning score performance. The interactive reports provide intelligence on various dimensions including geolocation, device configuration, IP, and reason code. 
    >[!NOTE]
    >The report from the tool refreshes every 24 hours with the latest account protection sessions. It retains account login and account creation sessions from the previous four weeks. The threat vulnerability trend report retains account login and account creation metrics and data from the previous four months.
