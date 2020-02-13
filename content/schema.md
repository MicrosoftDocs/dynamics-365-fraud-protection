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



## **AccountLog**** I ****i**** n**

AccountLogIncontains information and context about an incoming log-in event for a risk assessment.

The following schemas are used in the Evaluate and Protect experiences.



**AccountLog**** In ****ina**** Status**

AccountLogInStatus contains information and context about the status of an account log-in event. This is a data ingestion event only.

The following schemas are used in the Evaluate and Protect experiences.



**AccountUpdate**

AccountUpdate contains account information updates, for example, edited/addeduser profile, address, payment Instrument, phone, email and single sign-on (SSO). This is a data ingestion event only.

The following schemas are used in the Evaluate and Protect experiences.



**Label**

Labels API contains the additional knowledge for model training based on an additional set of fraud signals.This is a data ingestion event only.

The following schemas are used in the Evaluate and Protect experiences.

