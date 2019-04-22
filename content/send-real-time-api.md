---
author: jackwi111
description: This topic explains how you can send real-time data by using the Microsoft Dynamics 365 Fraud Protection application programming interface (API).
ms.author: v-jowigh
ms.service: crm-online
ms.date: 04/22/2019

ms.topic: conceptual
title: Send real-time data using the Dynamics 365 Fraud Protection API
---


# Send real-time data by using the Dynamics 365 Fraud Protection API

The Evaluate experience lets you use your real-time transaction data to compare Microsoft Dynamics 365 Fraud Protection with your existing fraud solution. You can send this data to the [Dynamics 365 Fraud Protection API](https://apidocs.microsoft.com/).

To accelerate the process, Microsoft provides sample code that authenticates with and calls the Dynamics 365 Fraud Protection API, adds device fingerprinting data, and shows the intended use and best practices of the API. In addition, you can use the [Dynamics 365 Fraud Protection portal](https://dfp.microsoft.com) to configure decision rules. When you send transaction data, these rules act on risk scores that are calculated by Dynamics 365 Fraud Protection. Therefore, the rules affect the fraud recommendation that is returned by the API. With minimal effort, you can implement the API to help guarantee that your product is correctly integrated.

## View the sample merchant app

Use the [Dynamics 365 Fraud Protection sample merchant app](https://go.microsoft.com/fwlink/?linkid=2085137) and the accompanying developer-oriented documentation to call Dynamics 365 Fraud Protection APIs for events that occur in your system. Ultimately, the knowledge that you gain will help you reduce fraud. The sample app also covers other API events, such as sending customer account updates, refunds, and chargebacks to the API in real time. The documentation for the sample app is linked to actual sample code whenever such links are possible. Otherwise, code samples exist directly in the documentation.
