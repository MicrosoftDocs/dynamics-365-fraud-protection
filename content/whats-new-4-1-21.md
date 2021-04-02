---
author: yvonnedeq
description: This topic explains what's new in the Microsoft Dynamics 365 Fraud Protection April 2021 release.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 04/01/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: What's new in Dynamics 365 Fraud Protection April 2021 release

---

# What's new in Dynamics 365 Fraud Protection April 2021 release

[!include [banner](includes/preview-banner.md)]

The April 2021 release of Microsoft Dynamics 365 Fraud Protection introduces several new capabilities and enhancements. 

## External calls  

Released as a preview feature, external calls allow you to connect to APIs outside of Fraud Protection and then use the response data in your rules. For example, you can use external calls to make decisions based on third-party phone or address verification services, or even your own custom scoring models. 

For more information, see [External calls](external-calls.md).

## Velocities  

Released as a preview feature, the new velocity feature allows you to define your own custom velocities to monitor the relationships and patterns between past transactions. Using this tool, you can now get the answers to questions such as:

- How much money has a user spent in the last 1 hour? 
- How many distinct payment instruments have been used from this device in the last 7 days? 
- How many times has this user attempted to sign in in the last 1 minute? 
 
You can then use this information in rules to make real-time decisions. 

For more information, see [Perform velocity checks](velocities.md).

## Enhanced data upload

We have improved the data upload experience for importing historical data for purchase protection and loss prevention. The benefits of the updated feature include:

- A centralized and unified experience that guides you to upload historical data for purchase protection and loss prevention. 
- The ability to map data columns with attributes in any order, and an auto-mapping ability to save manual effort. 
- Mappings which are remembered and can be reused for periodical data upload in just a few clicks. 
- Built-in data validations that alert you about data format errors before processing. For issues detected during data processing, details are provided in text files, which you can download and use for troubleshooting. 
- The ability to upload files with or without column headers. 

For more information, see [Upload historical data for purchase protection](data-upload.md) and [Upload historical data for loss prevention](loss-prevention-data-upload.md).

## Dynamics 365: 2021 release wave 1 plan

Wondering about upcoming and recently released capabilities in any of our business apps or platform?

Check out the [Dynamics 365: 2021 release wave 1 plan](https://docs.microsoft.com/dynamics365-release-plan/2021wave1/). We've captured all the details, end to end, top to bottom, in a single document that you can use for planning.



[!INCLUDE[footer-include](includes/footer-banner.md)]
