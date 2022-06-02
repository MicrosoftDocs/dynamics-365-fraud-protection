---
author: josaw1
description: This article provides answers to frequently asked questions (FAQ) about data residency and General Data Protection Regulation (GDPR) in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 06/02/2022
ms.topic: faq
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Data residency and GDPR FAQ
---

# Data residency and GDPR FAQ

This article provides answers to frequently asked questions (FAQ) about data residency and General Data Protection Regulation (GDPR) in Microsoft Dynamics 365 Fraud Protection.

### Can a customer choose a geography where Dynamics 365 Fraud Protection will store and process its data? If so, will any data move outside the geography? 

A customer can choose a geography where Fraud Protection stores the master copy of their data from the list of geographies where Fraud Protection is present (US, Canada, and the EU). To provide accurate scores and global fraud insights using Fraud Protection Network, Fraud Protection needs to store and process certain data outside of customer chosen geography.

Also, the pseudonymized data inside the Fraud Protection Network is stored and processed in a common set of regions and datacenters designated by the Fraud Protection team, with the primary data warehouse being in the United States. This includes pseudonymized data contributed by customers and also derived data such as features, aggregations, reports, and machine learning models. The list of regions may change over time, but regions are chosen with the goal of providing a low latency and accurate global fraud assessment for all Fraud Protection Network customers.

### What are the locations that directly process, transmit, or store merchant data? What are the physical access controls in place?

Fraud Protection customers can choose a geography where Fraud Protection stores and processes the master copy of their data. Microsoft chooses specific datacenters in those geographies based on availability of resources and other factors. To provide accurate scores and global fraud insights using Fraud Protection Network, Fraud Protection stores and processes certain data in datacenters outside of the customer's chosen geography.

Microsoft implements a common set of physical security best practices across their datacenters. Main access to the datacenter facilities is typically restricted to a single point of entry that is manned by security personnel. The main interior or reception areas have electronic card access control devices on the perimeter door(s) that restrict access to the interior facilities. Rooms within the Microsoft datacenters that contain critical systems (servers, generators, electrical panels, and network equipment) are restricted through various security mechanisms such as electronic card access control, keyed locks on each individual door, man traps, and biometric devices.

For more information on the physical security of Azure datacenters, see [Physical security of Azure datacenters](/azure/security/fundamentals/physical-security.md).

### Will Fraud Protection provide the physical location or geography where a customer's data is stored upon request? Does Fraud Protection allow customers to define acceptable geographical locations for data routing or resource instantiation?

Customers have no direct control over the instantiation of internal resources used by Fraud Protection to provide the service. Fraud Protection customers can choose a geography where Fraud Protection stores and processes the master copy of their data. Microsoft chooses specific datacenters in those geographies based on availability of resources and other factors. To provide accurate scores and global fraud insights using Fraud Protection Network, Fraud Protection stores and processes certain data in datacenters outside of a customer's chosen geography.

### Where is the data collected by the device fingerprinting feature stored and processed? How long is the data retained in those locations?

The data collected by the device fingerprinting feature is stored in a Microsoft-designated data center closest to the location of the transaction source (for example, a web browser or mobile device). The data center may be outside the customer-provisioned geography (US, Canada, or EU). This intermittent device fingerprinting data is stored for up to 28 days, after which the master copy of data is stored in the customer's environment in the provisioned geography.

### Do Fraud Protection customers have to sign a data processing agreement at the time of proof of concept?

Yes.

### What kind of technical and organizational measures (TOMs) does Fraud Protection take to protect personal data in accordance with GDPR?

Fraud Protection implements a set of technical and organizational measures around data security and privacy that meet requirements of ISO 27018, SOC2, and other certifications. For an up-to-date list of audit reports, see [Service Trust Portal](https://servicetrust.microsoft.com/).

### Does Fraud Protection work with a data privacy officer to oversee GDPR compliance per Article 37 GDPR?

Yes. The up-to-date contact information for the data privacy officer is available in the Microsoft data protection addendum on the [Licensing Documents](https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA) page of the Microsoft Licensing Resources and Documents site.

## Additional resources

[Service FAQ](service-faq.md)

[Legal considerations FAQ](legal-faq.md)

[Privacy and security FAQ](privacy-security-faq.md)

[Compliance FAQ](compliance-faq.md)
