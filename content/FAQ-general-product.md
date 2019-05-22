---
author: jackwi111
description: This topic provides frequently asked product questions about Microsoft Dynamics 365 Fraud Protection.
ms.author: v-jowigh
ms.service: crm-online
ms.date: 05/22/2019

ms.topic: conceptual
title: General product FAQ
---

# General product FAQ

**Can we upload historical data to compare our results with what Dynamics 365 Fraud Protection thinks about the data before we go through the full integration process?**

Yes. We have a Diagnose experience that is designed exactly for this purpose. You upload historical data (which stays in your own merchant Azure tenant as we don’t have access to this data), and Dynamics 365 Fraud Protection will run that data through our ML and produce both a data diagnosis report and a risk diagnosis report. The data diagnosis report is designed to help you identify potential gaps or additional signals that would improve the risk score. The risk diagnosis report is designed to help you see how our ML would have performed, and to allow you to play with the risk score thresholds to understand the potential impact to your business in terms of both fraud prevention and overall profit. 

**Can we pick and choose which orders are subject to a fraud check?**

The quality of a Dynamics 365 Fraud Protection risk assessment improves with every transaction that is sent. While the decision to accept or reject a transaction is entirely up to you, we recommend that you assess all transactions to maximize the quality of the scores. 

**How does your network size compare to that of payment processors like Chase, Worldpay, and Adyen?**

While we cannot disclose the names of other customers operating within our fraud proteciton network, we have seeded it with Microsoft worldwide merchant data which covers billions of transactions with a wide variety of physical and digital goods in all major markets. 

**What is the role of manual review in this solution?**

TBD

**What role would a customer's purchase history play in the fraud models? Is the fraud engine stricter with new customers than it is with customers who have significant purchase history with our business? Would the fraud engine be more trusting of customers whose purchase behavior matches past behavior (same device, device location, IP, shipping address, etc.) and less trusting of customers whose behavior is irregular?**

TBD

**How does your device fingerprinting solution work? Is it a script I link to? Can I self-host it?**

TBD

**What type of latency guarantees do you offer?**

TBD

**What payment types do you support?**

TBD

**Does Dynamics 365 Fraud Protection provide a liability shift?**

TBD

**How does this work with PSD2?**

A: TBD

**Do you provide reason codes or an explanation for a given risk assessment score?**

TBD

**How do you obtain quality fraud labels for model training?**

TBD

**Do I need to upload chargeback data to you? How do I do that?**

TBD

**I’m an existing Dynamics 365 customer. What type of integration is available to me out of the box?**

TBD
