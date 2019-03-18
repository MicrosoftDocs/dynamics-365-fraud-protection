---
author: jegrif
description: Diagnose experience
ms.author: v-jegrif
ms.date: 02/28/2019
ms.service:
 - d365-fraud-protection
ms.topic: conceptual
title: Diagnose experience
---


# Diagnose experience

Microsoft Dynamics 365 Fraud Protection offers multiple experiences to introduce you to the product and accelerate your journey into full production. The *Diagnose* experience evaluates your own historical data and generates reports that provide valuable risk insights into existing fraud patterns in your business. These reports can identify opportunities to improve your fraud protection capabilities.

## Upload data

After signing in, upload your historical data for analysis. The data should reflect approved transactions that were previously provided to your bank, and should include three months of purchases and chargebacks. Upload CSV files for each of the following entities (maximum file size 10 GB each):

- Purchases 
- Payment instruments 
- Products 
- Chargebacks 

Follow the [required schemas](schema.md) to ensure the files can be properly interpreted by Dynamics 365 Fraud Protection.

You can preview a sample of your data on the “Ready to upload your file” screen. If significant errors are detected with the file format, refer to this example to correct them before uploading the complete files. When ready, select **Upload**.

After all four files are uploaded, select **Generate data diagnostic report** to begin creating your report. Generation typically takes no longer than 48 hours, and may be shorter depending on the size of your uploads.

## Data diagnostic report

The **Data diagnostic report** contains a detailed visual breakdown of your data to provide intelligence on the completeness of its content. Key metrics include the chargeback match rate, which charts purchase and chargeback completion and shows the optimum chargeback basis points for analysis. Additional charts indicate any missing dates, formatting errors, the percentage of unique entities represented, and how many days of data were included in your files.

To generate your risk diagnostic report, these aspects of your data must reach a minimum quality threshold. If the quality is too low to be accurately evaluated, you will be prompted to improve the indicated problems and try again.

## Risk diagnostic report
After the data diagnostic report returns satisfactory results, your **Risk diagnostic report** will generate. This process should take no longer than 24 hours.

The risk diagnostic report enables you to assess your risk from fraudulent activity and evaluate its monetary impact to your business. Based on your data, Dynamics 365 Fraud Protection provides interactive charts about the following:

- **Model performance**: With the Receiver Operating Characteristic curves, see the percentage of rejected transactions with chargebacks vs. the percentage of rejected legitimate transactions. Use the risk score slider to adjust the graphs and see what your detection and false positive rates would be at different thresholds of acceptable risk.
- **Distribution of transactions by risk score**: See the fraudulent to non-fraudulent ratio of your historical transactions, plotted out by their risk score. Zoom in on selected ranges for details.
- **Top five risk factors**: View the most common types of fraud occurring in your business. Choose what percent of your riskiest transactions to view.

## Review reports 
Find your completed reports in the navigation at **Data diagnostic report** and **Risk diagnostic report**, or link to them from the dashboard. For a deeper analysis, download the full report as a PDF file.
