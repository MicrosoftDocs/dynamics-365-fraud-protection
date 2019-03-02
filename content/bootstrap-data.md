---
author: jegrif
description: Bootstrap and manage historical data
ms.author: v-jegrif
ms.date: 03/01/2019
ms.service:
 - d365-fraud-protection
ms.topic: conceptual
title: Bootstrap and manage historical data
---


# Bootstrap and manage historical data

To analyze your past transactions and tune machine learning to your business scenarios, upload your historical data into Microsoft Dynamics 365 Fraud Protection.

## Gather your data

The files required vary depending on the Dynamics 365 Fraud Protection experience you have chosen. In the Diagnose experience, upload your purchase and chargeback data to generate diagnostic reports about your business’ past transactions. In Experience and Protect, add refund, bank event, account update, and purchase status files for a more comprehensive analysis. 

Files must be in CSV format and be no larger than 10 GB. Follow the [required schemas](schema.md) for each of the following entities: 

- **All experiences**: Purchase, Purchase_PaymentInstruments, Purchase_Products, Chargebacks
- **Experience and Protect experiences**: Refund, PurchaseStatus, BankEvents, UpdateAccount, UpdateAccount_Address, UpdateAccount_PaymentInstruments


## Upload data

The basic data upload procedure is shared for all experiences.

Select **Data upload** to begin uploading each of your required files. After submitting, preview a sample of your data on the “Ready to upload your file” screen. If significant errors are detected with the file format, refer to this example to correct them before uploading the complete files. When ready, select **Upload**. 
