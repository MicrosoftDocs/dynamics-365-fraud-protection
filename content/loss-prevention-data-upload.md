---
author: josaw1
description: This article explains how to upload data for the loss prevention feature in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Upload historical data for loss prevention
---

# Upload historical data for loss prevention

[!include[deprecation](includes/deprecation.md)]

You can upload historical data from transactions, sales, payments, and payment methods into the system, so that the adaptive artificial intelligence (AI) models can look for anomalies. The historical data is processed and used to generate reports that show trends and anomalies. These reports provide actionable insights about any anomalies that the AI models detected.

The historical data must be imported from four entities:

* Transactions
* Sales
* Payments
* PaymentMethod

> [!IMPORTANT]
> This data is sensitive, and you should upload it only from a secure network location. Be aware that Microsoft requests only partial data about payment instruments (the bank identification number \[BIN\] and the last four digits). Microsoft doesn't request the full payment instrument number or Social Security number (SSN). Therefore, we recommend that you **exclude** this type of data from the files that you upload. For more information about how data is used and protected in Microsoft Dynamics 365 Fraud Protection, see [Security, compliance, and data subject requests](security-compliance.md).

## Website upload

You can upload your historical data from the **Loss prevention** tab of the **Data upload** page.

Follow these requirements and the [required schemas](./view-loss-prevent-schemas.md).

[!INCLUDE[data-upload-req](includes/data-upload-req.md)]

**To upload and process data files:**

1. In the left navigation, select **Data** > **Data upload**.
1. On the **Loss prevention** tab, select **Select data source**.
1. Select **Browse** and then select your CSV/TSV file.
1. If the file has no column headers, select the **This file doesn't include column headers** option. The system will automatically assign default column headers.
1. To begin data mapping, select **Next**, and then select the columns in your file that you want to map to each schema attribute.
1. In the data preview pane at the bottom of the page, confirm that the column mapping is correct.
1. When all the attributes are mapped, select **Save and close** to return to the **Data upload** page.
1. Select **Process data**.

You can save an incomplete mapping and then return to the **Loss prevention** tab later to complete it.

For related data types, such as purchase and account data, every file must be uploaded before you process the data.

**To upload additional data files:**

1. On the **Data upload** page, on the **Loss prevention** tab, select **Edit**.
1. Select **Change data source** to upload more files.
1. To apply the currently saved mapping to the newly uploaded file, select **Keep the current mapping**.
1. After mapping is completed, select **Save and close**.
1. On the **Data upload** page, select **Process data**.

Data processing might take up to a few hours, depending on the size of the file. You can check the status of data processing for each data source. If data processing encounters data errors, processing will fail, and the data import will be incomplete. Review the error file details, and fix the data issue that is noted. After you've finished fixing the issues, re-upload the file, remap the attributes if remapping is required, and retry data processing.

**To remove previously uploaded data files:**

- On the **Data upload** page, on the **Loss prevention** tab, select the files to remove, and then select **Delete**.

## API upload

During the evaluate and protect experiences, data can also be ingested through the API. A score will be returned for data that you upload in this way. For a more comprehensive overview of this process, see [Integrate Dynamics 365 Fraud Protection APIs](integrate-real-time-api.md).

## Download sample data

Before you use your internal data, you can download sample data and use it to explore Fraud Protection options.

**To download sample data:**

- Select [Loss prevention sample data file](https://download.microsoft.com/download/3/1/6/316b5f40-287d-48a3-ab3c-bf4c7a171cfc/LP1.zip).

## Connect to Dynamics 365 Commerce

In addition to uploading local files, you can connect to Dynamics 365 Commerce if this option is available to you. Note that when you connect to Commerce, all required data for Loss Prevention reports will automatically be imported and mapped. For more information, see [Loss prevention integration with Dynamics 365 Commerce](./loss-prevention-integration-with-commerce.md).


[!INCLUDE[footer-include](includes/footer-banner.md)]
