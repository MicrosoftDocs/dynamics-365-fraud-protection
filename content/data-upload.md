---
author: jegrif
description: Upload historical data
ms.author: v-jegrif
ms.date: 03/01/2019
ms.service:
 - d365-fraud-protection
ms.topic: conceptual
title: Upload historical data
---


# Upload historical data

In the Evaluate and Protect experiences of Dynamics 365 Fraud Protection, upload your historical data into the system to help increase the accuracy of your risk decisions. These uploads include purchase, chargeback, merchant and bank decisions, and account data. Using this historical data accelerates the process of priming our machine learning model and can improve the handling of your future transactions. 

## Data types

Historical data about the following entities can be analyzed by Dynamics 365 Fraud Protection, and can be uploaded either through the website or via API. In Evaluate and Protect, at least six months of data are recommended. Any chargeback data submitted should correspond directly to your uploaded purchase data.

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

> [!NOTE] 
> Note that this data is sensitive, and you should take every care to upload it only from a secure network location. Please be aware that we only request partial payment instrument data (BIN and last 4 digits). We do not request highly sensitive data such as full payment instrument number or SSN, so ensure that you do not include such data in the uploaded files. For more information on how data is utilized and protected in Dynamics 365 Fraud Protection, see [Security, compliance, and data subject requests](security-compliance.md). 

## Website upload

Your historical data can be uploaded directly through the **Data upload** page.

Each of your files must meet these requirements and should follow the [required schemas](schema.md) to ensure the files can be properly interpreted by Dynamics 365 Fraud Protection. 

- CSV (comma separated) format 
- Maximum file size: 10 GB 
- DateTime columns in ISO 8601 
- Decimal precision up to 2 places 
- Characters to be escaped: commas, new line characters, and multi-line characters in all columns

Use the **Upload** button to find your local file and submit it. After a successful upload, select **Process**. For related data types, like Purchase and Account, each individual file must be uploaded before processing the data. 

## API upload

In Evaluate and Protect, data can also be ingested through the API. Data uploaded in this manner will additionally return a risk score. For a more comprehensive overview, see [Send real-time data using APIs](send-real-time-api.md). 
