---
author: yvonnedeq
description: This topic explains how to upload data for the loss prevention feature in Microsoft Dynamics 365 Fraud Protection.
ms.author: v-madeq 
ms.service: fraud-protection
ms.date: 01/28/2020
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
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

You can upload your historical data from the **Loss prevention** tab on the **Data upload** page.

To ensure that Fraud Protection can correctly interpret the files that you upload, make sure that the files meet the following requirements, and that they follow the [required schemas](https://go.microsoft.com/fwlink/?linkid=2131494):

- The files are in CSV UTF-8 (comma delimited) format (\*.csv).
- The maximum file size is 10 gigabytes (GB).
- **DateTime** columns are in ISO 8601 format.
- The decimal precision is two decimal places.
- The following characters are escaped in all columns: commas, new line characters, and multiline characters.

**To browse and upload data files:**

1. On the left navigation, select **Data**, and then select **Data upload**.
1. On the **Data upload** page, select the **Loss prevention** tab, and then select **Select data source**. 
1. Select the file format type: **CSV** or **TSV**. 
1. If the file has no column headers, select the **This file doesn’t include column headers** option. 

   The system will automatically assign default column headers. 
   
1. To begin data mapping, select **Next**, and then select the columns in your file that you want to map to each schema attribute. 
1. In the data preview pane at the bottom of the page, confirm that the mapping is correct. 
1. When all the attributes are mapped, select **Save and close** to return to the **Data upload** page. 
1. Select **Process data**. 

  You can save an incomplete mapping and return to the **Loss prevention** tab later to complete it. 
  
  For related data types, such as purchase and account data, every file must be uploaded before you process the data.
  
**To upload additional data files:** 

1. On the **Data upload** page, select the **Loss prevention** tab, and then select **Edit**.
1. Select **Change data source** to upload more files. 
1. To apply the currently saved mapping to the newly uploaded file, select **Keep the current mapping**. 
1. After mapping is complete, select **Save and close**.
1. On the **Data upload** page, select **Process data**.
 
Data processing may take up to a few hours depending on the size of the file. You can check the status of data processing for each data source. 
If data processing encounters data errors, processing will fail, and the data import will be incomplete. Review the error file details and fix the noted data issue. After fixing the issues, re-upload the fixed file, re-map the attributes if needed, and retry data processing. 

**To remove previously uploaded data files:**
- On the **Loss prevention** tab in the **Data upload** page, select the files you want to remove, and then select **Delete**.


## API upload

Data can also be ingested through the AP during the evaluate and protect experiences. A score will be returned for data that you upload in this way. For a more comprehensive overview of this process, see [Integrate Dynamics 365 Fraud Protection APIs](integrate-real-time-api.md).

## Download sample data
You can download  sample data and use this data to explore Fraud Protection options before using your internal data.

**To download sample data:**
- Select [sample data file](https://download.microsoft.com/download/c/6/a/c6a37f61-1d4c-4357-8b3c-0a6d78bcb3a1/DFP_External_Sample_Data.zip).  

## Connect to Dynamics 365 Commerce

In addition to uploading local files, you can connect to Dynamics 365 Commerce if this is an option available to you. Note that connecting to Dynamics 365 Commerce will automatically import and map all required data for Loss Prevention reports. For more information, see [Loss prevention integration with Dynamics 365 Commerce](https://go.microsoft.com/fwlink/?linkid=2131495).

