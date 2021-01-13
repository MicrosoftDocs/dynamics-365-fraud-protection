---
author: yvonnedeq
description: This topic explains the global availability of Microsoft Dynamics 365 Fraud Protection.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 10/23/2020
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Regional availability of Fraud Protection services
---

# Regional availability of Fraud Protection services

Microsoft Dynamics 365 Fraud Protection provides the English, French, German, Brazilian Portuguese, Italian, Spanish, and Dutch languages, and is currently supported in the following regions:

- United States
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

- United Kingdom 

Customers in other areas might experience increased latency or lack of service, and can't be fully supported by Microsoft.

## Loss prevention

The following information is meant to help you with your assessment of adequacy as you plan for future deployments and use of Fraud Protection in India.

As is fully described in the dashboard that covers [geographical availability for Dynamics 365](https://dynamics.microsoft.com/geographic-availability/), Fraud Protection is hosted from data centers that are located in the United States and Europe. Therefore, for services that are sold in India, customer data is processed and stored in either the United States or Europe, depending on capacity availability. Currently, the online service isn't hosted in Indian data centers. Although Microsoft plans to address geo location, so that it can offer Fraud Protection that is primarily hosted from its data centers in India, this configuration isn't currently offered.

The data schema that Fraud Protection uses is available in Microsoft technical documentation. You can find this documentation in the following places:

- [Purchase protection](https://docs.microsoft.com/dynamics365/fraud-protection/schema-int)
- [Account creation](https://docs.microsoft.com/dynamics365/fraud-protection/labels-schema)
- [Account protection](https://docs.microsoft.com/dynamics365/fraud-protection/new-ap-schema)
- [Loss prevention](https://docs.microsoft.com/dynamics365/fraud-protection/view-loss-prevent-schemas#transactions)

The data schemas indicate the types of payment data per transaction that are typically configured for standard API calls. It's worth mentioning that these API calls are highly configurable by customers. Therefore, you can easily screen out data that could arguably be restricted in your location. As a reference, credit card information is processed only in a truncated format (only the last four digits), in accordance with standard security practices. In other words, offering truncated credit card values is optional to the customer. Customers can omit transmittal of this data to the service APIs.

As for any other artificial intelligence (AI) models, accuracy is correlated to the number of values that are computed. In general, if fewer values are provided to the AI models, the predictive capabilities of the online services won't be affected. However, the accuracy of the online services could be affected. As a user, you remain accountable for controlling the input and for using the output in accordance with local regulations.

### Disclaimer

The purpose of this document is to inform the reader, not to provide legal advice. Readers are advised to consult with both technical and legal advisers in assessing compliance with Indian Laws.
