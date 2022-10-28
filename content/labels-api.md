---
author: josaw1
description: This article explains how the labels API enables you to send information to the virtual fraud analyst and scorecard in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 10/28/2022
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Labels API
ms.custom: 
---

# Labels API

This article explains how the labels API enables you to send information to the virtual fraud analyst and scorecard in Microsoft Dynamics 365 Fraud Protection.

The labels API enables you to send fraud or non-fraud signals to Fraud Protection. This data is used in model training, model performance evaluation, and reporting. The labels API is a general API that labels assessment events using either individual transaction or event IDs, or entities such as user or payment instrument.

## Common label scenarios for transactions or events

- Any fraudulent transactions escalated by your customers.
- Fraudulent activity or account abuse identified by your review team.
- Any offline analysis (like behavior analysis or discovered connections to existing fraud cases).
- TC40/SAFE signals received.
- Reverse previous fraud signal after identifying it as non-fraud based on latest information available.
- Chargebacks/refunds received.
- Chargeback reversal after dispute.
 
Microsoft recommends using the chargeback and refund API for providing information related to chargebacks and refunds. For more information about supported events, see [Dynamics 365 Fraud Protection Service](https://go.microsoft.com/fwlink/?linkid=2084942).

## Account or payment instrument details 

- Fraudulent account or payment instrument info identified by your review team. 
- Account takeover scenarios escalated by your customers. 

## API Schema

| Attribute  | Type  | Description | 
|------------|-------|-------------|
| **labelObjectType*** |	Enum</br></br>Expected values: </br>PURCHASE, ACCOUNTCREATION, ACCOUNTLOGIN, ACCOUNT, PI, EMAIL	| Indicates how extensively you want to flag a label. For example, if you want to mark a single transaction as fraudulent, or if you want to mark all of the user account's transactions as fraudulent. Depending on the object type, Fraud Protection flags related transactions or events as fraud or non-fraud. For example, if the labelObjectType is PURCHASE, ACCOUNTCREATION, or ACCOUNTLOGIN, then Fraud Protection labels specific transactions. Similarly, if value is ACCOUNT or PI, then Fraud Protection flags all the transactions related to that user account or payment instrument. |
| **labelObjectId** | String  | The identifier corresponds to the value of the labelObjectType property. Fraud Protection uses this value to find related transactions and events. The IDs for each label object type are as follows:</br></br><ul><li>PURCHASE: purchaseId</li><li>ACCOUNTCREATION: signupId</li><li>ACCOUNTLOGIN: loginId</li><li>ACCOUNT: userId</li><li>PI: merchantPaymentInstrumentId</li></ul>This is a very important attribute because Fraud Protection uses it to identify the original assessment event, so the value must match with the original transaction or event ID. |
| **labelSource** | String  | Indicates the source of label information. Some suggested values are "ManualReview" if a fraud label is identified by the review team, and  "CustomerEscalation" if customer complains about a falsely rejected transaction (in other words, a false positive). TC40/SAFE data is another source for label data. |
| **isFraud**  |  Boolean   |  Specifies if the label is fraud or non-fraud. Fraud Protection defaults to **true** if no value is provided.  |
| **reasonText** |  String  | The reason for labeling something fraud or non-fraud. You can safely ignore reasons if you have limited information regarding your label sources, or you can map some scenarios to some of these values depending on your label workflows. |
| **labelReasonCodes**  |  String  | Normalized reason codes or reason codes received from payment processor. Safe to ignore if you don't have reason details. </br></br>Some suggested values are: </br></br>Processor Response Code, Bank Response Code, Fraud Refund, Account Takeover, Payment Instrument Fraud, Account Fraud, Abuse, Friendly Fraud, Account Credentials Leaked, or Passed Account Protection Checks |
| **labelState** | String   |  Indicates what kind of label you're sending. Used especially if you're reversing a previous fraud signal or false positive. In both cases, you'll set **isFraud** as **false**, but the state can help to identify false positive labels.   |
| **Processor**  | String  |  The name of the payment processor.  |
|  **eventTimeStamp**  |  DateTime (ISO 8601 format)  |   Label identified timestamp. If the API is integrated directly with the label detection process, this can be the current timestamp if you call label API as soon as the review agent flags a transaction as fraud. This value is especially important to figure out the order of events when there are multiple labels. For example, if a purchase or account creation transaction is labeled as "fraud", but then later is labeled "non-fraud", Fraud Protection will refer to this value to see which of the two labels is the most recent (and therefore accurate) label.|
|  **effectiveStartDate**  |  DateTime (ISO 8601 format)  |  The effective start and end dates are intended to enrich labels that are wider than one transaction (usually “Account” labelObjectTypes) to “limit” the impact of that label down to a particular timeframe. For example, in account compromise scenarios these dates specify the window of time in which you want to label the transactions or events.|
|  **effectiveEndDate**  |  DateTime (ISO 8601) format  |  The effective start and end dates are intended to enrich labels that are wider than one transaction (usually with a **labelObjectType** of "ACCOUNT") to limit the impact of that label to a particular timeframe. For example, in account compromise scenarios, these dates specify the window of time in which you want to label the transactions or events.|
| **Amount**	| Double	| The total fraud amount. You can skip this value if not available. For example, in account creation and sign-in scenarios, there may not be an associated amount. In the purchase scenario, Fraud Protection will use the transaction amount. |
| **Currency**	| String	| ISO three-character currency code related to the amount. |

## Sample API payloads for common scenarios

### Scenario 1

Your review team identified suspicious transactions by looking at the payment information. 

```JSON
{
  "labelObjectType": "PURCHASE",
  "labelObjectId": "<purchase transaction Id, i.e., purcahseId>",
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

A user lost access to their account and a malicious actor signed in with the user’s credentials. Later, the user recovered their credentials and reported a compromised time interval.
  
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
  
You blocked a suspicious user sign-in and later the user called the support team to get unblocked. If the support team reviews the evidence and confirms the user as legitimate user and unblocks the user, you must send a label with a **FalsePositive** state. 
 
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
