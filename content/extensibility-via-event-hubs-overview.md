---
author: josaw1
description: This article provides an overview about how you can use Microsoft Azure Event Hubs with code software development kits (SDKs) and Microsoft Power Platform to extend the functionality of Microsoft Dynamics 365 Fraud Protection and incorporate its data into an organization's processes and workflows.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: overview
search.audienceType:
  - admin
title: Extensibility via Event Hubs

---

# Extensibility via Event Hubs

This content guides you through the process of setting up and using the *event tracing data* that is available from Microsoft Dynamics 365 Fraud Protection. This data includes, but isn't limited to, data for *audit log events*, *latency events*, and *trace events*.

Through pure-code software development kits (SDKs), you can integrate this data with your own organization's workflows, requirements for granular control, and custom needs. Additionally, you can take advantage of fast-development tools such as Azure Logic Apps, Power BI, and Power Apps for powerful automation, reports, and applications.

> [!NOTE]
> Event Hub requires additional Azure services subscriptions. Contact your Microsoft Account Executive for details. If you have Azure global administrator credentials, log into the [Azure portal](https://ms.portal.azure.com/#home) to determine available subscriptions.

This content is organized into the following main articles:

- [Set up extensibility via Event Hubs](extensibility-setup.md)	
- [Work with code](extensibility-with-code.md)
- [Work with Logic Apps or Power Automate](extensibility-with-power-automate.md)
- [Work with Power BI](extensibility-with-power-bi.md)
- [Work with Power Apps](extensibility-with-power-apps.md)


> [!NOTE]
> Only the [Set up extensibility via Event Hubs](extensibility-setup.md) article is *required*. The remaining articles are optional, depending on your organization's needs. Each article is divided into sections, so that you can skip around and review only the parts that you require. In these articles, the terms *events*, *eventing data*, and *event tracing data* are used interchangeably. 
>
> Be sure to read the notes in each article *before* you move on to another article.



[!INCLUDE[footer-include](includes/footer-banner.md)]
