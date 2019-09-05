---
author: jegrif
description: This topic outlines the requred schema for the fraud label API.
ms.author: v-jegrif
ms.service: crm-online
ms.date: 09/04/2019

ms.topic: conceptual
title: View fraud label schema
---

# View fraud label schema

This topic outlines the schema for the fraud label API.

Note the following formatting guidelines throughout:

- The files are in CSV UTF-8 (comma delimited) format (\*.csv).
- The maximum file size is 10 gigabytes (GB).
- The **DateTime** columns are in ISO 8601 format. For example, **DateTime.UtcNow.ToString("o")** might have the result **"2019-03-14T20:18:11.254Z"**.
- The decimal precision is two decimal places.
- The following characters are escaped in all columns: commas, new line characters, and multiline characters.

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| trackingId | String | The unique ID for each event/record. |
| merchantLocalDate | DateTime | The date in the merchant&#39;s time zone. The format is ISO 8601.  |
| eventTimeStamp | DateTime | The date and time of the event. Examples: chargeback date, review date. The format is ISO 8601. |
| LabelObjectType | String | Examples: Purchase, Signup, User, UserEmail, PI   |
| LabelObjectId | String | Examples: PurchaseId, SignupId, UserId, MerchantPaymentInstrumentId, Email   |
| LabelSource | String | Examples: Chargeback, TC40, SAFE, Manual Review, Offline Analysis, Customer Escalation, Other   |
| LabelState | String | For Chargeback, the possible values are Enquiry, Received, Accepted, Disputed, Reversed, or ChargebackAfterReversal. For all others, the possible values are Fraud, Bad, Reversed, or Empty Value.  |
| LabelReasonCodes | String | For Chargeback/TC40/SAFE send Processor/Bank Reason Codes, Fraud Refund/Account Take Over/PI Fraud/Account Fraud/Abuse/Friendly Fraud/Empty Value   |
| Processor | String | Required to understand the Bank/Processor Reason codes. |
| EffectiveStartDate | DateTime | The date from which this fraud label is effective. This is mainly used if account or PI is the fraud identifier. The format is ISO 8601. |
| EffectiveEndDate | DateTime | The end date for this fraud label. This is mainly used if account or PI is the fraud identifier. The format is ISO 8601.    |
