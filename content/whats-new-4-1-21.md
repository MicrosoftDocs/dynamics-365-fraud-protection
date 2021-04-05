---
author: yvonnedeq
description: This topic explains what's new in the Microsoft Dynamics 365 Fraud Protection April 2021 release.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 04/05/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: What's new in Dynamics 365 Fraud Protection April 2021 release

---

# What's new in Dynamics 365 Fraud Protection April 2021 release

[!include [banner](includes/preview-banner.md)]

The April 2021 release of Microsoft Dynamics 365 Fraud Protection (Fraud Protection) introduces several new capabilities and enhancements. 

## External calls  

Until  now, using the Fraud Protection rule engine, merchants could make real-time decisions based only on the data available within Fraud Protection. While we have been able to use this data to help omnichannel merchants protect their business from fraud, it isn’t always enough. Sometimes merchants need additional signals from data sources outside of Fraud Protection to inform their decisions. Some merchants have partnered with other third-party information providers for additional data enrichment such as address verification and phone reputation. We’ve seen other merchants utilize scores from their own in-house models, that are tailored to their business. All these inputs are important for merchant to make fully informed decisions regarding their business.

Our new external calls feature, currently released in preview, allows merchants to connect to APIs outside of Fraud Protection to help determine which events should be approved or rejected. We do not limit merchants to a small subset of providers we want them to do business with. Instead, merchants will be able to bring in data from essentially any API endpoint, ensuring they have context and flexibility needed at the point of decision. We’ve also worked to make this process as simple and intuitive as possible, allowing users to connect to these APIs, and test that they work as expected, all in under 1 minute.

For more information, see [External calls](external-calls.md).

## Velocities  

Released as a preview feature, the new velocity feature allows merchants to define their own custom velocities to monitor the relationships and patterns between past transactions. 

Would you consider it suspicious if someone buys one exercise bike? Probably not. But what about 15 exercise bikes? And what if they used 20 different payment methods, 8 of which were rejected? These activities seems a little more suspicious, and may be a good indicator that they are in possession of stolen payment information. Therefore, monitoring the relationships and patterns between current and past transactions is an essential in determining the riskiness of any given event. 

The Fraud Protection machine learning (ML) score already considers a very wide range of velocities across multiple entities (such as IP, device, location , user email, time, etc.). The new velocity features now allow merchants to explicitly test for the historical patterns of an individual or entity, such as an email address, credit card information, or IP address, and then uses these patterns in real-time explicit decision making. 

Here are some examples of how velocity checks can be used to assess risk and make decisions: 

-	Block transactions coming from an account that has already purchased over $1000 of goods in the last 24 hours. 
-	Block transactions coming from users who have used more than 10 different credit cards in the last 7 days.
-	Review transactions if more than 10 users have attempted to login from the same device in the last 1 hour.

Some behaviors are always suspicious regardless of the business, while others may be suspicious for one business, but not another. For example, while 2-6 transaction a month at a grocery store may be expected, the same number of transactions from a luxury car dealer may be more alarming. 

Velocities are an important tool for any fraud protection service, but its effectiveness depends on being able to customize it to your business. Fraud Protection’s new velocity feature focuses on providing merchants with the ability to fully customize their velocities; all the way from which attributes to monitor, to the timeframe over which they monitor them, to which thresholds they want to set. 

For more information, see [Perform velocity checks](velocities.md).

## Enhanced data upload

We have improved the data upload experience for importing historical data for purchase protection and loss prevention. The benefits of the updated feature include:

- A centralized and unified experience that guides you to upload historical data for purchase protection and loss prevention. 
- The ability to map data columns with attributes in any order, and an auto-mapping ability to save manual effort. 
- Mappings which are remembered and can be reused for periodical data upload in just a few clicks. 
- Built-in data validations that alert you about data format errors before processing. For issues detected during data processing, details are provided in text files, which you can download and use for troubleshooting. 
- The ability to upload files with or without column headers. 

For more information, see [Upload historical data for purchase protection](data-upload.md) and [Upload historical data for loss prevention](loss-prevention-data-upload.md).

## Fraud Protection achieves PCI Compliance

The Payment Card Industry - Data Security Standards (PCI DSS) is a global information security standard designed to reduce credit card fraud. Customers can leverage Azure’s PCI DSS certification to minimize their compliance burden and pursue their own PCI DSS certification. 

PCI certifications provide solid guardrails and increased trust to sell our services to both existing and potential customers who handle credit card data. With the recently concluded audit cycle, Fraud Protection is now successfully certified for PCI DSS Compliance.

## Expandability of transaction trust knowledge

Fraud Protection's transaction acceptance booster (TAB) feature allows customers to send contextual data about a transaction, also known as transaction trust knowledge, to issuing banks. This contextual data helps the issuing banks make a more informed assessment and results in more accurate decisions by issuing banks. 

In this release we have enabled expandability that allows customers to send additional raw data beyond the standard format.

For more information, see [Boost bank acceptance rates](transaction-acceptance-booster.md).


## Dynamics 365: 2021 release wave 1 plan

Wondering about upcoming and recently released capabilities in any of our business apps or platform?

Check out the [Dynamics 365: 2021 release wave 1 plan](https://docs.microsoft.com/dynamics365-release-plan/2021wave1/). We've captured all the details, end to end, top to bottom, in a single document that you can use for planning.



[!INCLUDE[footer-include](includes/footer-banner.md)]
