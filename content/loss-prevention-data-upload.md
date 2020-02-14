---
author: v-davido
description: This topic explains how to upload data for Microsoft Dynamics 365 Fraud Protection Loss Prevention system.
ms.author: v-davido
ms.service: fraud-protection
ms.date: 02/14/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Upload historical data
---

# Upload historical data

You can upload the historical data into the system for the adaptive AI models to detect anamalies and generate reports that will provide actionable insights on the anamolies detected . These uploads include data from transactions, sales, payments and payment methods. This historical data is processed and used to generate reports illustrating trends and anomalies. There are four entities from which the data needs to be imported:

* Transactions
* Sales
* Payments
* PaymentMethod



> [!IMPORTANT]
> This data is sensitive, and you should take care to upload it only from a secure network location. Be aware that Microsoft requests only partial data about payment instruments (the bank identification number \[BIN\] and the last four digits). We don't request the full payment instrument number or Social Security number (SSN). We recommend that you do **not** include this type of data in the files that you upload. For more information about how data is used and protected in Fraud Protection, see [Security, compliance, and data subject requests](security-compliance.md).

## Website upload

You can upload your historical data from the **Data upload** page.

To help guarantee that Fraud Protection can correctly interpret the files that you upload, make sure that they meet the following requirements, and that they follow the [required schemas](schema.md):

Use the **Upload** button to find and submit your local files. After a successful upload, select **Generate Reports**. Every file must be uploaded before you process the data.

To upload additional data, select **Reupload** to submit more files, and then process the new files. You can also select **Delete** to remove any data files. 
