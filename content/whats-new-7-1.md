---
author: yvonnedeq
description: This topic explains what's new in the Microsoft Dynamics 365 Fraud Protection July 2020 release.
ms.author: josaw
ms.date: 07/07/2020

ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: What's new in Dynamics 365 Fraud Protection July 2020 release

---

# What's new in Dynamics 365 Fraud Protection July 2020 release 

## May INT (only) features available in both INT and PROD

In the May release, only features in INT were updated. However, in the July release, both PROD and INT are updated so that they are in parity. Features from the May release are now available in PROD.

### Extend and tailor merchant purchase ontology

In several cases, a merchant might need capabilities beyond the core features that Microsoft Dynamics 365 Fraud Protection provides. When merchants extend the base ontology with custom knowledge in the marquee scenarios of payment fraud and account takeover, they might want to use specialized data beyond the base ontology of Fraud Protection to help improve the fraud protection capability of the product. For example, for airline ticket purchases, the seat class might be an important attribute to consider.

Furthermore, customers might have niche fraud protection scenarios, such as refunds, loyalty programs, and warranty programs, each of which has its own set of relevant data. Merchants can now bring specialized data into the product by extending the ontology as they require.

Merchants can also define custom rules. They can use custom knowledge to create and update the configuration of model operating points by using specialized data. These model operating points can use the full spectrum of available knowledge to produce decisions for each type of event.

### More powerful rule and list capabilities

Fraud Production has released an all-new rules experience that lets merchants express their augmented custom fraud logic in a rich and expressive language. This language is designed to give merchants the power and flexibility that they need to customize their fraud strategy and enforce their unique fraud business policies. The language is coupled with assistive technologies such as reusable lists, rich IntelliSense, highlighting, real-time debugging, and frequently used templates to help merchants get started.

In addition to payload values and scores that are based on artificial intelligence (AI), rules can also use custom lists that merchants create to manage data that is specific to their needs or fraud protection strategy.

### Expanded coverage for transaction acceptance booster

The transaction acceptance booster feature has enabled the sharing of transaction trust knowledge with selected partner banks to help increase the acceptance rate and reduce fraud. In this release, more banks are added to the partner network. This change increases the market coverage and lets merchants boost the acceptance rate on more transactions in the US and other countries and regions.

## Loss prevention

The loss prevention capability in Fraud Protection is a cloud-based solution that helps protect revenue by identifying potential fraud on returns and discounts that arise from omni-channel purchases. Therefore, store managers and investigators can quickly take action to mitigate losses.

To integrate loss prevention capability with Dynamics 365 Commerce, follow these steps:

-	Turn on the Azure Data Lake Storage service for the Commerce environment.
-	Turn on loss prevention in the Commerce environment.
-	Add a service account and subscribe to Fraud Protection in the Commerce environment.
-	Configure loss prevention settings in Fraud Protection.

## Event tracing

The event tracing functionality lets merchants establish a real-time telemetry platform that is extensible and operational outside the Fraud Protection portal. Each event is either scheduled or triggered by a user-level or system-level action and forwarded to the merchant's Azure Event Hubs.

Events can be aggregated and used to define metrics that merchants can use to monitor and manage service costs and utilization. Events can also be used to maintain system logs of actions that are taken in the Fraud Protection portal (for example, actions to edit rules and lists) or to develop custom reports by using Azure Stream Analytics and Power BI.

By using the Event Hubs connectors that are available in Power Automate and Logic Apps, merchants can also use the data that they send to Event Hubs to develop alerting or highly customized workflows.

## Custom assessments

Effective fraud management is a multi-tier strategy. To maximize fraud detection and minimize customer friction, merchants must assess interactions at various phases of a user's journey, and decide whether the interactions should be allowed, challenged, or prevented. Every business is different, and so are the associated user interactions that transmit signals about potential fraud. For example, profile updates, such as changes to a user's address or payment information, might be a key event for an e-commerce business. Depending on the business model, other examples of user interactions that might be key events include submission of reviews, updates of seat preferences on a travel site, the addition of family and friends on a subscription or gaming service, and submission of a service support ticket or a complaint.

Microsoft understands the importance of including these types of business-specific events to help merchants with their overall fraud management strategy. Therefore, Fraud Protection now lets merchants add custom assessments in addition to common assessment events, such as account creation, account login, and purchase protection events. Merchants can create and define a custom assessment, including its name, the API path, and a payload that is appropriate to the specific event. They can then configure rules that the assessment uses to return a decision, such as **Approve**, **Reject**, **Review**, or **Challenge**.

## Mobile reference implementation

Mobile device fingerprinting is a new addition to Fraud Protection's device fingerprinting capability. Merchants can use this capability to make device fingerprinting available in their mobile apps. The reference implementation will help developers and customers learn how to make device fingerprinting capabilities available in their mobile apps.

## Rule drafts

The rules experience is extended so that users can save changes to their rules as drafts before they commit them to production.

## Additional language support

Fraud Protection is now available in seven languages: English, French, German, Brazilian Portuguese, Italian, Spanish, and Dutch.


[!INCLUDE[footer-include](includes/footer-banner.md)]
