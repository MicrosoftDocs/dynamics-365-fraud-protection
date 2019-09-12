---
author: jegrif
description: This topic provides information about artificial intelligence (AI) and insights from the fraud protection network in Microsoft Dynamics 365 Fraud Protection.
ms.author: v-jegrif
ms.service: fraud-protection
ms.date: 04/22/2019

ms.topic: conceptual
title: Artificial intelligence (AI) and insights from the fraud protection network
---


# Artificial intelligence (AI) and insights from the fraud protection network

Microsoft Dynamics 365 Fraud Protection takes advantage of the industry-leading Microsoft artificial intelligence (AI) platform to assess the likelihood that a transaction is fraudulent. The AI platform uses transactional data to train machine learning models and detect linkages of fraud that occur across all merchants in the fraud protection network.

By participating in this network, you can derive insights from the collective experience of other merchants who use Dynamics 365 Fraud Protection. In this way, you can help your business handle emerging fraud vectors.

## Participation and privacy

To use the Evaluate and Protect experiences in Dynamics 365 Fraud Protection, you must grant permission to share selected data with the fraud protection network. To help protect the privacy of participating businesses and their customers, any data that the network uses is always in one of the following forms:

- **Derived features of attributes of entities** – A plain text address, for example, is never shared. Instead, the fact that the address represents a post office box might be shared. These derivations can't be reverse engineered to reveal the original values.
- **Irreversibly hashed tokens of entities** – Tokenization helps guarantee that the fraud protection network can build up linkage information without storing the explicit details of the entities. This behavior helps protect both customer privacy and merchant privacy.

The fraud protection network is owned and controlled exclusively by Microsoft. It has superior security and compliance capabilities. Participation in the fraud protection network doesn't cause your data to be revealed to other merchants or external entities. Additionally, no merchant can exploit business intelligence from any other merchant for competitive purposes. Only Dynamics 365 Fraud Protection and device fingerprinting applications that are explicitly devoted to fraud protection have access to the network.

For more information about how your data is protected, see [Security, compliance, and data subject requests](security-compliance.md).
