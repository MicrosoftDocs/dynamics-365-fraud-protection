---
author: jegrif
description: This topic outlines the schemas that are required for signup status under account creation assessment.
ms.author: v-jegrif
ms.service: crm-online
ms.date: 09/04/2019

ms.topic: conceptual
title: View account creation assessment schemas -  Sign-up status
---

# View account creation assessment schemas - Sign-up status

This topic outlines the schemas for the Signup status data for account creation assessment. For Signup, see [this accompanying page](signp-schema.md).

Note the following formatting guidelines throughout:

- The files are in CSV UTF-8 (comma delimited) format (\*.csv).
- The maximum file size is 10 gigabytes (GB).
- The **DateTime** columns are in ISO 8601 format. For example, **DateTime.UtcNow.ToString("o")** might have the result **"2019-03-14T20:18:11.254Z"**.
- The decimal precision is two decimal places.
- The following characters are escaped in all columns: commas, new line characters, and multiline characters.

## SignupStatus schema

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| trackingID | string | The identifier of the SignupStatus event. |
| merchantLocalDate | DateTime | The Signup ingestion date in the merchant's time zone. The format is ISO 8601. |

## Data

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| signupId | string | The identifier of the Signup event. |

### Status

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| statusType | string | The type of status: APPROVED, REJECTED, or HELD. |
| statusDate | DateTime | The date and time when the status was applied. The format is ISO 8601. |
| reason | string | The reason for the status transition. |

### User

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| userId | string | The user identifier. This information is provided by the merchant. |

#### UserDetails \ PaymentInstrument \ PaymentInstrumentDetails

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| merchantPaymentInstrumentId | string | The identifier of the payment instrument. This information is provided by the merchant. |
