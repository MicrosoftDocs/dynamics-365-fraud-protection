---
author: v-davido
description: This topic explains how to upload data for Microsoft Dynamics 365 Fraud Protection Loss Prevention system.
ms.author: v-davido
ms.service: fraud-protection
ms.date: 01/28/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Upload historical data
---

# Upload historical data

In the loss prevention add-in to Microsoft Dynamics 365 Fraud Protection, you upload your historical data into the system to be processed. These uploads include data from transactions, sales, and payments. This historical data is processed and used to generate reports illustrating trends and any anomalies. There are four entities from which the data needs to be imported:

* Transactions
* Sales
* Payments
* PaymentMethod



> [!IMPORTANT]
> This data is sensitive, and you should take care to upload it only from a secure network location. Be aware that Microsoft requests only partial data about payment instruments (the bank identification number \[BIN\] and the last four digits). We don't request the full payment instrument number or Social Security number (SSN). We recommend that you do **not** include this type of data in the files that you upload. For more information about how data is used and protected in Fraud Protection, see [Security, compliance, and data subject requests](security-compliance.md).

## Website upload

You can upload your historical data from the **Data upload** page.

To help guarantee that Fraud Protection can correctly interpret the files that you upload, make sure that they meet the following requirements, and that they follow the [required schemas](schema.md):

- The files are in CSV UTF-8 (comma delimited) format (\*.csv).
- The maximum file size is 10 gigabytes (GB).
- The **DateTime** columns are in ISO 8601 format.
- The decimal precision is two decimal places.
- The following characters are escaped in all columns: commas, new line characters, and multiline characters.

Use the **Upload** button to find and submit your local files. After a successful upload, select **Process**. For related data types, such as purchase and account data, every file must be uploaded before you process the data.

To upload additional data, select **Reupload** to submit more files, and then process the new files.
