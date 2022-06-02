---
author: josaw1
description: This topic provides frequently asked questions and answers (FAQ) relating to legal considerations in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 06/01/2022
ms.topic: faq
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Legal considerations FAQ
---

# Legal considerations FAQ

## How does Dynamics 365 Fraud Protection ensure it doesn't collect data from end users who are under the minimum age legally allowed in connection with data profiling/collection?

It is the responsibility of the merchant to ensure the data collected is legally valid in each jurisdiction (for example, as required by COPPA in the United States).

## Is Fraud Protection staff required to sign confidentiality or non-disclosure agreements?

Yes.

## Are customers notified when Fraud Protection makes material changes to information security and/or privacy policies?

Yes.
Fraud Protection will notify customers if there are changes to policies which are not reflected in Microsoft or Dynamics level communication, but Fraud Protection tries to closely follow policies set by Microsoft and Dynamics, and those are being communicated via the central trust portal.

For more information regarding Dynamics 365 security, see the [Microsoft Trust Center](https://www.microsoft.com/trustcenter/default.aspx).

## Does Fraud Protection enforce and attest to tenant data separation when producing data in response to legal subpoenas?

See Microsoft's new EU privacy campaign (Schrems II) and commitments in the following blog post: [New steps to defend your data](https://blogs.microsoft.com/on-the-issues/2020/11/19/defending-your-data-edpb-gdpr/).

FOr information on how Microsoft handles government requests, see the [U.S. National Security Order Report](https://www.microsoft.com/en-us/corporate-responsibility/us-national-security-orders-report?activetab=pivot_1%3aprimaryr2) and [Law Enforcement Requests Report](https://www.microsoft.com/en-us/corporate-responsibility/law-enforcement-requests-report). 
<https://www.microsoft.com/en-us/corporate-responsibility/law-enforcement-requests-report>

## Can Fraud Protection support litigation holds (freeze of data from a specific point in time) for a specific tenant without freezing other tenant data?

When a party is in litigation, Microsoft (at an organizational level) can isolate data by taking a snapshot of the data and securing such data separately to be "untouched". Fraud Protection can do a full backup as a snapshot, however it doesn't provide this functionality in a self-serve manner since it's not expected to function as a system of record for customers.

## Does Fraud Protection have legal counsel to review all customer and third-party agreements?

Yes.

## Is Fraud Protection associated with any third-party organization to process, transmit, or store data? If yes, are there supporting legal documents?

For information about Microsoft's sub-processors, see the [	Microsoft Cloud Services Subprocessors List](https://servicetrust.microsoft.com/ViewPage/TrustDocumentsV3?command=Download&downloadType=Document&downloadId=ede6342e-d641-4a9b-9162-7d66025003b0&tab=7f51cb60-3d6c-11e9-b2af-7bb9f5d2d913&docTab=7f51cb60-3d6c-11e9-b2af-7bb9f5d2d913_Subprocessor_List) on the Data Protection Resources page.
