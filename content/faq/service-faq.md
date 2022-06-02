---
author: josaw1
description: This topic provides frequently asked questions and answers (FAQ) about the Microsoft Dynamics 365 Fraud Protection service.
ms.author: josaw
ms.date: 06/01/2022
ms.topic: faq
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Service FAQ
---

# Service FAQ

## What types of fraud is Dynamics 365 Fraud Protection designed to mitigate?

Fraud Protection offers solutions through 3 different channels: Purchase Protection, Account Protection, and Loss Prevention. Purchase protection deals with payment fraud, account protection deals with account login and creation fraud, and loss prevention assists merchants in identifying and investigating anomalous behaviors at point of sale terminals.

## What methodology does Fraud Protection use for scoring transactions and how does it work?

Fraud Protection enables its customers (businesses using Fraud Protection for fraud protection) to embed Fraud Protection's device fingerprinting technology in their end user experience (web and mobile) and call Fraud Protection's fraud assessment APIs with specific details of an event and in response receive back risk probability score and reason code from Fraud Protection. For example, during purchase flow, Fraud Protection's customer can embed device fingerprinting on check out page and whenever end user clicks on confirm purchase button, Fraud Protection's risk assessment API for Purchase can be invoked with purchase details such as who is making purchase, details of items being purchased, using what type of payment method. Fraud Protection ML models use Purchase information, device fingerprinting information, and data from Fraud Protection's fraud protection network that spans knowledge from customers in various industry verticals (stored in a compliant de-identified form) to generate a score and reason codes that depicts probability of that specific purchase being a fraudulent attempt.

Fraud Protection provides the risk score, but the ultimate decision on whether to proceed with the purchase transaction is made by the customer and can be made through rules that customers configure in Dynamics 365 Fraud Protection's decision engine.

## What machine learning capability/algorithms are built into the Fraud Protection system?

Fraud Protection uses an advanced breed of machine learning (ML) called adaptive artificial intelligence (Adaptive AI) to accurately differentiate between fraud and legitimate transactions. The technique consumes real-time data attributes from a global network of connected commerce data (compiled from all customers using the service, including Microsoft's own businesses). This data provides valuable insights into how instances of fraud are connected across the world in terms of entities such as devices, products, IP addresses etc. The ML algorithms then use specialized fast-retraining mechanisms and multi-layer models that take full advantage of these informative early signals regarding newly evolving fraud attacks to help "immunize" the members of the network before the new fraud attack reaches them. Microsoft also uses the latest breed of ML modelling techniques including deep semi-supervised learning, while also providing human understandable explanations for every ML risk assessment.

## What types of data should merchants provide to Fraud Protection for efficient fraud analysis?

The Purchase API mainly collects data attributes including transaction context (order type, order-initiated channel etc.), transaction time (customer local time etc.), user information (account ID, email, country, creation date etc.), payment instrument information (payment instrument ID, payment method, bin number, billing address etc.), product information (product type, SKU, name, price, quantity etc.), device information (IP address, device context ID etc.) and some additional information.

The PurchaseStatus, BankEvent, Label API collect corresponding feedback information to update the final status of the transaction.

For a detailed list of APIs, refer to [Swagger UI](https://dfpswagger.azurewebsites.net/index.html).


## What reporting and analytics functionality does Fraud Protection offer out of the box? What are the main features of the reporting?

Analytics include general trends, score distributions, and model performance within particular transaction types. Reporting is provided within the product through built-in PowerBI dashboards that allow users to see performance across the system for purchase protection, account protection and loss prevention. KPI trends are displayed in the pre-built reporting. In addition, we work with all our customers to ensure we can meet or provide the tools to meet any additional reporting capabilities they may need.

## How does the Fraud Protection system or services scale to meet increasing transactional needs? What proven capabilities are used to handle high transaction levels across the Fraud Protection customer base?

Fraud Protection is built on top of Microsoft's Azure cloud platform and benefits from the same cloud scalability that Azure provides to all its customers. In addition to its external customers, Fraud Protection has been handling the scale of Microsoft's own business for several years with no scale challenges.
