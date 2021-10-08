---
author: josaw1
description: This topic provides an overview of what custom and support lists are, and how you can manage information in lists in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 09/24/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Lists overview

---

# Lists overview

Lists help you manage information that you use to fight fraud and enforce business policies. For example, you can create a list to track payment instruments that you consider risky or user email addresses that you consider safe. You can then upload the list as a comma-separated values (CSV) file and reference it in a [rule](rules.md) to help automate decisions.

In Microsoft Dynamics 365 Fraud Protection, you can create two types of list: custom lists and support lists.

## Custom lists

Custom lists are created and defined by you. You can upload any number of custom lists and fill them with data that is specific to your business needs or your fraud protection strategy. For example, you can create a custom list that contains email addresses, IP addresses, or product IDs, and additional values that are associated with each entry. For information about how to manage custom lists, see [Manage custom lists](lists.md).

## Support lists

Support lists are predefined lists that are included in Dynamic 365 Fraud protection to help you get started. There are support lists for each of the following entities: email address, payment instrument, IP address, user ID, and device ID. You can assign entities a status of *Safe*, *Block*, or *Watch*. For information about how to manage support lists, see [Manage support lists](manage-support-lists.md).
