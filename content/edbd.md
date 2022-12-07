---
author: josaw1
description: This article provides an overview of data egress outside of the European Union that occurs in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 12/07/2022
ms.topic: overview
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: European Data Boundary Descriptions

---

# European Data Boundary Descriptions

> [!IMPORTANT]
> For comprehensive details about Microsoft's EU Data Boundary commitment, refer to [insert link here](http://www.microsoft.com).

The goal of the EU Data Boundary is to minimize cases where EU customers’ Customer Data or Personal Data leaves the EU. However, there are some scenarios where Microsoft must transfer data to meet cloud and service operational requirements. 

## Data egress in Dynamics 365 Fraud Protection

Fraud Protection transmits all or a significant amount of Customer Data collected from credit card transactions and device fingerprinting in a pseudonymized format to a separate database in the US for machine learning modeling and processing across all services tenants (Network database). These data are further encrypted and the crypto keys are hashed and salted for increased security protection. 

## Additional resources

- [Device fingerprinting](device-fingerprinting.md)
- [Transaction account booster (TAB)](tab.md)
- [insert link to transparency doc here](http://www.microsoft.com)






<!--- A device fingerprint contains information that is collected about a remote computing device for the purpose of identifying the device. Device fingerprinting collects device telemetry during online actions, including hardware information, browser information, geographic information, and the Internet Protocol (IP) address. 
Dynamics 365 Fraud Protection provides a device fingerprinting service so that device identification can be used as input to the process of fraud assessment. This service helps Fraud Protection track and link seemingly unrelated events in the fraud protection network to help identify patterns of fraud. When device characteristics and attributes are collected, the device fingerprinting service uses machine learning to probabilistically identify the device.
•	Reason for Customer Data egression: The data is collected in the region/geography closest to the customer’s device and the data is updated as the device reports additional data. The data is then replicated across all fingerprinting geographies and matched with the data from other regions. Device fingerprinting is sensitive to latency between the end-user device and the fingerprinting endpoint. Increased latency would result in a significant loss of fingerprinting precision. To decrease latency and improve assessment results, data flows to the United States where data processing and storage occur. The data is then either merged with the transaction data of the customer and moved to their geography, or pseudonymized and sent to the fraud protection network. Data does not flow out of the customer’s geography after the data arrives to that geography.
•	Types of Customer Data being egressed: The types of data collected include device attributes such as plugins installed and processor class, operating system attributes, browser-related attributes (if applicable) such as browser language and font, and network attributes such as IP address and signature hash. The data does not contain unique device identifiers and is collected without authentication of the device or the user.
•	Location data is egressed to: To minimize latency, the data flows out of the EU Data Boundary to the United States where data processing and storage occur. 
•	How the data is secured when outside of the EU Data Boundary: The egressed data is processed by the fingerprinting service, and access to the data by Microsoft personnel can be granted only through Secure Admin Workstation (SAW) or just-in-time (JIT) access permission. Data transfer is encrypted.
•	Dynamics 365 Fraud Protection Transaction acceptance booster Dynamics 365 Fraud Protection customers may opt-in to sending their transaction data which can include bank identification number, email address, mobile phone, etc. to participating card networks and issuing banks participating in the “Transaction acceptance booster” (TAB) program. When the optional feature is turned on by the customer, Dynamics 365 Fraud Protection will communicate to the external endpoint managed by the corresponding card network or issuing bank which may be hosted outside of the customer’s geography. Customer Data is transient for Dynamics 365 Fraud Protection protected by encryption, while the data is stored by the TAB participating bank or card network based on their policies. Customers need to opt-in to this service feature.--->

