---
author: josaw1
description: This article provides an overview of data egress outside of the European Union that occurs in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 12/14/2022
ms.topic: overview
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: EU Data Boundary exceptions for Dynamics 365 Fraud Protection

---

# EU Data Boundary exceptions for Dynamics 365 Fraud Protection

> [!IMPORTANT]
> For comprehensive details about Microsoft's EU Data Boundary commitment, refer to [insert link here](https://www.microsoft.com).

The goal of the EU Data Boundary is to minimize cases where EU customers’ Customer Data or Personal Data leaves the EU. However, serious threats of fraud from sophisticated users are not constrained by national or geographic boundaries. Malicious actors operate on a worldwide basis leveraging known and newly-discovered vulnerabilities, technical or socially engineered. Therefore, limiting the scope of our fraud detection technology to any given region compromises our ability to offer the best intelligence to detect and prevent online fraud. Fraud protection technologies and professionals are only equipped sufficiently when their scope is enabled to identify patterns, behaviors, and practices on a worldwide basis. Below you will find the scenarios supported by Fraud Protection on a global basis to meet these highly-demanding operational standards. 

## Data egress in Fraud Protection

To provide accurate scores and global fraud insights by using the Fraud Protection Network, Fraud Protection must store and process some data outside a customer's selected geography. Fraud Protection transmits a significant amount of Customer Data collected from payment transactions, online account activities, transactional events of other types, and device fingerprinting in a pseudonymized format to a separate database in the US for machine learning modeling and processing across all service tenants. This data includes pseudonymized data that customers contribute and derived data such as features, aggregations, reports, and machine learning models. This data is further encrypted at rest and in transit with the crypto keys stored in secure locations and managed by Microsoft according to its security best practices.

For more information about what data Fraud Protection processes and how Fraud Protection processes the data, refer to [Privacy protection for customer data](data-processing-protection.md).

### Device fingerprinting

The device fingerprinting feature collects data in the region/geography closest to the customer’s device. The data is then replicated across all fingerprinting geographies and matched with the data from other regions. Device fingerprinting is sensitive to latency between the end-user device and the fingerprinting endpoint. Increased latency would result in a significant loss of fingerprinting precision. To decrease latency and improve assessment results, data flows to the US where data processing and storage occur. This intermittent device fingerprinting data is stored for up to 28 days in the US. After 28 days, the master copy of the data is stored in the customer's environment in the provisioned geography.

### Transaction acceptance booster (TAB)

Customers may opt in to sending their transaction data, which can include bank identification number, email address, mobile phone, etc. to participating card networks and issuing banks participating in the “Transaction acceptance booster” (TAB) program. When the optional feature is turned on by the customer, Fraud Protection will communicate to the external endpoint managed by the corresponding card network or issuing bank, which may be hosted outside of the customer’s geography. Customer Data is stored by the TAB participating bank or card network based on their policies.


## Additional resources

- [insert link to transparency doc here](https://www.microsoft.com)
- [Privacy protection for customer data](data-processing-protection.md)
- [Data residency FAQ](faq/data-residency-gdpr-faq.md)
- [Compliance FAQ](faq/compliance-faq.md)
- [Service FAQ](faq/service-faq.md)
- [Legal considerations FAQ](faq/legal-faq.md)
- [Privacy and security FAQ](faq/privacy-security-faq.md)
- [Device fingerprinting](device-fingerprinting.md)
- [Transaction account booster (TAB)](transaction-acceptance-booster.md)


