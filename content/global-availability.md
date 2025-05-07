---
author: josaw1
description: This article explains the global availability of Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: article
search.audienceType:
  - admin
title: Regional availability of Dynamics 365 Fraud Protection services
---

# Regional availability of Dynamics 365 Fraud Protection services

[!include[deprecation](includes/deprecation.md)]

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

Fraud Protection is hosted from data centers that are located in the United States and Europe. Customers in other areas might experience increased latency or lack of service, and may not be fully supported by Microsoft.

The data schema that Fraud Protection uses is available at these locations:

- [Purchase protection](view-purchase-protection-schemas.md)
- [Account protection](ap-schema.md)
- [Loss prevention](view-loss-prevent-schemas.md#transactions)

The data schemas indicate the types of payment data per transaction that are typically configured for standard API calls. It's worth mentioning that these API calls are highly configurable by customers. Therefore, you can easily screen out data that could arguably be restricted in your location. As a reference, credit card information is processed only in a truncated format (only the last four digits), in accordance with standard security practices. In other words, offering truncated credit card values is optional to the customer. Customers can omit transmittal of this data to the service APIs.

As for any other artificial intelligence (AI) models, accuracy is correlated to the number of values that are computed. In general, if fewer values are provided to the AI models, the predictive capabilities of the online services won't be affected. However, the accuracy of the online services could be affected. As a user, you remain accountable for controlling the input and for using the output in accordance with local regulations.

[!INCLUDE[footer-include](includes/footer-banner.md)]
