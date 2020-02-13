---
author: v-davido
description: Test of ap schema tables2
ms.author: v-davido
ms.service: fraud-protection
ms.date: 01/14/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: View account protection schemas

---

# View account protection schemas

This topic outlines the schemas for historical data that is bulk-uploadedpassed into Microsoft Dynamics 365 Fraud Protection as comma-separated values (CSV) files. For information about the upload procedure, see [Upload historical data](https://docs.microsoft.com/en-us/dynamics365/fraud-protection/data-upload). If data will be ingested via the application programming interface (API), see [Integrate Dynamics 365 Fraud Protection real-time APIs](https://docs.microsoft.com/en-us/dynamics365/fraud-protection/integrate-real-time-api).

Note the following formatting guidelines throughout:

- The files are in CSV UTF-8 (comma delimited) format (\*.csv).
- The maximum file size is 10 gigabytes (GB).
- The  **DateTime**  columns are in ISO 8601 format. For example, **DateTime.UtcNow.ToString(&quot;o&quot;)** might have the result  **&quot;2019-03-14T20:18:11.254Z&quot;**.
- The decimal precision is two decimal places.
- The following characters are escaped in all columns: commas, new line characters, and multiline characters.

## **AccountCreation**

AccountCreationAPI schema contains information and context about an incoming new account creation event for a risk assessment.

The following schemas are used in the Evaluate, andEvaluate and Protect experiences.


**AccountCreationStatus**

AccountCreationStatus contains information and context about the status of an account creation event. This is a data ingestion event only.

The following schemas are used in the Evaluate and Protect experiences.



## **AccountLogin**

AccountLogIn contains information and context about an incoming login event for a risk assessment.

The following schemas are used in the Evaluate and Protect experiences.



**AccountLogInStatus**

AccountLogInStatus contains information and context about the status of an account login event. This is a data ingestion event only.

The following schemas are used in the Evaluate and Protect experiences.



**AccountUpdate**

AccountUpdate contains account information updates, for example: edited/addeduser profile, address, payment Instrument, phone, email and single sign-on (SSO). This is a data ingestion event only.

The following schemas are used in the Evaluate and Protect experiences.



**Label**

Labels API contains the additional knowledge for model training based on an additional set of fraud signals.This is a data ingestion event only.

The following schemas are used in the Evaluate and Protect experiences.
| Category | Attribute          | Type     | Description                                                                                                                                                                                                                                                          |
|----------|--------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| N/A      | Name               | string   | "AP\.AccountLabel"                                                                                                                                                                                                                                                   |
| N/A      | Version            | string   | "0\.5"                                                                                                                                                                                                                                                               |
| MetaData | TrackingId         | String   | The unique ID for each event/record\.                                                                                                                                                                                                                                |
| MetaData | merchantTimeStamp  | DateTime | The date in the merchant's time zone\. The format is ISO 8601\.                                                                                                                                                                                                      |
| MetaData | userId             | string   | The user identifier\. This information is provided by the merchant\.                                                                                                                                                                                                 |
| Label    | EventTimeStamp     | DateTime | The date and time of the event\. Possible values: Chargeback Date or Review Date\. The format is ISO 8601\.                                                                                                                                                          |
| Label    | LabelObjectType    | String   | This field indicates the type of label: Purchase, Account Creation, Account Login, Account Update, Custom Fraud Evaluation, Account, Payment instrument, or Email\.                                                                                                  |
| Label    | LabelObjectId      | String   | This is an identifier field for the object: PurchaseId, AccountCreationId, AccountLoginId, AccountUpdateId, UserId, MerchantPaymentInstrumentId, or Email\.                                                                                                          |
| Label    | LabelSource        | String   | This field represents the source of the label: Customer Escalation, Chargeback, TC40\_SAFE, Manual Review, Refund, Offline Analysis, Account Protection Review                                                                                                       |
| Label    | LabelState         | String   | This field indicates the current status of the label: Inquiry Accepted, Fraud, Disputed, Reversed, Abuse, Resubmitted Request, AccountCompromised, AccountNotCompromised                                                                                             |
| Label    | LabelReasonCodes   | String   | This field indicates the reason codes associated with each type of label: Processor/Bank Response Code, Fraud Refund, Account TakeOver, Payment Instrument Fraud, Account Fraud, Abuse, Friendly Fraud, Account Credentials Leaked, Passed Account Protection Checks |
| Label    | Processor          | String   | The name of the bank or payment processor that is generating the TC40 or SAFE information\.                                                                                                                                                                          |
| Label    | EffectiveStartDate | DateTime | The date from which this label is effective\. The format is ISO 8601\.                                                                                                                                                                                               |
| Label    | EffectiveEndDate   | DateTime | The end date for this label\. The format is ISO 8601\.                                                                                                                                                                                                               |

