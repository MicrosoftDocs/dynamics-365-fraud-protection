---
author: josaw1
description: This article provides answers to frequently asked questions (FAQ) about data residency in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 12/09/2022
ms.topic: faq
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Data residency FAQ
---

# Data residency FAQ

This article provides answers to frequently asked questions (FAQ) about data residency in Microsoft Dynamics 365 Fraud Protection.

>[!NOTE]
>For information about Fraud Protection and Microsoft's EU Data Boundary commitment, refer to the [European Data Boundary Descriptions](../edbd.md) article.

#### Can customers choose the geography where Fraud Protection stores and processes their data? If so, will any data move outside that geography?

Yes, customers can choose the geography where Fraud Protection stores the master copy of their data by selecting it in a list of geographies where Fraud Protection is present (US, Canada, and EU). To provide accurate scores and global fraud insights by using Fraud Protection Network, Fraud Protection must store and process some data outside a customer's selected geography.

In addition, the pseudonymized data inside the Fraud Protection Network is stored and processed in a common set of regions and datacenters that have been designated by the Fraud Protection team. The primary data warehouse is in the United States. This data includes pseudonymized data that customers contribute and derived data such as features, aggregations, reports, and machine learning models. The list of regions might change over time, but regions are chosen with the goal of providing a low-latency and accurate global fraud assessment for all Fraud Protection Network customers.


#### What are the locations that directly process, transmit, or store merchant data? What physical access controls are in place?

Fraud Protection customers can choose the geography where Fraud Protection stores and processes the master copy of their data. Microsoft chooses specific datacenters in those geographies, based on the availability of resources and other factors. To provide accurate scores and global fraud insights by using Fraud Protection Network, Fraud Protection stores and processes some data in datacenters that are outside the customer's selected geography.

Microsoft implements a common set of physical security best practices across its datacenters. Main access to the datacenter facilities is typically restricted to a single point of entry that is staffed by security personnel. The main interior or reception areas have electronic card access control devices on the perimeter doors to restrict access to the interior facilities. Rooms inside the Microsoft datacenters that contain critical systems (servers, generators, electrical panels, and network equipment) are restricted through various security mechanisms, such as electronic card access control, keyed locks on each individual door, man traps, and biometric devices.

For more information about the physical security of Azure datacenters, see [Physical security of Azure datacenters](/azure/security/fundamentals/physical-security).

#### Will Fraud Protection provide, upon request, the physical location or geography where a customer's data is stored? Does Fraud Protection allow customers to define acceptable geographical locations for data routing or resource instantiation?

Customers have no direct control over the instantiation of internal resources that Fraud Protection uses to provide the service. Fraud Protection customers can choose the geography where Fraud Protection stores and processes the master copy of their data. Microsoft chooses specific datacenters in those geographies, based on the availability of resources and other factors. To provide accurate scores and global fraud insights by using Fraud Protection Network, Fraud Protection stores and processes some data in datacenters that are outside a customer's selected geography.

#### Where is the data that the device fingerprinting feature collects stored and processed? How long is the data retained in those locations?

The data that the device fingerprinting feature collects is stored in the Microsoft-designated datacenter that is closest to the location of the transaction source (for example, a web browser or mobile device). The datacenter might be outside the customer-provisioned geography (US, Canada, or EU). This intermittent device fingerprinting data is stored for up to 28 days. After 28 days, the master copy of the data is stored in the customer's environment in the provisioned geography.

#### Do Fraud Protection customers have to sign a data processing agreement at the time of proof of concept?

Yes.

#### What type of technical and organizational measures does Fraud Protection take to protect personal data?

Fraud Protection implements a set of technical and organizational measures (TOMs) around data security and privacy that meet requirements of ISO 27018, SOC2, and other certifications. For an up-to-date list of audit reports, see [Service Trust Portal](https://servicetrust.microsoft.com/).

#### Does Fraud Protection work with a data privacy officer to oversee compliance per Article 37 GDPR?

Yes. The up-to-date contact information for the data privacy officer is available in the Microsoft data protection addendum on the [Licensing Documents](https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA) page of the Microsoft Licensing Resources and Documents site.

## Additional resources

[European Data Boundary Descriptions](../edbd.md)

[Service FAQ](service-faq.md)

[Legal considerations FAQ](legal-faq.md)

[Privacy and security FAQ](privacy-security-faq.md)

[Compliance FAQ](compliance-faq.md)
