---
author: jegrif
description: This topic explains how to upload historical data for Microsoft Dynamics 365 Fraud Protection.
ms.author: v-jegrif
ms.service: crm-online
ms.date: 07/17/2019

ms.topic: conceptual
title: Upload historical data
---

# Upload historical data

In the Evaluate and Protect experiences in Microsoft Dynamics 365 Fraud Protection, you upload your historical data into the system to help increase the accuracy of your risk decisions. These uploads include data for purchases, chargebacks, merchant and bank decisions, and accounts. This historical data helps accelerate the process of priming the machine learning model and can help improve the handling of your future transactions.

## Data types

Dynamics 365 Fraud Protection can analyze historical data about the following entities. This data can be uploaded through either the website or the application programming interface (API). In the Evaluate and Protect experiences, we recommend that you upload at least six months of data. Any chargeback data that is submitted should correspond directly to the purchase data that is uploaded.

- Purchase data

    - Purchases
    - Payment instruments
    - Products

- Chargebacks
- Refunds
- Purchase status
- Bank events
- Account data

    - Update accounts
    - Update account addresses
    - Update account payment instruments

> [!IMPORTANT]
> This data is sensitive, and you should take care to upload it only from a secure network location. Be aware that Microsoft requests only partial data about payment instruments (the bank identification number \[BIN\] and the last four digits). We don't request the full payment instrument number or Social Security number (SSN). We recommend that you do **not** include this type of data in the files that you upload. For more information about how data is used and protected in Dynamics 365 Fraud Protection, see [Security, compliance, and data subject requests](security-compliance.md).

## Website upload

You can upload your historical data from the **Data upload** page.

To help guarantee that Dynamics 365 Fraud Protection can correctly interpret the files that you upload, make sure that they meet the following requirements, and that they follow the [required schemas](schema.md):

- The files are in CSV UTF-8 (comma delimited) format (\*.csv).
- The maximum file size is 10 gigabytes (GB).
- The **DateTime** columns are in ISO 8601 format.
- The decimal precision is two decimal places.
- The following characters are escaped in all columns: commas, new line characters, and multiline characters.

Use the **Upload** button to find and submit your local files. After a successful upload, select **Process**. For related data types, such as purchase and account data, every file must be uploaded before you process the data.

To overwrite a previous upload with new data, select **Reupload** to submit the new files, and then process the updated data.

## API upload

In the Evaluate and Protect experiences, data can also be ingested through the API. A risk score will be returned for data that you upload in this way. For a more comprehensive overview, see [Integrate Dynamics 365 Fraud Protection APIs](integrate-real-time-api.md).
