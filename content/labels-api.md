---
author: josaw1
description: This article explains how the labels API enables you to send information to the virtual fraud analyst and scorecard.
ms.author: josaw
ms.date: 07/09/2020
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Labels API
ms.custom: 
---

# Labels API

The labels API enables you to send additional information to Microsoft Dynamics 365 Fraud Protection in addition to the data that informs the virtual fraud analyst and scorecard features. The labels API provides the additional knowledge for model training based on an additional set of fraud signals.  

You can use the Fraud Protection labels API to send information about [transactions](labels-api.md#transaction-purchasesignupgenericevent-details), [account or payment instrument details](labels-api.md#account-or-payment-instrument-details), and [reversals](labels-api.md#reversals). 

## Transaction (Purchase/Signup/GenericEvent) details 
- TC40/SAFE signals received 
- Fraudulent activity or account abuse identified by your review team 
- Any fraudulent transactions escalated by your customers 
- Any offline analysis (like behavior analysis or discovered connections to existing fraud cases) 
- Chargebacks/refunds received 

We recommend using the Chargeback and Refund API for providing information pertaining to chargebacks and refunds. For more information about all supported events, see <a href="https://go.microsoft.com/fwlink/?linkid=2084942" target="_blank">Dynamics 365 Fraud Protection API</a>.

## Account or payment instrument details 
- Fraudulent account or payment instrument info identified by your review team 
- Account takeover scenarios escalated by your customers 

## Reversals 
- Transaction details that update the status of reversed chargeback or fraud signals 

 


[!INCLUDE[footer-include](includes/footer-banner.md)]
