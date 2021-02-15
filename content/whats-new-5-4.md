---
author: yvonnedeq
description: This topic explains what's new in the Microsoft Dynamics 365 Fraud Protection May 2020 release.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 02/02/2021

ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: What’s new in Dynamics 365 Fraud Protection May 2020 release

---

# What’s new in Dynamics 365 Fraud Protection May 2020 release

## Extend and tailor merchant purchase ontology 

There are several cases where a merchant might need capabilities beyond Fraud Protection’s core features: 

- To extend the base ontology with custom knowledge in the marquee scenarios of payment fraud. Merchants might want to use specialized data beyond the base ontology of Fraud Protection to improve the fraud protection capability of the product. For example, the seat class selection might be an important attribute to consider for airline ticket purchases. 

- To bring specialized data into the product by extending the ontology as needed. Customers might have niche fraud protection scenarios, such as refunds, loyalty programs, and warranty programs, each of which has its own set of relevant data. 

- To define custom rules. Custom knowledge can be used to create and update the configuration of model operating points using specialized data. These model operating points can consume the full spectrum of available knowledge to produce decisions for each type of event

## More powerful rules and lists capabilities

For purchase protection and account protection, Fraud Production has created a new rules experience to help merchants express their augmented custom fraud logic in a rich and expressive language. This language is designed to give merchants the power and flexibility they need to customize their fraud strategy and enforce their unique fraud business policies. It is coupled with assistive technologies such as reusable lists, rich IntelliSense, highlighting, real-time debugging, and commonly used templates to help them get started with creating custom rules. In addition to payload values and AI-based scores, rules also leverage custom lists which merchants create to manage data specific to their needs or fraud protection strategy.
For more information, see [Manage lists](lists.md), [Manage rules](rules.md), and the [Rules language guide](fpl-lang-ref.md).


[!INCLUDE[footer-include](includes/footer-banner.md)]