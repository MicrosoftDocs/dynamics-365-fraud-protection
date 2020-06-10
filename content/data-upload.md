---
author: v-davido
description: This topic explains how to upload historical data for Microsoft Dynamics 365 Fraud Protection.
ms.author: veganesa 
ms.service: fraud-protection
ms.date: 06/10/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Upload historical data
---

# Upload historical data

In the evaluate and protect experiences in Microsoft Dynamics 365 Fraud Protection, you upload your loss prevention historical data into the system to help increase the accuracy of your purchase protection. These uploads include data for purchases, chargebacks, merchant and bank decisions, and accounts. This historical data helps accelerate the process of priming the machine learning model and can help improve the handling of your future transactions.

## Data types

Fraud Protection can analyze loss prevention historical data about several entities. This data can be uploaded through either the website or the application programming interface (API). We recommend that you upload at least six months of data. Any chargeback data that is submitted should correspond directly to the purchase data that is uploaded.

**Entities:**

- Purchase data

    - Purchases
    - Payment instruments
    - Products

- Chargebacks
- Labels
- Refunds
- Purchase status
- Bank events
- Account data

    - Update accounts
    - Update account addresses
    - Update account payment instruments

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

## API upload

In the Evaluate and Protect experiences, data can also be ingested through the API. A score will be returned for data that you upload in this way. For a more comprehensive overview, see [Integrate Dynamics 365 Fraud Protection APIs](integrate-real-time-api.md).

## Download sample data
We have sample data for download: [sample data file](https://download.microsoft.com/download/c/6/a/c6a37f61-1d4c-4357-8b3c-0a6d78bcb3a1/DFP_External_Sample_Data.zip). You can use this to explore options before using your own internal data. 
