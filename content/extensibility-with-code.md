---
author: yvonnedeq
description: How to use event hubs with code SDKs to extend Fraud Protection functionality and incorporate Fraud Protection data into an organization’s processes and workflows.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 09/16/2020
ms.topic: conceptual
search.app:
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Working with code

---

# Working with code

You can use code to:
- Test that your Event Hub is working correctly by sending test events to it. 
- Listen to and view sample events from the event tracing subscriptions you setup in Fraud Protection. 
- Work with eventing data with full control (storing events in persistent storage for auditing purposes, running custom automated scripts, etc.).

### Getting started

There are many SDK kits available for working with events from event hubs.NET, Java, Python, JavaScript,  Go, andApache Storm. You can find an extensive tutorial for sending and receiving events from Event Hubs [here](https://docs.microsoft.com/azure/event-hubs/get-started-node-send-v2). You can also find instructions for the rest of the code SDK kits from the left navigation area in Fraud Protection.

> [!NOTE]  
>  You will need to setup an **Azure Storage Account** and **Blob Container** to *receive* events. This is explained in the [tutorial](https://docs.microsoft.com/azure/event-hubs/get-started-node-send-v2). You can use the **Resource Group** and **Event Hub** you setup earlier.  

### Sample Event Hubs sender and receiver code (JavaScript)

You can find a sample of working code to send and receive events to and from Event Hubs via JavaScript [here](https://docs.microsoft.com/azure/event-hubs/event-hubs-node-get-started-send).


## Related topics
- [Extensibility via Event Hubs - Overview]( extensibility-via-event-hubs-overview.md)
- [Setup extensibility via Event Hubs](extensibility-setup.md)	
- [Working with Logic Apps/Power Automate]( extensibility-with-power-automate.md)
- [Working with Power BI]( extensibility-with-power-bi.md)
- [Working with Power Apps]( extensibility-with-power-apps.md)
- [Pricing](extensibility-pricing.md)
