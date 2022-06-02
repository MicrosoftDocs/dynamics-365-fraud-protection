---
author: josaw1
description: This article provides answers to frequently asked questions (FAQ) relating to legal considerations in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 06/02/2022
ms.topic: faq
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Legal considerations FAQ
---

# Legal considerations FAQ

This article provides answers to frequently asked questions (FAQ) relating to legal considerations in Microsoft Dynamics 365 Fraud Protection.

### How does Fraud Protection ensure that it doesn't collect data from users under the minimum age legally allowed in connection with data profiling and collection?

It is the responsibility of the merchant to ensure that the data collected is legally valid in each jurisdiction, for example as required by the Children's Online Privacy Protection Act (COPPA) in the United States.

### Is Fraud Protection staff required to sign confidentiality or non-disclosure agreements?

Yes.

### Are customers notified when Fraud Protection makes material changes to information security and/or privacy policies?

Yes. Fraud Protection will notify customers if there are changes to policies that are not reflected in Microsoft or Dynamics communications. However, Fraud Protection tries to closely follow policies set by Microsoft and Dynamics, and those policies are communicated via the [Service Trust Portal](https://servicetrust.microsoft.com).

For more information regarding Dynamics 365 security, see the [Microsoft Trust Center](https://www.microsoft.com/trustcenter/default.aspx).

### Does Fraud Protection enforce and attest to tenant data separation when producing data in response to legal subpoenas?

For information on Microsoft's new EU privacy campaign (Schrems II) and commitments, see [New steps to defend your data](https://blogs.microsoft.com/on-the-issues/2020/11/19/defending-your-data-edpb-gdpr/).

For information on how Microsoft handles government requests, see the [U.S. National Security Order Report](https://www.microsoft.com/en-us/corporate-responsibility/us-national-security-orders-report?activetab=pivot_1%3aprimaryr2) and the [Law Enforcement Requests Report](https://www.microsoft.com/en-us/corporate-responsibility/law-enforcement-requests-report). 

### Does Fraud Protection support litigation holds (freeze of data from a specific point in time) for a specific tenant without freezing other tenant data?

When a party is in litigation, Microsoft (at an organizational level) can isolate data by taking a snapshot of the data and securing such data separately to be "untouched." Fraud Protection can do a full backup as a snapshot, however it doesn't provide this functionality as a self-serve service since it's not expected to function as a system of record for customers.

### Does Fraud Protection have legal counsel to review all customer and third-party agreements?

Yes.

### Is Fraud Protection associated with any third-party organization to process, transmit, or store data? If yes, are there supporting legal documents?

For information about Microsoft's data subprocessors, see the [Microsoft Cloud Services Subprocessors List](https://servicetrust.microsoft.com/ViewPage/TrustDocumentsV3?command=Download&downloadType=Document&downloadId=ede6342e-d641-4a9b-9162-7d66025003b0&tab=7f51cb60-3d6c-11e9-b2af-7bb9f5d2d913&docTab=7f51cb60-3d6c-11e9-b2af-7bb9f5d2d913_Subprocessor_List).

## Additional resources

[Service FAQ](service-faq.md)

[Privacy and security FAQ](privacy-security-faq.md)

[Data residency and GDPR FAQ](data-residency-gdpr-faq.md)

[Compliance FAQ](compliance-faq.md)
