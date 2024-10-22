---
author: josaw1
description: This article explains how to use event hubs with code software development kits (SDKs) to extend the functionality of Microsoft Dynamics 365 Fraud Protection and incorporate its data into an organization's processes and workflows.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Work with code

---

# Work with code

You can use code for the following purposes:

- Test that your event hub is working correctly by sending test events to it.
- Listen to and view sample events from the event tracing subscriptions that you set up in Microsoft Dynamics 365 Fraud Protection.
- Have full control as you work with eventing data (for example, store events in persistent storage for auditing purposes and run custom automated scripts).

## Getting started

There are many software development kits (SDKs) available for working with events [from Event Hubs in .NET, Java, Python, JavaScript, Go, and Apache Storm](/azure/event-hubs/sdks). 

For an extensive tutorial about how to send and receive events from Azure Event Hubs, see [Send events to or receive events from event hubs by using JavaScript (azure/event-hubs version 5)](/azure/event-hubs/get-started-node-send-v2). You can also access instructions for the remaining code SDKs from the left navigation in Fraud Protection.

> [!NOTE]
> To *receive* events, you must set up an Azure storage account and blob container. This process is explained in the previously mentioned [tutorial](/azure/event-hubs/get-started-node-send-v2). You can use the resource group and event hub that you set up earlier.

## Sample Event Hubs sender and receiver code (JavaScript)

For a sample of working code that sends and receives events to and from Event Hubs via JavaScript, see [Send events to or receive events from event hubs by using JavaScript (azure/event-hubs version 5)](/azure/event-hubs/event-hubs-node-get-started-send).

## Related articles

- [Extensibility via Event Hubs](extensibility-via-event-hubs-overview.md)
- [Set up extensibility via Event Hubs](extensibility-setup.md)	
- [Work with Logic Apps or Power Automate](extensibility-with-power-automate.md)
- [Work with Power BI](extensibility-with-power-bi.md)
- [Work with Power Apps](extensibility-with-power-apps.md)


[!INCLUDE[footer-include](includes/footer-banner.md)]
