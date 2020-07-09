---
author: jegrif
description: This topic provides a description of the required schema for the fraud label API.

ms.author: v-jegrif
ms.service: fraud-protection
ms.date: 09/04/2019

ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin

title: View the schema for the labels API
---

# View the schema for the labels API

This topic outlines the schema for the labels API.

## Formatting guidelines

Note the following formatting guidelines throughout:

- The files are in CSV UTF-8 (comma delimited) format (\*.csv).
- The maximum file size is 10 gigabytes (GB).
- The **DateTime** columns are in ISO 8601 format. For example, **DateTime.UtcNow.ToString("o")** might have the result **"2019-03-14T20:18:11.254Z"**.
- The decimal precision is two decimal places.
- The following characters are escaped in all columns: commas, new line characters, and multiline characters.

## Attributes

| Attribute | Type | Description |
| --- | --- | --- |
| TrackingId | String | The unique ID for each event/record. |
| MerchantLocalDate | DateTime | The date in the merchant&#39;s time zone. The format is ISO 8601.  |
| EventTimeStamp | DateTime | The date and time of the event. Possible values: Chargeback Date or Review Date. The format is ISO 8601. |
| LabelObjectType | String | This field indicates the type of label: Purchase, Signup, Custom Fraud Evaluation, Account, Payment instrument, or Email. |
| LabelObjectId | String | This is an identifier field for the type of object: PurchaseId, SignupId, UserId, MerchantPaymentInstrumentId, or Email.  |
| LabelSource | String | This field represents the source of the label: Customer Escalation, Chargeback, TC40_SAFE, Manual Review, Refund, Offline Analysis. |
| LabelState | String | This field indicates the current status of the label: Inquiry Accepted, Fraud, Disputed, Reversed, Abuse, or Resubmitted Request.  |
| LabelReasonCodes | String | This field indicates the reason codes associated with each type of label: Processor/Bank Response Code, Fraud Refund, Account TakeOver, Payment Instrument Fraud, Account Fraud, Abuse, or Friendly Fraud. |
| Processor | String | The name of the bank or payment processor that is generating the TC40 or SAFE information. |
| EffectiveStartDate | DateTime | The date from which this label is effective. The format is ISO 8601. |
| EffectiveEndDate | DateTime | The end date for this label. The format is ISO 8601. |
