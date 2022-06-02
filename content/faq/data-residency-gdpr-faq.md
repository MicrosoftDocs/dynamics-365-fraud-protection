---
author: josaw1
description: This topic provides frequently asked questions and answers (FAQ) about data residency and GDPR in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 06/01/2022
ms.topic: faq
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Data residency and GDPR FAQ
---

# Data residency and GDPR FAQ

## Can a customer choose a geography where Dynamics 365 Fraud Protection will store and process its data? Will any data move outside the geography? 

A customer can choose a geography where Fraud Protection will be storing the master copy of their data from the list of geographies where Fraud Protection is present (US, CA, EU). To provide accurate scores and global fraud insights using Fraud Protection Network, Fraud Protection needs to store and process certain data outside of customer chosen geography.

Also, the pseudonymized data inside the Fraud Protection Network is stored and processed in a common set of regions and datacenters designated by the Fraud Protection team with the primary data warehouse in the United States. This includes pseudonymized data contributed by customers and derived data such as features, aggregations, reports, and machine learning models. The list of regions may change over time but is chosen with the goal of providing a low latency and accurate global fraud assessment for all Fraud Protection Network customers.

## What are the locations that will directly process, transmit, or store merchant data? What are the physical access controls in place?

Fraud Protection customers can choose a geography where Fraud Protection will be storing and processing the master copy of their data. Microsoft will choose specific datacenters in those geographies based on availability of resources and other factors. To provide accurate scores and global fraud insights using Fraud Protection Network, Fraud Protection will store and process certain data in datacenters outside of customer chosen geography.

Microsoft implements a common set of physical security best practices across their datacenters. Main access to the datacenter facilities is typically restricted to a single point of entry that is manned by security personnel. The main interior or reception areas have electronic card access control devices on the perimeter door(s), which restrict access to the interior facilities. Rooms within the Microsoft datacenters that contain critical systems (servers, generators, electrical panels, network equipment, etc.) are restricted through various security mechanisms, such as electronic card access control, keyed lock on each individual door, man traps, and / or biometric devices.

For more information on the physical security of Azure datacenters, see the [Physical security of Azure datacenters](/azure/security/fundamentals/physical-security.md) topic.



## Will Fraud Protection provide the physical location or geography where a customer's data is stored upon request? Does Fraud Protection allow customers to define acceptable geographical locations for data routing or resource instantiation?

Customers have no direct control over instantiation of internal resources used by Fraud Protection to provide the service. Fraud Protection Customers can choose a geography where Fraud Protection will store and process the master copy of their data. Microsoft will choose specific datacenters in those geographies based on availability of resources and other factors. To provide accurate scores and global fraud insights using Fraud Protection Network, Fraud Protection will store and process certain data in datacenters outside of customer chosen geography.

## Where is the data collected by the device fingerprinting feature stored and processed? How long is the data retained in those locations?

The data collected by the device fingerprinting feature is stored in a Microsoft designated data center closest to the location of the transaction source (for example, web browser or mobile device).  This data center may be outside the customer-provisioned geography (US, CA or EU).  This intermittent data is stored for up to 28 days after which the master copy of data is stored in the customer's environment in the provisioned geography.

##  Do Fraud Protection customers have to sign a data processing agreement at the time of proof of concept?

Yes.

## What kind of technical and organizational measures (TOMs) does Fraud Protection take to protect personal data in accordance with GDPR?

Fraud Protection implements a set of technical and organizational measures around data security and privacy which meet requirements of ISO 27018, SOC2 and other certifications. See the [Service Trust Portal](https://servicetrust.microsoft.com/) for the up-to-date list of audit reports.

## Does Fraud Protection work with a data privacy officer to oversee GDPR compliance (art. 37 GDPR)?

Yes. 
The up-to-date contact information for the data privacy officer is available in the Microsoft data protection addendum here: [Licensing documents](https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA).
