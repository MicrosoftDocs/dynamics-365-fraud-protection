---
author: josaw1
description: This article provides an overview of data egress outside of the European Union that occurs in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: overview
search.audienceType:
  - admin
title: EU Data Boundary exceptions for Dynamics 365 Fraud Protection

---

# EU Data Boundary exceptions for Dynamics 365 Fraud Protection

> [!IMPORTANT]
> For comprehensive details about Microsoft's EU Data Boundary commitment, refer to [Microsoft's EU Data Boundary documentation](/privacy/eudb/eu-data-boundary-learn).

The goal of the EU Data Boundary is to minimize cases where EU customers’ Customer Data or Personal Data leaves the EU. However, serious threats of fraud from sophisticated attackers are not constrained by national/regional or geographic boundaries. Malicious actors operate on a worldwide basis leveraging known and newly discovered technical or socially engineered vulnerabilities. Therefore, limiting the scope of a fraud detection technology to any given region compromises its ability to offer the best intelligence to detect and prevent online fraud. Fraud protection technologies and professionals are only sufficiently equipped when their scope is enabled to identify patterns, behaviors, and practices on a worldwide basis. 

The scenarios supported by Fraud Protection on a global basis to meet these highly demanding operational standards are detailed in the following sections. 

## Data egress in Fraud Protection

To provide accurate scores and global fraud insights, the Fraud Protection Network must store and process some data outside a customer's selected geography. To that end, Fraud Protection pseudonymizes transaction data and the data derived from it and transmits it to a separate database in the US for machine learning modeling and processing across all service tenants. This data is further encrypted at rest and in transit with the crypto keys stored in secure locations and managed by Microsoft according to its security best practices.

For more information about what data Fraud Protection processes and how Fraud Protection processes the data, refer to [Privacy protection for customer data](data-processing-protection.md).

### Device fingerprinting

The device fingerprinting feature collects data in the region/geography closest to the end user’s device for optimal latency between the device and the fingerprinting endpoint. The data is then replicated across all fingerprinting datacenters and matched with the data from other regions. To improve assessment results and generate additional intelligence, data flows to the US where data processing and storage occur. When device fingerprinting data is matched with a customer's transaction data, a master copy is created and stored in the customer's environment in the provisioned geography. All intermittent device fingerprinting data is retained for up to 28 days and deleted after that period. To enable additional insights, pseudonymized data collected by device fingerprinting is transmitted to and processed by the Fraud Protection Network as explained [above](#data-egress-in-fraud-protection).

### Transaction acceptance booster (TAB)

Customers may opt in to sending their transaction data, which can include bank identification number, email address, and mobile phone to participating card networks and issuing banks that participate in the “Transaction acceptance booster” (TAB) program. When the optional feature is turned on by the customer, Fraud Protection will communicate to the external endpoint managed by the corresponding card network or issuing bank, which may be hosted outside of the customer’s geography. Customer Data is stored by the TAB participating bank or card network based on their policies.


## Additional resources

- [Microsoft's EU Data Boundary documentation](/privacy/eudb/eu-data-boundary-learn)
- [Privacy protection for customer data](data-processing-protection.md)
- [Data residency FAQ](faq/data-residency-faq.md)
- [Compliance FAQ](faq/compliance-faq.md)
- [Service FAQ](faq/service-faq.md)
- [Legal considerations FAQ](faq/legal-faq.md)
- [Privacy and security FAQ](faq/privacy-security-faq.md)
- [Device fingerprinting](device-fingerprinting.md)
- [Transaction account booster (TAB)](transaction-acceptance-booster.md)


