---
author: josaw1
description: This article provides answers to frequently asked questions (FAQ) about data residency in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 04/14/2023
ms.topic: faq
search.audienceType:
  - admin
title: Data residency FAQ
---

# Data residency FAQ

[!include[deprecation](../includes/deprecation.md)]

This article provides answers to frequently asked questions (FAQ) about data residency in Microsoft Dynamics 365 Fraud Protection.

>[!NOTE]
>For information about Fraud Protection and Microsoft's EU Data Boundary commitment, refer to the [EU Data Boundary exceptions for Fraud Protection](../edbd.md) article.

#### Can customers choose the geography where Fraud Protection stores and processes their data? If so, will any data move outside that geography?

Yes, at the time of creating a new Fraud Protection environment, customers can choose the geography where Fraud Protection stores the master copy of their data by selecting it from a list of geographies where Fraud Protection is present (US, Canada, and EU). It is also possible to create multiple environments with different geographies if a customer requires different segments of data to be stored in different geographies. For more information about creating environments, see [Create a new environment](../manage-psp-environments.md#create-a-new-environment). Fraud Protection also stores metadata that is not specific to an individual environment (such as billing or search settings) into a separate storage location in the same geography as the first environment. Customers can view the geography of their metadata store on the **Admin Settings** page within Fraud Protection portal. Changes to this geography can be requested by creating a support request from the portal. 

To provide accurate scores and global fraud insights by using Fraud Protection Network, Fraud Protection must store and process some data outside a customer's selected geography. This data includes pseudonymized data that you contribute and other derived data such as features, aggregations, reports, and machine learning models.

The pseudonymized data inside Fraud Protection is stored and processed in a common set of regions and datacenters that have been designated by the Fraud Protection team. The primary data warehouse is in the United States from where some data is replicated to other regions. The list of regions might change over time, but regions are chosen with the goal of providing a low-latency and accurate global fraud assessment for all Fraud Protection customers.

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

#### Does Fraud Protection work with a data privacy officer to oversee compliance?

Yes. The up-to-date contact information for the data privacy officer is available in the Microsoft data protection addendum on the [Licensing Documents](https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA) page of the Microsoft Licensing Resources and Documents site.

## Additional resources

[EU Data Boundary exceptions for Fraud Protection](../edbd.md)

[Service FAQ](service-faq.md)

[Legal considerations FAQ](legal-faq.md)

[Privacy and security FAQ](privacy-security-faq.md)

[Compliance FAQ](compliance-faq.md)
