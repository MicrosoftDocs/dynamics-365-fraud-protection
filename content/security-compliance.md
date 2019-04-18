---
author: jackwi111
description: Security, compliance, and data subject requests
ms.author: v-jowigh
ms.service: crm-online
ms.date: 02/25/2019

ms.topic: conceptual
title: Security, compliance, and data subject requests
---


# Security, compliance, and data subject requests

Microsoft runs on trust. Dynamics 365 Fraud Protection is built upon the four Microsoft Trusted Cloud foundational principles: security, privacy, compliance, and transparency. Microsoft safeguards your business knowledge as if it were our own.
For additional resources, see the following documents:

- [Microsoft Trust Center](https://www.microsoft.com/en-us/trustcenter/default.aspx)

- [Microsoft Runs on Trust](https://www.microsoft.com/en-us/legal/compliance/integrity)

## Data subject requests

Dynamics 365 Fraud Protection provides tools to help you comply with requests from your customers (data subjects) to export or delete their personal data.

For additional resources, see the following documents:

- [Data Subject Requests](https://docs.microsoft.com/en-us/microsoft-365/compliance/gdpr-data-subject-requests)

- [Safeguarding individual privacy rights with the Microsoft Cloud](https://www.microsoft.com/en-us/trustcenter/privacy/gdpr/gdpr-overview)

- [Microsoft Dynamics 365 and GDPR](https://docs.microsoft.com/en-us/dynamics365/get-started/gdpr/index)

- [Microsoft Power BI GDPR Whitepaper](https://powerbi.microsoft.com/en-us/blog/power-bi-gdpr-whitepaper-is-now-available/)

In the Dynamics 365 Fraud Protection Diagnose experience, you can delete the offline data you have uploaded into Dynamics 365 Fraud Protection. Under **Upload data**, for **Transactions**, **Payment Instruments**, **Products**, or **Chargebacks**, select the vertical ellipsis, and then select **Delete**. Alternatively, at the top of the screen, select **Delete my data**.

In the Evaluate and Protect experiences, for all entities containing personal data, you can:

- Identify these entities.

- Delete entities.

- Export entities.

## How to use data subject requests

From the left navigation bar, under **Data engineering**, select **Subject requests**. The **Searc** tab provides the following selections to expedite your search:

- User.Email

- User.UserId

- Purchase.PurchaseId

- PaymentInstrument.PaymentInstrumentId

After making your selection, for more specificity, use the Search bar to enter keywords. From your search results, you can either **Export user and associated data** or **Delete user and associated data**.

Select the **Request** tab that identifies these properties for your particular search:

- Request IDs

- Request types (delete or export)

- Statuses (pending or complete)

- Exported data links
