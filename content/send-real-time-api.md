---
author: jackwi111
description: Send real-time data using the Dynamics 365 Fraud Protection API
ms.author: v-jowigh
ms.date: 02/25/2019
ms.service:
 - d365-fraud-protection
ms.topic: conceptual
title: Send real-time data using the Dynamics 365 Fraud Protection API
---


# Send real-time data using the Dynamics 365 Fraud Protection API

The Evaluate experience enables you to use your real-time transaction data to compare Dynamics 365 Fraud Protection with your existing fraud solution. You can send this data to the [Dynamics 365 Fraud  Protection API](https://go.microsoft.com/fwlink/?linkid=2084942). 

To accelerate the process, we provide sample code that authenticates with and calls the Dynamics 365 Fraud Protection API, adds device fingerprinting data, and shows the intended use and best practices of the API. In addition, you can use the [Dynamics 365 Fraud Protection portal](https://dfp.microsoft.com) to configure decision rules. When you send transaction data, these rules act on risk scores calculated by Dynamics 365 Fraud Protection. Consequently, the rules affect the fraud recommendation returned by the API. With minimal effort, you can implement the API to ensure your product is properly integrated.

## View sample merchant app

Use the [Dynamics 365 Fraud Protection sample merchant app](https://go.microsoft.com/fwlink/?linkid=2085137), and accompanying developer-oriented documentation, to call Dynamics 365 Fraud Protection APIs for events that happen in your system. Ultimately, this knowledge helps you reduce fraud. The sample app also covers other API events like sending customer account updates, refunds, and chargebacks in real time to the API. In general, the sample app documents link to actual sample code, where possible; otherwise, code samples exist directly in the documentation.
