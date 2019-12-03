---
author: v-davido
description: This topic provides information about security, compliance, and data subject requests.
ms.author: v-davido
ms.service: fraud-protection
ms.date: 12/2/2019

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Security, compliance, and data subject requests
---

# Security, compliance, and data subject requests

Microsoft runs on trust. Microsoft Dynamics 365 Fraud Protection is built on the four foundational principles that Microsoft has defined for a trusted cloud: security, privacy, compliance, and transparency. Microsoft safeguards your business knowledge as if it were its own.

For more information, see the following resources:

- [Microsoft Trust Center](https://www.microsoft.com/trustcenter/default.aspx)
- [Microsoft Runs on Trust](https://www.microsoft.com/en-us/legal/compliance/integrity)

## Data subject requests

Fraud Protection provides tools to help you comply with requests from your customers (data subjects) to export or delete their personal data.

For more information, see the following resources:

- [Data Subject Requests for the GDPR](https://docs.microsoft.com/microsoft-365/compliance/gdpr-data-subject-requests)
- [Safeguard individual privacy with the Microsoft Cloud](https://www.microsoft.com/trustcenter/privacy/gdpr/gdpr-overview)
- [Microsoft Dynamics 365 and GDPR](https://docs.microsoft.com/dynamics365/get-started/gdpr/index)
- [Microsoft Power BI GDPR white paper](https://powerbi.microsoft.com/blog/power-bi-gdpr-whitepaper-is-now-available/)

In the Diagnose experience for Fraud Protection, you can delete the offline data that you've uploaded. At the top of the page, select **Delete my data**.

In the Evaluate and Protect experiences, for all entities that contain personal data, you can perform the following tasks:

- Identify entities that contain personal data.
- Delete entities.
- Export entities.

## Manage data subject requests

On the left navigation bar, under **Data engineering**, select **Subject requests**. The **Search** tab provides the following selections to expedite your search:

- User.Email
- User.UserId
- Purchase.PurchaseId
- PaymentInstrument.PaymentInstrumentId

After you make your selection, if you require more specificity, you can use the search bar to enter keywords. From the search results, you can select either **Export user and associated data** or **Delete user and associated data**.

Select the **Requests** tab that identifies the following properties for your search:

- Request ID
- Request types (delete or export)
- Subject ID
- Statuses (pending or complete)
- Exported data links
