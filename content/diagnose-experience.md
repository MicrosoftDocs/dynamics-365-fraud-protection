---
author: yvonnedeq
description: This topic provides information about the diagnose experience in Microsoft Dynamics 365 Fraud Protection.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 10/23/2020
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: The diagnose experience in Fraud Protection

---

# The diagnose experience in Fraud Protection

Microsoft Dynamics 365 Fraud Protection's *Diagnose experience* evaluates your historical data and generates reports that provide valuable risk insights into existing fraud patterns in your business. These reports can help you identify opportunities for improving your fraud protection capabilities.


## Upload data

To begin your diagnose experience, upload your historical data for analysis. Your data files should reflect approved transactions that were approved by you (the merchant) and sent to your bank.

To help guarantee that Fraud Protection can interpret the files that you upload, make sure that they meet the following requirements.

### Data requirements
- Upload files for each of these entities: Purchases, Payment instruments, Products, and Chargebacks.
- The files must include at least 100,000 transactions, 4,000 chargebacks, and 30 days of data. We recommend three months of data.
- The chargeback data should correspond directly to the purchase data. For the best results, there should be at least 5 chargebacks associated with every 100 purchases.

### Format requirements
- The files must be in CSV (comma-separated values) format and follow the [required schemas](schema.md).
- The maximum file size is 10 gigabytes (GB).
- The DateTime columns are in ISO 8601 format.
- The decimal precision is two decimal places.
- The following characters should be escaped in all columns: commas, new line characters, and multiline characters.

> [!IMPORTANT]
> This data is sensitive, and you should take care to upload it only from a secure network location. Be aware that Microsoft requests only partial data about payment instruments (the bank identification number \[BIN\] and the last four digits). We don't request the full payment instrument number or Social Security number (SSN). We recommend that you do **not** include this type of data in the files that you upload. For more information about how data is used and protected in Fraud Protection, see [Security, compliance, and data subject requests](security-compliance.md).

## Generate reports

1. In the left navigation, select **Purchase**, and then select **Diagnose**. 
1. When you're ready to upload the data, select **Upload Data**.

    After all four data files (Purchases, Payment instruments, Products, and Chargebacks) are uploaded, you can start to generate reports.

1. To generate a report, select **Generate reports**. 

    Typically, report generation takes no longer than 24 hours. However, it might take more or less time, depending on the size of your files.

### Data diagnostic report

The *data diagnostic report* contains a detailed visual breakdown of your data, so that you can determine how complete the content is. Key metrics include the chargeback match rate, which shows purchase and chargeback completion, and the optimum baseline chargeback basis points for analysis. Additional charts indicate any missing dates, formatting errors, the percentage of unique entities that are represented, and the number of days of data that were included in the uploaded files.

Before you can generate your risk diagnostic report, the key metrics of your data must reach a minimum quality threshold. If the quality of the data is too low to allow for accurate evaluation, you will be prompted to improve the indicated issues and try again. 

#### To upload updated data:
1. Return to the **Diagnose** page.
2. To submit your updated data, select **Upload data**.
 
### Risk diagnostic report

After the data diagnostic report returns satisfactory results, the *risk diagnostic report* is generated. This process should take no longer than 24 hours.

The risk diagnostic report lets you assess your risk from fraudulent activity and evaluate its monetary impact on your business. Based on your data, Fraud Protection provides interactive charts for the following information:

- **Model performance** – The **Receiver operating characteristic** curves let you see the percentage of rejected transactions that have chargebacks versus the percentage of rejected legitimate transactions. By using the **risk score** slider to adjust the graphs, you can see what your detection and false positive rates would be at different thresholds of acceptable risk.
- **Distribution of transactions by risk score** – See the reported ratio of fraudulent to non-fraudulent historical transactions. The transactions are plotted based on their risk score. You can zoom in on selected ranges to see details.
- **Top 5 risk factors** – See the top risk factors for transactions that have the highest risk scores. Use the drop-down menu to select the percentage of your transactions to view.

## Review reports

You can review your completed data diagnostic and risk diagnostic reports in Fraud Protection. Depending on the type of report you want to review: 

1. Select **Purchase**, and then, on the **Diagnose** tab, view the risk report.
1. To review the data diagnostic report, select **Check data quality**.
1. For deeper analysis and additional information, download the full reports as .docx files.
