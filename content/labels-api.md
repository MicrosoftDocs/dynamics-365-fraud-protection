---
author: josaw1
description: This article explains how the labels API enables you to send information to the virtual fraud analyst and monitoring dashboards in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 07/29/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Labels API
ms.custom: 
---

# Labels API

This article explains how the labels API enables you to send information to the reporting and monitoring dashboards in Microsoft Dynamics 365 Fraud Protection.

The labels API enables you to send fraud or non-fraud signals to Fraud Protection. This data is used for model training, model performance evaluation, and reporting. The labels API is a general API that labels assessment events by using either individual transaction or event IDs, or entities such as user or payment instrument.

## Common label scenarios for transactions or events

- Any fraudulent transactions that are escalated by your customers
- Fraudulent activity or account abuse that is identified by your review team
- Any offline analysis (such as behavior analysis or discovered connections to existing fraud cases)
- TC40/SAFE signals that are received
- Reversal of a previous fraud signal after it's identified as non-fraud based on the latest available information
- Chargebacks/refunds that are received
- Chargeback reversal after a dispute
 
We recommend that you use the chargeback and refund API to provide information that is related to chargebacks and refunds. For more information about supported events, see [Dynamics 365 Fraud Protection Service](https://go.microsoft.com/fwlink/?linkid=2084942).

## Account or payment instrument details 

- Fraudulent account or payment instrument information that is identified by your review team
- Account takeover scenarios that are escalated by your customers

## API Schema

| Attribute | Type | Description | 
|-----------|------|-------------|
| labelObjectType | <p>Enum</p><p>Expected values: PURCHASE, ACCOUNTCREATION, ACCOUNTLOGIN, ACCOUNT, PI, EMAIL</p> | This attribute indicates how extensively you want to flag a label. For example, you might want to mark a single transaction as fraudulent, or you might want to mark all a user account's transactions as fraudulent. Depending on the object type, Fraud Protection flags related transactions or events as fraud or non-fraud. For example, if the **labelObjectType** value is **PURCHASE**, **ACCOUNTCREATION**, or **ACCOUNTLOGIN**, Fraud Protection labels specific transactions. If the value is **ACCOUNT** or **PI**, Fraud Protection flags all the transactions that are related to the user account or payment instrument. |
| labelObjectId | String | <p>The identifier that corresponds to the value of the **labelObjectType** attribute. Fraud Protection uses this value to find related transactions and events. The IDs of the label object types are as follows:</p><ul><li>**PURCHASE:** purchaseId</li><li>**ACCOUNTCREATION:** signupId</li><li>**ACCOUNTLOGIN:** loginId</li><li>**ACCOUNT:** userId</li><li>**PI:** merchantPaymentInstrumentId</li></ul><p>This attribute is very important, because Fraud Protection uses it to identify the original assessment event. Therefore, the value must match the original transaction or event ID.</p> |
| labelSource | String | The source of label information. Some suggested values are **ManualReview** if a fraud label is identified by the review team, and **CustomerEscalation** if a customer complains about a falsely rejected transaction (in other words, a false positive). TC40/SAFE data is another source for label data. |
| isFraud | Boolean | This attribute indicates whether the label is fraud or non-fraud. If no value is provided, Fraud Protection uses **true** as the default value. |
| reasonText | String | The reason for labeling something fraud or non-fraud. You can safely ignore reasons if you have limited information about your label sources. Alternatively, depending on your label workflows, you can map some scenarios to some of these values. |
| labelReasonCodes | String | <p>Normalized reason codes or reason codes that are received from the payment processor. You can safely ignore this attribute if you don't have reason details.</p><p>Some suggested values are **Processor Response Code**, **Bank Response Code**, **Fraud Refund**, **Account Takeover**, **Payment Instrument Fraud**, **Account Fraud**, **Abuse**, **Friendly Fraud**, **Account Credentials Leaked**, and **Passed Account Protection Checks**.</p> |
| labelState | String | The kind of label that you're sending. This attribute is used especially if you're reversing a previous fraud signal or false positive. In both cases, you'll set **isFraud** to **false**. However, the state can help identify false positive labels. |
| Processor | String | The name of the payment processor. |
| eventTimeStamp | DateTime (ISO 8601 format) | The label-identified timestamp. If the API is integrated directly with the label detection process, and you call the label API as soon as a review agent flags a transaction as fraud, the value can be the current timestamp. This value is especially important for determining the order of events when there are multiple labels. For example, if a purchase or account creation transaction is labeled as fraud but is later labeled as non-fraud, Fraud Protection will refer to this value to determine which of the two labels is more recent and therefore correct. |
| effectiveStartDate | DateTime (ISO 8601 format) | The effective start and end dates are intended to enrich labels that are wider than one transaction (and that usually have a **labelObjectType** value of **ACCOUNT**) to limit the impact of those labels to a specific timeframe. For example, in account compromise scenarios, these dates specify the timeframe that you want to label the transactions or events in. |
| effectiveEndDate | DateTime (ISO 8601) format | The effective start and end dates are intended to enrich labels that are wider than one transaction (and that usually have a **labelObjectType** value of **ACCOUNT**) to limit the impact of that label to a specific timeframe. For example, in account compromise scenarios, these dates specify the timeframe that you want to label the transactions or events in. |
| Amount | Double | The total fraud amount. You can skip this value if no amount is available. For example, in account creation and sign-in scenarios, there might not be an associated amount. In the purchase scenario, Fraud Protection will use the transaction amount. |
| Currency | String | The three-character International Organization for Standardization (ISO) currency code that is related to the amount. |

## Sample API payloads for common scenarios

### Scenario 1

Your review team identified suspicious transactions by looking at the payment information. 

```JSON
{
    "labelObjectType": "PURCHASE",
    "labelObjectId": "<purchase transaction Id, i.e., purchaseId>",
    "labelSource": "ManualReview",
    "isFraud": true,
    "labelState": "Fraud",
    "eventTimeStamp": "2022-10-04T16:24:36.045Z",
    "_metadata": {
        "trackingId": "<guid or identifier>",
        "merchantTimeStamp": "2022-10-04T20:44:14.706Z"
    }
}
```

### Scenario 2

A user lost access to their account, and a malicious actor used that user's credentials to sign in. Later, the user recovered their credentials and reported a compromised time interval.

```JSON
{
    "labelObjectType": "ACCOUNT",
    "labelObjectId": "<userId>",
    "labelSource": "CustomerEscalation",
    "isFraud": true,
    "reasonText": "AccountCompromise",
    "labelState": "Fraud",
    "eventTimeStamp": "2022-10-04T12:21:46.326Z",
    "effectiveStartDate": "2022-10-03T10:00:00.000Z",
    "effectiveEndDate": "2022-10-04T12:16:00.000Z",
    "_metadata": {
        "trackingId": "<guid or identifier>",
        "merchantTimeStamp": "2022-10-04T12:21:46.326Z"
    }
}
```

### Scenario 3

You blocked a suspicious user sign-in, and later the user called the support team to get unblocked. If the support team reviews the evidence, confirms that the user is the legitimate user, and unblocks the user, you must send a label that has a **FalsePositive** state. 
 
```JSON
{
    "labelObjectType": "ACCOUNT",
    "labelObjectId": "<userId>",
    "labelSource": "CustomerEscalation",
    "isFraud": false,
    "reasonText": "AccountCompromise",
    "labelState": "FalsePositive",
    "eventTimeStamp": "2022-10-04T16:21:46.326Z",
    "_metadata": {
        "trackingId": "<guid or identifier>",
        "merchantTimeStamp": "2022-10-04T16:21:46.326Z"
    }
}
```

[!INCLUDE[footer-include](includes/footer-banner.md)]
