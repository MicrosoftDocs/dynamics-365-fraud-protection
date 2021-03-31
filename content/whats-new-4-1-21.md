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

The April 2021 release of Microsoft Dynamics 365 Fraud Protection introduces several new capabilities and enhancements. 

## External calls  

Released as a preview feature, external calls allow you to connect to APIs outside of Fraud Protection and then use the response data in your rules. For example, you can use external calls to make decisions based on third party phone or address verification services, or even your own custom scoring models. 

For more information, see [External calls](external-calls.md).

## Velocities  

Released as a preview feature, the new velocity feature allow you to define your own custom velocities to monitor the relationships and patterns between past transactions. Using this tool, you can now get the answers to questions such as:

- How much money has a user spent in the last 1 hour? 
- How many distinct payment instruments have been used from this device in the last 7 days? 
- How many times has this user attempted to login in the last 1 minute? 
 
You can then use all this information in rules to make real-time decisions. 

For more information, see [Perform velocity checks](velocities.md).

## New data upload

We have improved the data upload experience for importing historical data for purchase protection and loss prevention. The benefits of the updated feature include:

1. A centralized and unified experience which guides you to upload historical data for purchase protection and loss prevention. 
2. The ability to map data columns with attributes in any order, and an auto-mapping ability to save manual effort. 
3. Mappings which are remembered and can be reused for periodical data upload in just a few clicks. 
4. Built-in data validations which alert you about data format errors before processing. For issues detected during data processing, details are provided in text files which you can download and use for troubleshooting. 
5. The ability to upload files with or without column headers. 

For more information, see [Upload historical data for purchase protection](data-upload.md) and [Upload historical data for loss prevention](loss-prevention-data-upload.md).

## Other enhancements

### Pre-fetch assessment APIs 

Fraud Protection organizes content on a site to define its identity, help you find the information you’re looking for, and then process it meaningfully and intuitively. This process involves aligning the navigation with your mental models and the jobs to be done.

In this release, Fraud Protection introduces new groupings for assessments and features. Each assessment aligns to a category of fraud and has features which are unique to them and available as tab pages. These features are shared across multiple assessments are then grouped into **Data** and **Setting** sections:

- The **Data** section includes everything relevant for data exploration, ingress, and egress.
- The **Setting** section includes all the typical administrative and service-management related features, such as metering and user access.

This new navigational structure enables you to determine why, how, and when to use Fraud Protection.

### Redesigned home page and guided tours

To further streamline first-time and ongoing use of the portal, Fraud Protection introduces an updated experience for the home page as well as feature-specific guided tours.

The Fraud Protection home page now includes tiles for each assessment, which allow you to select tours that cover features such as creating rules and generating the first loss prevention report. Each tour guides you through the portal, explains the use cases, and provides high-level tips for getting started with the feature.

The home page also includes:

- A static list of steps for onboarding onto each assessment.
- A list of general administrative tasks and links to the user documentation.
- A link to the *Ideas portal* where you can engage with the Fraud Protection community and have an impact on the future of the Fraud Protection product by submitting and voting on new feature requests.

## Enhancement to rules 

### Clause naming

Rules are made up of clauses, each of which might express a different aspect of your fraud strategy. Fraud Protection now provides you with the option to give each clause a unique name. Clause names are surfaced not only in the rule itself but are also exposed in the API response for an assessment. 

This means that for a given transaction, in addition to providing the rule that triggered a decision, Fraud Protection now provides the name of the specific clause that triggered the decision.  

### Rule evaluation behavior setting

Fraud Protection has added a new setting called *Rule evaluation behavior*. This setting provides you with two distinct options for how they’d like their rules to be evaluated. If no clause within an individual rule returns a decision, this setting allows you to specify whether you’d like the transaction to be approved or go to the next rule to be evaluated. 

A new section called *ruleEvaluations* is now included in the assessment API response. This section provides a list of each rule and clause that was evaluated for a transaction. 

## Dynamics 365 Commerce customer offer

Starting October 2020, a limited capacity of Fraud Protection is included in the Microsoft Dynamics 365 Commerce license. Commerce customers can now use Fraud Protection for no extra charge, up to the limits specified below:

- **Purchase protection** - Up to 2,000 assessments per month.
- **Account protection** - Up to 20,000 assessments per month. 
- **Loss prevention** - Up to 8,000 transactions per month. 

If their usage requires higher limits, Commerce customers have the option of purchasing additional Fraud Protection add-ons. This offer makes it easier for all existing and new Commerce customers to evaluate how Fraud Protection capabilities can help protect their organizations against fraudulent purchases, fake accounts creation, suspicious logins, and employee fraud in the form of inappropriate discounts or returns. 

To start using Fraud Protection if you are already an existing Commerce customer, visit the [Fraud Protection portal](https://dfp.microsoft.com/), sign in with tenant global administrator credentials, and complete a one-time setup for your environment.



[!INCLUDE[footer-include](includes/footer-banner.md)]
