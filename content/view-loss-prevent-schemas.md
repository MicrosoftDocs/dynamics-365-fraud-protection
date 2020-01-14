---
author: v-davido
description: This topic outlines the requred schema for the loss prevention API.
ms.author: v-davido
ms.service: fraud-protection
ms.date: 01/14/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin

title: View loss prevention schema
---

# View loss prevention schema

This topic outlines the schema for the loss prevention API.

Note the following formatting guidelines throughout:

- The files are in CSV UTF-8 (comma delimited) format (\*.csv).
- The maximum file size is 10 gigabytes (GB).
- The **DateTime** columns are in ISO 8601 format. For example, **DateTime.UtcNow.ToString("o")** might have the result **"2019-03-14T20:18:11.254Z"**.
- The decimal precision is two decimal places.
- The following characters are escaped in all columns: commas, new line characters, and multiline characters.

## Transaction Staging

| Attribute | Type | Description |
| --- | --- | --- |
| trackingId | string | The identifier of the Signup event. |

## Transaction Sales Line Staging

| Attribute | Type | Description |
| --- | --- | --- |
| trackingId | string | The identifier of the Signup event. |

## Transaction Payment Line Staging

| Attribute | Type | Description |
| --- | --- | --- |
| trackingId | string | The identifier of the Signup event. |

## Payment Method

| Attribute | Type | Description |
| --- | --- | --- |
| trackingId | string | The identifier of the Signup event. |

## Transaction Staging

| Attribute | Type | Description |
| --- | --- | --- |
| trackingId | string | The identifier of the Signup event. |


