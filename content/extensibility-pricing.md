---
author: yvonnedeq
description: Information about official and current pricing options.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 09/11/2020
ms.topic: conceptual
search.app:
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Pricing

---
# Pricing 

Pricing varies based on your individual needs and usages, so it is flexible based on which tools you choose to use. 

You can find official and current pricing options here:
- [Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/) - A tool to receive and send events.
- [Storage Accounts](https://azure.microsoft.com/pricing/details/storage/) -  A tool to work with code SDK’s.
- [Power Apps](https://powerapps.microsoft.com/pricing/) -  A quick, low-code application development tool for fast, powerful apps.
- [Logic Apps](https://azure.microsoft.com/pricing/details/logic-apps/) - A tool to parse Fraud Protection events to store in CDS and if you want to quickly create automated workflows. 

   If you need a tool for setting limits and restrictions for Power Automate, you can find it [here](https://docs.microsoft.com/power-automate/limits-and-config). 
- [Power Automate](https://flow.microsoft.com/pricing/) - A tool that is similar to Logic Apps but packaged and priced differently. 

   If you need a tool for setting limits and restrictions for **Power Automate**, you can find it [here](https://docs.microsoft.com/power-automate/limits-and-config). Consider your team size and technical requirements when deciding between **Power Automate** and **Logic Apps**. Larger organizations may prefer the **Logic Apps** pricing plan as opposed to the **Power Automate** per-user pricing plan.
   
- [Power BI](https://powerbi.microsoft.com/pricing/) - A tool to create effective data visualizations with Fraud Protection data.
- [CDS Database Storage Add-ons](https://docs.microsoft.com/power-platform/admin/powerapps-flow-licensing-faq#add-ons).

### Sample pricing breakdown

The following is a sample pricing breakdown of a certain use case of **Event Hubs (Standard Tier)** + **Logic Apps** + **CDS** + **Power Apps** to  work with **Latency Events**. It simulates an organization that processes on average 500,000 transactions per month and records latency measurements every 1 minute, producing ~1,000,000 events. The **Logic App** used contains 3 **Actions** and 2 **Standard Connectors**.

| Service/Tool | Pricing for 1 Month |
|--------------|---------------------|
| Event Hubs   | $21.93             |
| Logic Apps   | $112.00             |
| CDS          | $40.00              |
| Power Apps   | $10.00              |
| Total        | $183.98             |

#### Cost calculator
For a pricing breakdown specific to your own organization’s needs and usages, use the following [cost calculator](https://azure.microsoft.com/pricing/calculator/).

## Related topics
- [Extensibility via Event Hubs - overview]( extensibility-via-event-hubs-overview.md)
- [Setup extensibility via Event Hubs](extensibility-setup.md)	
- [Working with code](extensibility-with-code.md)
- [Working with Logic Apps/Power Automate]( extensibility-with-power-automate.md)
- [Working with Power BI]( extensibility-with-power-bi.md)
- [Working with Power Apps]( extensibility-with-power-apps.md)

