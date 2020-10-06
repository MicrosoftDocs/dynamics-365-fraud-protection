---
author: yvonnedeq
description: This topic explains what's new in the Microsoft Dynamics 365 Fraud Protection October 2020 release.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 10/06/2020

ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: What's new in Dynamics 365 Fraud Protection October 2020 release

---

# What's new in Dynamics 365 Fraud Protection October 2020 release (placeholder)

The October 2020 release of Microsoft Dynamics 365 Fraud Protection introduces several new capabilities and enhancements. 

## Manual review (preview) 

Released as a preview, manual review is a new capability that introduces the ability for Fraud Protection customers to augment their fraud workflows with manual review capabilities, also known as *case review*. This feature allows customers to  author rules to identify  transactions that may benefit from further further human review, and then place them into a queue to facilitate and amplify the review process.

Key components of the preview version of the manual review feature include:

- **Queue management** 

  Customers can create workflows that route fraudulent transactions to different queues for manual review based on specific criteria. 
  
- **Review dashboard** 

  Customers can review a transaction and analyze the fraud pattern efficiently.
  
- **Create customized actions** 

  Customers can dynamically create remedy actions such as decisions and fraud labeling that can be applied for tracking and analysis purposes.
  
- **A customized performance dashboard** 

  A dashboard capable of displaying a list of reviewed orders, fraud orders, the false positive rate, and so on, calculated by the team or analyst, with daily and monthly views.

## Enhanced user experiences

### Enhanced workflow navigation and homepage

The way we organize content on a site defines its identity and helps you find the information you’re looking for and then process it meaningfully and intuitively. This involves aligning the navigation with your mental models and jobs to be done. To that extent we have introduced new groupings for our assessments and features. Each assessment aligns to a category of fraud and has features which are unique to them easily available as tabs underneath. Features which are shared across multiple assessments are then grouped under Data and Settings. Under Data you will find everything relevant for data exploration, ingress, and egress. And under Settings you will find all of the typical admin and service-management related features such as metering and user access. With this new navigational structure we hope to enable you enables you to ascertain why, how, and when to use our product.

### Guided tours

To further streamline first-time and ongoing use of the portal we have introduced an updated experience for the homepage as well as feature-specific guided tours. The new homepage has tiles for each assessment and allows you to select tours that cover features such as creating rules, generating your first loss prevention report, so on and so forth. Each tour will guide you through the portal and explain the use cases and high-level tips to getting started with that feature. The new homepage will then also include a static list of steps for onboarding onto each assessment as well as general admin tasks. Lastly, also provided on the homepage are links to the documentation as well as the ideas portal where you can engage with the Dynamics 365 Fraud Protection community to make your mark on the product by submitting and voting on new feature requests.

## Enhancement to rules 

### Clause naming

Rules are made up of clauses, each of which may express a different aspect of a customer's fraud strategy. Fraud Protection now provides the option for customers to give each clause a unique name. Clause names are surfaced not only in the rule itself, but are also exposed in the API response for an assessment. 

This means that for a given transaction, in addition to providing the rule that triggered a decision, Fraud Protection now provides the name of the specific clause that triggered the decision.  

### New rule evaluation behavior

Fraud Protection introduces a new setting which provides customers with two distinct options for how they’d like their rules to be evaluated. 

- If no clauses within an individual rule returns a decision, this setting allows customers to specify whether they’d like the transaction to be approved, or if the they’d like to go to the next rule to be evaluated. 
- A new section in the assessment API response called *ruleEvaluations* which provides a list of each rule and clause that was evaluated for a transaction. 

## Dynamics 365 Commerce customer offer

Starting October 01, 2020, a limited capacity of Fraud Protection is included in the Microsoft Dynamics 365 Commerce license. Commerce customers are now able to use Fraud Protection for no extra charge up to the limits specified below:

- **Purchase protection:** 2,000 assessments per month.
- **Account protection:** 20,000 assessments per month. 
- **Loss prevention:** 8,000 transactions per month. 

If their usage requires higher limits, Commerce customers have the option of purchasing additional Fraud Protection add-ons. 

This makes it easier for all existing and new Commerce customers to evaluate how Fraud Protection capabilities can help protect their organizations against fraudulent purchases, fake accounts creation, suspicious log-ins, and employee fraud in the form of inappropriate discounts or returns. 

To start using Fraud Protection in just a few minutes, Commerce customers can visit the [product portal](https://dfp.microsoft.com/), sign in with tenant global administrator credentials, and complete a one-time setup for their environment.

