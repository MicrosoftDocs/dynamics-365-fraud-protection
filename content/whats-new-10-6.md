---
author: yvonnedeq
description: This topic explains what's new in the Microsoft Dynamics 365 Fraud Protection October 2020 release.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 10/23/2020
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: What's new in Dynamics 365 Fraud Protection October 2020 release

---

# What's new in Dynamics 365 Fraud Protection October 2020 release

The October 2020 release of Microsoft Dynamics 365 Fraud Protection (Fraud Protection) introduces several new capabilities and enhancements. 

## Manual review (preview) 

Released as a preview in this version, manual review is a new capability that introduces the ability for Fraud Protection customers to augment their fraud workflows with manual review capabilities (also known as *case review*.) This allows customers to author rules to identify  transactions which might benefit from further human review, and then place the rules into a queue to facilitate and amplify the review process.

Key components of the preview version of the manual review capabilities include:

- **Queue management** - Customers can create workflows that route fraudulent transactions to different queues for manual review based on specific criteria. 
  
- **Review dashboard** -  Customers can review a transaction and analyze the fraud pattern efficiently.
  
- **Create customized actions** - Customers can dynamically create remedy actions, such as decisions and fraud labeling, that can be applied for tracking and analysis purposes.
  
- **A customized performance dashboard** - Customers have access to a dashboard that displays a list of reviewed orders, fraudulent orders, the false positive rate, and so on, calculated by the team or analyst, with daily and monthly views.

## Enhanced user experiences

### Streamlined site navigation
Fraud Protection organizes content on a site to define its identity, help customers find the information they’re looking for, and then process it meaningfully and intuitively. This process involves aligning the navigation with the customers' mental models and jobs to be done. 

In this release, Fraud Protection introduces new groupings for assessments and features. Each assessment aligns to a category of fraud and has features which are unique to them and available as tab pages. Features that are shared across multiple assessments are then grouped into **Data** and **Settings** sections: 

- The **Data** section includes everything relevant for data exploration, ingress, and egress. 

- The **Settings** section includes all the typical administrative and service-management related features, such as metering and user access. 

This new navigational structure enables customers to determine why, how, and when to use Fraud Protection.

### Redesigned home page and guided tours

To further streamline first-time and ongoing use of the portal, Fraud Protection introduces an updated experience for the home page as well as feature-specific guided tours. 

The Fraud Protection home page now includes tiles for each assessment, which allow customers to select tours that cover features such as creating rules and generating the first loss prevention report. Each tour guides customers through the portal, explains the use cases, and provides high-level tips for getting started with the feature. 

The home page also includes:

- A static list of steps for onboarding onto each assessment. 
- A list of general administrative tasks and links to the user documentation. 
- A link to the *Ideas portal* where customers can engage with the Fraud Protection community and have an impact on the future of the Fraud Protection product by submitting and voting on new feature requests.

## Enhancement to rules 

### Clause naming

Rules are made up of clauses, each of which might express a different aspect of a customer's fraud strategy. Fraud Protection now provides the option for customers to give each clause a unique name. Clause names are surfaced not only in the rule itself, but are also exposed in the API response for an assessment. 

This means that for a given transaction, in addition to providing the rule that triggered a decision, Fraud Protection now provides the name of the specific clause that triggered the decision.  

### Rule evaluation behavior setting

Fraud Protection has added a new setting called *Rule evaluation behavior*. This setting provides customers with two distinct options for how they’d like their rules to be evaluated. If no clause within an individual rule returns a decision, this setting allows customers to specify whether they’d like the transaction to be approved or go to the next rule to be evaluated. 

A new section called *ruleEvaluations* is now included in the assessment API response. This section provides a list of each rule and clause that was evaluated for a transaction. 

## Dynamics 365 Commerce customer offer

Starting October 2020, a limited capacity of Fraud Protection is included in the Microsoft Dynamics 365 Commerce license. Commerce customers can now use Fraud Protection for no extra charge, up to the limits specified below:

- **Purchase protection** - Up to 2,000 assessments per month.
- **Account protection** - Up to 20,000 assessments per month. 
- **Loss prevention** - Up to 8,000 transactions per month. 

If their usage requires higher limits, Commerce customers have the option of purchasing additional Fraud Protection add-ons. This offer makes it easier for all existing and new Commerce customers to evaluate how Fraud Protection capabilities can help protect their organizations against fraudulent purchases, fake accounts creation, suspicious log-ins, and employee fraud in the form of inappropriate discounts or returns. 

To start using Fraud Protection if you are an existing Commerce customer, visit the [Fraud Protection portal](https://dfp.microsoft.com/), sign in with tenant global administrator credentials, and complete a one-time setup for your environment.



[!INCLUDE[footer-include](includes/footer-banner.md)]
