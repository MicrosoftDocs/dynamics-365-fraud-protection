---
author: yvonnedeq
description: This topic provides information about official and current pricing options.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 10/08/2020
ms.topic: conceptual
search.app:
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Pricing

---
# Pricing

Pricing is based on your individual requirements and usage. Therefore, it's flexible and depends on the tools that you choose to use.

Here is a list of links to official and current pricing options for the various tools:

- [Microsoft Azure Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/) – A tool that lets you receive and send events.
- [Azure storage accounts](https://azure.microsoft.com/pricing/details/storage/) – A tool that lets you work with code software development kits (SDKs).
- [Power Apps](https://powerapps.microsoft.com/pricing/) – A quick, low-code application development tool for fast, powerful apps.
- [Azure Logic Apps](https://azure.microsoft.com/pricing/details/logic-apps/) – A tool that lets you parse Dynamics 365 Fraud Protection events so that the data can be stored in Common Data Service, and that lets you quickly create automated workflows.
- [Power Automate](https://flow.microsoft.com/pricing/) – A tool that is similar to Logic Apps, but that is packaged and priced differently.

    If you require a tool that lets you set limits and restrictions for Power Automate, see [Limits and configuration in Power Automate](https://docs.microsoft.com/power-automate/limits-and-config). When you're trying to decide between Logic Apps and Power Automate, consider the size of your team and your technical requirements. Larger organizations might prefer the Logic Apps pricing plan to the per-user pricing plan for Power Automate.

- [Power BI](https://powerbi.microsoft.com/pricing/) – A tool that lets you create effective data visualizations by using Fraud Protection data.
- [Common Data Service database storage add-ons](https://docs.microsoft.com/power-platform/admin/powerapps-flow-licensing-faq#add-ons)

## Sample pricing breakdown

The following table shows a sample pricing breakdown for a specific use case where Event Hubs (Standard Tier), Logic Apps, Common Data Service, and Power Apps are used to work with latency events. This sample simulates an organization that processes an average of 500,000 transactions per month, records latency measurements every minute, and therefore produces approximately 1,000,000 events. The logic app that is used contains three actions and two standard connectors.

| Service/tool        | Pricing for one month |
|---------------------|-----------------------|
| Event Hubs          | $21.93                |
| Logic Apps          | $112.00               |
| Common Data Service | $40.00                |
| Power Apps          | $10.00                |
| **Total**           | **$183.93**           |

### Cost calculator

For a pricing breakdown that is specific to your organization's requirements and usage, use [this cost calculator](https://azure.microsoft.com/pricing/calculator/).

## Related topics

- [Extensibility via Event Hubs](extensibility-via-event-hubs-overview.md)
- [Set up extensibility via Event Hubs](extensibility-setup.md)	
- [Work with code](extensibility-with-code.md)
- [Work with Logic Apps or Power Automate](extensibility-with-power-automate.md)
- [Work with Power BI](extensibility-with-power-bi.md)
- [Work with Power Apps](extensibility-with-power-apps.md)
