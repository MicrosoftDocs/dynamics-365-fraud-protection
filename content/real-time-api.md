---
author: jackwi111
description: Explore data using APIs
ms.author: v-jowigh
ms.date: 02/25/2019
ms.service:
 - d365-fraud-protection
ms.topic: conceptual
title: Explore data using APIs
---


# Explore data using APIs

The *Evaluate* experience enables you to use your real-time transactional traffic to compare Dynamics 365 Fraud Protection with your incumbent fraud solution. To ingest your real-time transaction data, Dynamics 365 Fraud Protection provides an event API. For fast ramp-up, we provide sample code that calls the risk event APIs, adds device fingerprinting tags, and enables you to configure decision rules in the rules engine. These rules can consume a risk score evaluated by the risk model in the fraud protection network. With minimal effort, you can implement Dynamics 365 Fraud Protection APIs to ensure your product is properly integrated. 

Using the following [API examples](https://github.com/Microsoft/Dynamics-365-Fraud-Protection-Samples), you can inform Dynamics 365 Fraud Protection of events that happen in your system. Ultimately, this knowledge helps you reduce fraud. The examples also cover the other API calls like sending account updates in through the API in real time and sending refunds and chargebacks to through the API.

These documents are largely based on a sample application developed to demonstrate how you can integrate your system with Dynamics 365 Fraud Protection. In general, the documents link to actual sample application code, where possible; otherwise, code samples exist directly in the documentation.

**Track purchases**
- Make a purchase - Approved purchase flow
- Make a purchase - Handle Dynamics 365 Fraud Protection purchase response
- Make a purchase - Rejected purchase flow
- Make a purchase - Existing user
- Make a purchase - Guest user

**Refunds and Chargebacks**
- Record a refund
- Record a chargeback

## View sample implementation
