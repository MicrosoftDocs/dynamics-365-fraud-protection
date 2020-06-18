---
author: yvonnedeq
description: This topic explains what's new in the Microsoft Dynamics 365 Fraud Protection July 2020 release.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 06/18/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: What’s new in Dynamics 365 Fraud Protection July 2020 release

---

# What’s new in Dynamics 365 Fraud Protection July 2020 release 


## Summary of changes

### May INT (only) features available in both INT and PROD
In our May release we only updated features in INT, however for July both PROD and INT are updated to be in parity. Features from our May release are now available in PROD.
                
#### Extend and tailor merchant purchase ontology 
There are several cases where a merchant may need capabilities beyond the core features that Microsoft Dynamics 365 Fraud Protection provides. When merchants extend the base ontology with custom knowledge in the marquee scenarios of payment fraud and account takeover, they may want to use specialized data beyond the base ontology of Fraud Protection to help improve the fraud protection capability of the product. For example, for airline ticket purchases, the seat class may be an important attribute to consider. 

Furthermore, customers may have niche fraud protection scenarios, for example, refunds, loyalty programs, and warranty programs; each of which has its own set of relevant data. Merchants can now bring specialized data into the product by extending the ontology as needed. 

Merchants can also define custom rules, using custom knowledge to create and update the configuration of model operating points by using specialized data. These model operating points can use the full spectrum of available knowledge to produce decisions for each type of event.

#### More powerful rules and lists capabilities

Fraud Production has released an all-new rules experience that allows merchants to express their augmented custom fraud logic in a rich and expressive language. This language is designed to give merchants the power and flexibility they need to customize their fraud strategy and enforce their unique fraud business policies. The language is coupled with assistive technologies including reusable lists, rich intellisense, highlighting, real-time debugging, and commonly used templates which help merchants get started. 

In addition to payload values and AI-based scores, rules can also leverage custom lists which merchants can create to manage data specific to their needs or fraud protection strategy.

### Rules drafts

The rules experience is extended so users can save changes to their rules as drafts before committing them to production.

#### Expanded coverage for transaction acceptance booster

The transaction acceptance booster feature has enabled the sharing of transaction trust knowledge with selected partner banks to help increase the acceptance rate and reduce fraud. In this release, more banks are added to the partner network. This change increases the market coverage and enables merchants to boost the acceptance rate on more transactions in the US and other countries and regions.

### Loss prevention 

The loss prevention capability in Fraud Protection is a cloud-based solution that helps protect revenue by identifying potential fraud on returns and discounts that arise from omni-channel purchases. This enables store managers and investigators to quickly take action to mitigate losses. 

To integrate loss prevention capability with Dynamics 365 Commerce (Commerce), perform the following steps:
-	Enable the Azure Data Lake Storage (ADLS) service for the Commerce environment.
-	Enable loss prevention in the Commerce environment.
-	Add a service account and subscribe to Fraud Protection in the Commerce environment.
-	Configure loss prevention settings in Fraud Protection.

### Event tracing 

The event tracing functionality enables merchants to  establish a real-time telemetry platform that is extensible and operational outside the portal. Each event is either scheduled or triggered by a user-level or system-level action and forwarded to the merchant's Azure Event Hubs. 

Events can be aggregated and used to define metrics that merchants can use to monitor and manage service costs and utilization. 
They can also be used to maintain system logs on actions that are taken in the Fraud Protection portal (for example, to edit rules and lists) or to develop custom reports using Azure Stream Analytics and Microsoft Power BI. 

Merchants can also use the Event Hubs connectors that are available in Power Automate and Logic Apps to use the data they send to Event Hubs to develop alerting or highly customized workflows.

### Custom assessments

Effective fraud management is a multi-tier strategy. To maximize fraud detection and minimize customer friction, merchants must assess interactions at various phases of a user's journey, and decide whether the user should be allowed to continue, should be challenged, or should be blocked. Every business is different, and so are the associated user interactions that transmit signals about potential fraud. For example, profile updates, such as changes to a user's address or payment information, may be a key event for an e-commerce business. Depending on the business model, other examples of user interactions that may be key events include submission of reviews, updates of seat preferences on a travel site, the addition of family and friends on a subscription or gaming service, and submission of a service support ticket or a complaint.

Microsoft understands the importance of including these types of business-specific events to help merchants with their overall fraud management strategy. Therefore, Fraud Protection now enables merchants to add custom assessments in addition to common assessment events, for example, account creation, account login, and purchase protection events. Merchants can create and define a custom assessment, including its name, the API path, and a payload that is appropriate to the specific event. They can then configure rules that the assessment uses to return a decision, such as *Approve*, *Reject*, *Review*, or *Challenge*.

### Mobile reference implementation 

Mobile device fingerprinting capability is a new addition to Fraud Protection's device fingerprinting capability. Merchants can now use this capability to enable device fingerprinting on their mobile applications. With the help of this reference implementation, developers and customers can learn to enable device fingerprinting capabilities in their mobile applications. 

### Additional language support

Fraud Protection is now available in 7 languages: English, French, German, Brazilian Portuguese, Italian, Spanish, and Dutch.
