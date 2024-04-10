---
author: josaw1
description: This article explains how to upload historical data for Microsoft Dynamics 365 Fraud Protection.
ms.author:  josaw
ms.date: 04/10/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Upload historical data for purchase protection 
---

# Upload historical data for purchase protection 

In Microsoft Dynamics 365 Fraud Protection's evaluate and protect experiences, you can upload your purchase protection historical data into the system to help train and improve the accuracy of the machine learning models. The uploads can include data for purchases, chargebacks, merchant and bank decisions, and accounts.

For the best results, we recommend that you upload at least six months' worth of historical data.

If your Fraud Protection instance has multiple environments, data upload for each environment can be found by using the environment switcher. If the environment has child environments, the data that's uploaded will be processed in the environment that you selected.

## Data types

You can upload historical data through the Fraud Protection portal or the application programming interface (API).

**Entities:**

- Purchases

    - Purchases
    - Payment instruments
    - Products

- Purchase status
- Bank events
- Chargebacks
- Refunds
- Labels
- Account

    - Update accounts
    - Update account addresses
    - Update account payment instruments

> [!IMPORTANT]
> This data is sensitive, and you should take care to upload it only from a secure network location. Be aware that Microsoft requests only partial data about payment instruments (the bank identification number \[BIN\] and the last four digits). We don't request the full payment instrument number or Social Security number (SSN). We recommend that you **not** include this type of data in the files that you upload. For more information about how data is used and protected in Fraud Protection, see [Security, compliance, and data subject requests](security-compliance.md).

## Website upload

You upload your historical data on the **Purchase protection** tab of the **Data upload** page.

Follow these requirements and the [required schemas](view-purchase-protection-schemas.md):

[!INCLUDE[data-upload-req](includes/data-upload-req.md)]

**To upload and process data files:**

1. In the left navigation, select **Data** > **Data upload**.
1. On the **Purchase protection** tab, select **Select data source**.
1. Select **Browse** and then select your CSV/TSV file.
1. If the file has no column headers, select **This file doesn't include column headers**. The system automatically assigna default column headers.
1. Select **Next** to begin data mapping, and then select the columns in your file that you want to map to each schema attribute.
1. In the data preview pane at the bottom of the page, confirm that the column mapping is correct.
1. When all the attributes are mapped, select **Save and close** to return to the **Data upload** page.
1. Select **Process data**.

You can save an incomplete mapping and then return to the **Purchase protection** tab later to complete it.

For related data types, such as purchase and account data, every file must be uploaded before you process the data.

**To upload additional data files:**

1. On the **Data upload** page, on the **Purchase protection** tab, select **Edit**.
1. Select **Change data source** to upload more files.
1. To apply the currently saved mapping to the newly uploaded file, select **Keep the current mapping**.
1. After mapping is completed, select **Save and close**.
1. On the **Data upload** page, select **Process data**.

Data processing might take up to a few hours, depending on the size of the file. You can check the status of data processing for each data source. If data processing encounters data errors, processing will fail, and the data import will be incomplete. Review the error file details, and fix the data issue that is noted. After you've finished fixing the issues, re-upload the file, remap the attributes if remapping is required, and retry data processing.

**To remove previously uploaded data files:**

- On the **Data upload** page, on the **Purchase protection** tab, select the files to remove, and then select **Delete**.

## API upload

During the evaluate and protect experiences, data can also be ingested through the API. A score will be returned for data that you upload in this way. For a more comprehensive overview of this process, see [Integrate Dynamics 365 Fraud Protection APIs](integrate-real-time-api.md).

## Download sample data

Before you use your internal data, you can download sample data and use it to explore Fraud Protection options.

**To download sample data:**

- For samples you can use with loss prevention, select [Loss prevention sample data file](https://download.microsoft.com/download/3/1/6/316b5f40-287d-48a3-ab3c-bf4c7a171cfc/LP1.zip).
- For samples you can use with purchase protection, select [Purchase protection sample data file](https://download.microsoft.com/download/c/6/a/c6a37f61-1d4c-4357-8b3c-0a6d78bcb3a1/PP1.zip).



[!INCLUDE[footer-include](includes/footer-banner.md)]
