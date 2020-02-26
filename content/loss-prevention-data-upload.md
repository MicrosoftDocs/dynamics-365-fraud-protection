---
author: v-davido
description: This topic explains how to upload data for the loss prevention feature in Microsoft Dynamics 365 Fraud Protection.
ms.author: veganesa 
ms.service: fraud-protection
ms.date: 02/20/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Upload historical data for loss prevention
---

# Upload historical data for loss prevention

You can upload historical data from transactions, sales, payments, and payment methods into the system, so that the adaptive artificial intelligence (AI) models can look for anomalies. The historical data is processed and used to generate reports that show trends and anomalies. These reports provide actionable insights about any anomalies that the AI models detected.

The historical data must be imported from four entities:

* Transactions
* Sales
* Payments
* PaymentMethod

> [!IMPORTANT]
> This data is sensitive, and you should upload it only from a secure network location. Be aware that Microsoft requests only partial data about payment instruments (the bank identification number \[BIN\] and the last four digits). Microsoft doesn't request the full payment instrument number or Social Security number (SSN). Therefore, we recommend that you **exclude** this type of data from the files that you upload. For more information about how data is used and protected in Microsoft Dynamics 365 Fraud Protection, see [Security, compliance, and data subject requests](security-compliance.md).

## Website upload

You can upload your historical data from the **Data upload** page.

To ensure that Fraud Protection can correctly interpret the files that you upload, make sure that the files meet the following requirements, and that they follow the [required schemas](schema.md):

- To find and submit your local files, use the **Upload** button. After a successful upload, select **Generate Reports**. Every file must be uploaded before you process the data.
- To upload additional data, select **Reupload** to submit more files, and then process the new files. You can also select **Delete** to remove data files. 
