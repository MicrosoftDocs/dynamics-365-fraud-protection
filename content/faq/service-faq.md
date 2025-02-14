---
author: josaw1
description: This article provides answers to frequently asked questions (FAQ) about the Microsoft Dynamics 365 Fraud Protection service.
ms.author: josaw
ms.date: 12/09/2022
ms.topic: faq
search.audienceType:
  - admin
title: Service FAQ
---

# Service FAQ

[!include[deprecation](../includes/deprecation.md)]

This article provides answers to frequently asked questions (FAQ) about the Microsoft Dynamics 365 Fraud Protection service.

#### What types of fraud is Fraud Protection designed to mitigate?

Fraud Protection offers solutions through three channels: purchase protection, account protection, and loss prevention. Purchase protection deals with payment fraud, account protection deals with account sign-in and creation fraud, and loss prevention helps merchants identify and investigate anomalous behavior at point of sale (POS) terminals.

#### What methodology does Fraud Protection use to score transactions, and how does it work?

Fraud Protection enables its customers to embed Fraud Protection's device fingerprinting technology in their web and mobile user experiences, and to call Fraud Protection's fraud assessment APIs by using specific details of an event. Customers then receive a risk probability score and reason codes from Fraud Protection. For example, during the purchase flow, a Fraud Protection customer can embed device fingerprinting on the checkout page and whenever a user selects the purchase confirmation button. Fraud Protection's risk assessment API for Purchase can be invoked by using purchase details such as the person who is making the purchase, details of the items that are being purchased, and the type of payment method that is used. Fraud Protection machine learning (ML) models use purchase information, device fingerprinting information, and data from the Fraud Protection Network to generate a score and reason codes that represent the probability that the purchase is a fraudulent attempt.

Although Fraud Protection provides the risk score, customers make the ultimate decision about whether to proceed with the purchase transaction. This decision can be made through rules that customers configure in Fraud Protection's decision engine.

#### What machine learning capabilities and algorithms are built into the Fraud Protection system?

Fraud Protection uses an advanced type of machine learning (ML) that is known as adaptive artificial intelligence (Adaptive AI) to accurately differentiate between fraud and legitimate transactions. The technique consumes real-time data attributes from a global network of connected commerce data that is compiled from all customers who use the service, including Microsoft's own businesses. This data provides valuable insights into how instances of fraud are connected across the world, in terms of entities such as devices, products, and IP addresses. The ML algorithms then use specialized fast retraining mechanisms and multilayer models that take advantage of these informative early signals about newly evolving fraud attacks to help "immunize" members of the network before the new fraud attack reaches them. Microsoft also uses the latest ML modeling techniques, including deep, semi-supervised learning, and provides human-understandable explanations for every ML risk assessment.

#### What types of data should merchants provide to Fraud Protection for efficient fraud analysis?

The Purchase API mainly collects data attributes that include transaction context (such as order type and order-initiated channel), transaction time (such as customer local time), user information (such as account ID, email address, country or region, and creation date), payment instrument information (such as payment instrument ID, payment method, Bank Identification Number \[BIN\], and billing address), product information (such as product type, stock keeping unit \[SKU\], name, price, and quantity), device information (such as IP address and device context ID), and some additional information.

The PurchaseStatus, BankEvent, and Label APIs collect corresponding feedback information to update the final status of a transaction.

For a detailed list of APIs, see [Swagger UI](https://dfpswagger.azurewebsites.net/index.html).

#### What reporting and analytics functionality does Fraud Protection offer out of the box? What are the main features of the reporting?

Analytics include general trends, score distributions, and model performance in specific transaction types. Reporting is provided in the product through built-in Power BI dashboards that let users view performance across the system for purchase protection, account protection, and loss prevention. Trends for key performance indicators (KPIs) are shown in the prebuilt reporting. In addition, we work with all our customers to ensure that we can meet or provide the tools to offer any other reporting capabilities that are required.

#### How does the Fraud Protection system or service scale to meet increasing transactional needs? What proven capabilities are used to handle high transaction levels across the Fraud Protection customer base?

Fraud Protection is built on top of Microsoft's Azure cloud platform and benefits from the same cloud scalability that Azure provides to all its customers. In addition to its external customers, Fraud Protection has been handling the scale of Microsoft's own business for several years and has encountered no scale challenges.

## Additional resources

[Legal considerations FAQ](legal-faq.md)

[Privacy and security FAQ](privacy-security-faq.md)

[Data residency FAQ](data-residency-faq.md)

[Compliance FAQ](compliance-faq.md)
