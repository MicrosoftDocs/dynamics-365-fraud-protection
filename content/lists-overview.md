---
author: josaw1
description: This topic provides an overview of what support and custom lists are, and how to manage information on lists in Dynamics 365 Fraud Protection.  
ms.author: josaw
ms.date: 09/24/2021
ms.topic: how-to
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Lists overview

---

# Lists overview

Lists help you manage information that you use to fight fraud and enforce business policies. For example, you can create a list to track payment instruments that you consider risky or user email addresses that you consider safe. You can then upload the list as a comma-separated values (CSV) file and then reference it in a [rule](rules.md) to help automate decisions. 

In Microsoft Dynamics 365 Fraud Protection, there are two types of list that you can create, custom lists and support lists. 

## Custom lists

Custom lists are created and defined by you. You can upload any number of custom lists and fill them with data that is specific to your business needs or your fraud protection strategy. For example, you can create a custom list that contains email addresses, IP addresses, or product IDs, and additional values that are associated with each entry. For details on how to manage custom lists, see [Manage custom lists](lists.md).

## Support lists

Support lists are predefined lists included in Dynamic 365 Fraud protection that help you get started. There are support lists for each of the following entities: email address, payment instrument, IP address, user ID and device ID. You can assign entities the status of safe, block, or watch. For details on how to manage support lists, see [Manage support lists](manage-support-lists.md).

