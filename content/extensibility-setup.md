---
author: yvonnedeq
description: This topic provides information about how to set up event hubs to extend the functionality of Microsoft Dynamics 365 Fraud Protection and incorporate Fraud Protection data into an organization's processes and workflows.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 10/23/2020
ms.topic: conceptual
search.app:
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Set up extensibility via Event Hubs

---


# Set up extensibility via Event Hubs

> [!NOTE]
> This topic provides text-based instructions and links to relevant information. If you prefer a visual video format, watch the [setup tutorial series](https://vimeo.com/showcase/7308527).

To get started, you must set up the following items:

- A [resource group](https://docs.microsoft.com/azure/azure-resource-manager/management/manage-resource-groups-portal)
- A [Microsoft Azure Event Hubs namespace and an event hub](https://docs.microsoft.com/azure/event-hubs/event-hubs-create)
- An [event tracing subscription in Dynamics 365 Fraud Protection](https://docs.microsoft.com/dynamics365/fraud-protection/event-tracing)
	
> [!NOTE]
> We recommend that you set up a *separate* event hub for the subscription for each event *type*. For example, you can set up an **audit-events** event hub that has a Fraud Protection event tracing subscription to send *audit events*. Then set up a **latency-events** event hub that has a separate subscription to send *latency events*. You can set up both event hubs under the same namespace.

After you complete the setup that is described in this topic, you will have the basics that are required to work with Fraud Protection event data. The following data flow is also set up.

![Data flow](media/eventhubs/data-flow.png)

Fraud Protection produces real-time events and sends them to your Event Hubs instance. They are then consumed by event receivers such as Power Automate, Logic Apps, etc.

To work with these events from Event Hubs, you can use either code via software development kits (SDKs) or Microsoft Power Platform tools.

## Related topics

- [Extensibility via Event Hubs](extensibility-via-event-hubs-overview.md)
- [Work with code](extensibility-with-code.md)
- [Work with Logic Apps or Power Automate](extensibility-with-power-automate.md)
- [Work with Power BI](extensibility-with-power-bi.md)
- [Work with Power Apps](extensibility-with-power-apps.md)
- [Pricing](extensibility-pricing.md)
