---
author: yvonnedeq
description: How to setup event hubs to extend Fraud Protection functionality and incorporate Fraud Protection data into an organization’s processes and workflows.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 09/11/2020
ms.topic: conceptual
search.app:
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Setup extensibility via Event Hubs

---


# Setup extensibility via Event Hubs

> [!NOTE]  
> This document provides text-based instruction and links to relevant information. If you prefer a visual video format, watch [the setup tutorial series](https://vimeo.com/showcase/7308527).

To get started, you must setup the following: 
- Setup a [Resource Group](https://docs.microsoft.com/azure/azure-resource-manager/management/manage-resource-groups-portal).
- Setup an [Event Hubs Namespace and an Event Hub](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).
- Setup an [Event Tracing subscription within Fraud Protection](https://docs.microsoft.com/dynamics365/fraud-protection/event-tracing).
	
> [!NOTE]  
> It is advised to setup a *separate* Event Hubs for each event *type* subscription. For example, you can setup an `audit-events` Event Hubs with a Fraud Protection Event Tracing subscription to send **Audit Events**,  and then setup another `latency-events` Event Hubs with a separate subscription to send **Latency Events**. You can setup both event hubs under the same namespace.  

After completing the **Setup** section, you will have the basics required to work with Fraud Protection event data. The following data flow is also setup:

![data flow](media/eventhubs/data-flow.png)

   Note that Fraud Protection sends events to Event Hubs, and we can use either **code via SDK kits** or **Power Platform** tools to work with those events from Event Hubs.

## Related topics
- [Extensibility via Event Hubs -  overview](extensibility-via-event-hubs-overview.md)
- [Working with code](extensibility-with-code.md)
- [Working with Logic Apps/Power Automate](extensibility-with-power-automate.md)
- [Working with Power BI](extensibility-with-power-bi.md)
- [Working with Power Apps](extensibility-with-power-apps.md)
- [Pricing](extensibility-pricing.md)
 
