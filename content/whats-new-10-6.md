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

The October 2020 release of Dynamics 365  Fraud Product introduces several new capabilities and enhancements. 

## Manual Review (preview) 

Manual Review (preview)is a new capability  that introduces the ability for Dynamic Fraud Protection customers to augment their fraud workflows with manual review capabilities (also known as case review) .  This provides the customer with the ability to  author rules to identify  transactions that can benefit from further  further human review, and place them into a queue to facilitate and amplify  the review process.

Key components of this Manual Review (preview) feature include:

- Queue Management. Ability to create workflows so that fraudulent transactions can be routed to different queues for manual review based on specific criteria.
- Review Dashboard: Ability to review the transaction and analyze fraud pattern in an efficient way.
- Customized Action Creation:  Ability to create remedy actions dynamically, such as decisions, fraud labeling, that are applied for tracking and analysis purposes
- Customized Performance Dashboard:  Ability to display dashboard of reviewed orders, fraud orders, false positive rate and so on, calculated by team or analyst, per daily and per monthly.

## Enhanced User Experiences

### Enhanced Workflow Navigation and Homepage

The way we organize content on a site defines its identity and helps you find the information you’re looking for and then process it meaningfully and intuitively. This involves aligning the navigation with your mental models and jobs to be done. To that extent we have introduced new groupings for our assessments and features. Each assessment aligns to a category of fraud and has features which are unique to them easily available as tabs underneath. Features which are shared across multiple assessments are then grouped under Data and Settings. Under Data you will find everything relevant for data exploration, ingress, and egress. And under Settings you will find all of the typical admin and service-management related features such as metering and user access. With this new navigational structure we hope to enable you enables you to ascertain why, how, and when to use our product.

### Guided Tours

To further streamline first-time and ongoing use of the portal we have introduced an updated experience for the homepage as well as feature-specific guided tours. The new homepage has tiles for each assessment and allows you to select tours that cover features such as creating rules, generating your first loss prevention report, so on and so forth. Each tour will guide you through the portal and explain the use cases and high-level tips to getting started with that feature. The new homepage will then also include a static list of steps for onboarding onto each assessment as well as general admin tasks. Lastly, also provided on the homepage are links to the documentation as well as the ideas portal where you can engage with the Dynamics 365 Fraud Protection community to make your mark on the product by submitting and voting on new feature requests.

## Enhancement to Rules 

### Clause Naming

Rules are made up of clauses, each of which may express a different aspect of your fraud strategy. We now provide the option for customers to give each of these clauses a unique name. These clause names are surfaced not only in the rule itself, but are also exposed in the API response for an assessment. This means that for a given transaction, in addition to the rule that triggered a decision, we now provide the name of the clause that triggered the decision as well.  

### New rule evaluation behavior

We’ve introduced a new setting which provides customers with two distinct options for how they’d like their rules to be evaluated. In the case that no clauses within an individual rule return a decision, this setting allows customers to specify whether they’d like the transaction to be approved, or if the they’d like the next rule to be evaluated. We’ve also added a new section in the assessment API response, called “ruleEvaluations”, which lists each rule and clause that was evaluated for a particular transaction. 

## Dynamics 365 Commerce Customer Offer

Starting October 01, 2020, a limited capacity of Microsoft Dynamics 365 Fraud Protection is included in the Dynamics 365 Commerce license. Commerce customers will be able to use Fraud Protection for no extra charge up to the limits specified below, and will have the option to purchase additional Fraud Protection add-ons if their usage requires higher limits:
- Purchase protection up to 2,000 assessments per month 
- Account protection up to 20,000 assessments per month 
- Loss prevention up to 8,000 transactions per month 

This will make it easy for all existing and new Commerce customers to evaluate how Fraud Protection capabilities can help protect their organizations against fraudulent purchases, fake accounts creation, suspicious log-ins, and employee fraud in the form of inappropriate discounts or returns. Commerce customers can start using Fraud Protection in just a few minutes by visiting the [product portal](https://dfp.microsoft.com/), signing in with tenant Global Admin credentials and completing a one-time set up for their environment.

