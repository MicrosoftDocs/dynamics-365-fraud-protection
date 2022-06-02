---
author: josaw1
description: This topic provides frequently asked questions and answers (FAQ) relating to legal issues in Microsoft Dynamics 365 Fraud Protection.
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

1.  How do you ensure you do not collect data from any end users who are under the minimum age legally allowed in connection with data profiling/collection in each jurisdiction (e.g., as required by COPPA in the U.S.)?

It is the responsibility of the merchant to ensure the data collected is legally valid.

2.  Are staff members required to sign confidentiality or non-disclosure agreements?

Yes

3.  Are customers notified when Fraud Protection makes material changes to information security and/or privacy policies?

Yes, Fraud Protection will notify if there are changes to policies which are not reflected in Microsoft or Dynamics level communication, but Fraud Protection tries to closely follow policies set by Microsoft and Dynamics, and those are being communicated via the central trust portal.

Additional information regarding Dynamics 365 security can be found here: [<u>https://www.microsoft.com/trustcenter/default.aspx</u>](https://www.microsoft.com/trustcenter/default.aspx)

4.  Does Fraud Protection enforce and attest to tenant data separation when producing data in response to legal subpoenas?

Please see Microsoft's new EU privacy campaign (aka Schrems II) and commitments made available in the following blog post:

New steps to defend your data - Microsoft on the Issues blog: [<u>https://blogs.microsoft.com/on-the-issues/2020/11/19/defending-your-data-edpb-gdpr/</u>](https://blogs.microsoft.com/on-the-issues/2020/11/19/defending-your-data-edpb-gdpr/)

See also our Law Enforcement Request Report and U.S. National Security Order Report, which are updated every six months, to see how we handle government requests

<https://www.microsoft.com/en-us/corporate-responsibility/law-enforcement-requests-report>

<https://www.microsoft.com/en-us/corporate-responsibility/us-national-security-orders-report?activetab=pivot_1%3aprimaryr2>

5.  Is Fraud Protection capable of supporting litigation holds (freeze of data from a specific point in time) for a specific tenant without freezing other tenant data?

When a party is in litigation, Microsoft (At an Organizational level) can isolate data by taking a snapshot of the data and securing such data separately to be "untouched". Fraud Protection can do a full back up as a snapshot, however it doesn't provide this functionality in a self-serve manner to the customers, since it's not expected to function as a system of record for customers.

6.  Does Fraud Protection have legal counsel to review all customer and third-party agreements?

Yes

7.  Is Fraud Protection associated with any 3rd party organizations to process, transmit or store data? If yes, do we have supporting legal documents for each?

Information concerning Microsoft's sub processor list can be found here: [Data Protection (microsoft.com)](https://servicetrust.microsoft.com/ViewPage/TrustDocumentsV3?command=Download&downloadType=Document&downloadId=ede6342e-d641-4a9b-9162-7d66025003b0&tab=7f51cb60-3d6c-11e9-b2af-7bb9f5d2d913&docTab=7f51cb60-3d6c-11e9-b2af-7bb9f5d2d913_Subprocessor_List)
