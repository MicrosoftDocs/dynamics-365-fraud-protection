---
author: yvonnedeq
description: This topic explains the global availability of Microsoft Dynamics 365 Fraud Protection.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 07/13/2020
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Regional availability of Fraud Protection services
---

# Regional availability of Fraud Protection services

Microsoft Dynamics 365 Fraud Protection provides English, French, German, Brazilian Portuguese, Italian, Spanish, and Dutch languages and is currently supported in the following regions. 
- US 
- Canada
- Western Europe (excluding Switzerland) 
    - Austria 
    - Belgium 
    - Denmark 
    - Finland 
    - France
    - Ireland 
    - Italy 
    - Netherlands 
    - Norway 
    - Portugal 
    - Spain 
    - Sweden 
- UK 

Customers in other areas may experience increased latency or lack of service, and cannot be fully supported by Microsoft. 

## Loss Prevention

As you plan for future deployments and use of Fraud Protection in India, the following information is meant to equip you with some tools that will assist your assessment of adequacy.  
 
Fraud Protection is hosted from data centers located in the US and Europe; this is fully described in our dashboard covering [Geographical Availability for Dynamics 365](https://dynamics.microsoft.com/en-us/geographic-availability/). This means that for services sold in India, customer data is processed and stored in the United States or Europe, depending on capacity availability. Currently, the online service is not hosted in our Indian data centers. Although we plan to address geo-location to offer Fraud Protection primarily hosted from our data centers in India, this is not a configuration offered today. 
 
The data schema used by Fraud Protection is available in our technical documentation, which you can find in the following locations:
 
- [Purchase Protection](https://docs.microsoft.com/en-us/dynamics365/fraud-protection/schema-int) 
- [Account Creation](https://docs.microsoft.com/en-us/dynamics365/fraud-protection/labels-schema) 
- [Account Protection](https://docs.microsoft.com/en-us/dynamics365/fraud-protection/new-ap-schema)
- [Loss Prevention](https://docs.microsoft.com/en-us/dynamics365/fraud-protection/view-loss-prevent-schemas#transactions) 
 
The data schemas indicate the types of payment data per transaction that are typically configured for standard API calls. It is worth mentioning that these API calls are highly configurable by customers, so you can easily screen out data that could be arguably restricted in your location. As a reference, credit card information is only processed in a truncated format (only last four digits) following standard security practices. In other words, offering truncated credit card values is optional to the customer. Customers have the ability to omit transmittals of these data to the service APIs. 
 
As with any other AI models, accuracy is correlated to the number of values computed. Fewer values provided to the AI models will not affect the predictive capabilities of the online services in general, but it could affect its accuracy. As a user, you remain accountable for controlling the input and using the output in accordance with local regulations. 
  
[!DISCLAIMER]
> The purpose of this document is to inform the reader, not to provide legal advice. Readers are advised to consult with both technical and legal advisers in assessing compliance with Indian Laws.

