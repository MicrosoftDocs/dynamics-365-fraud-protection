---
author: josaw1
description: This article explains how the labels API enables you to send information to the virtual fraud analyst and scorecard.
ms.author: josaw
ms.date: 10/13/2022
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Labels API
ms.custom: 
---

# Labels API

The labels API enables you to send fraud or non-fraud signal to Microsoft Dynamics 365 Fraud Protection. This data will be used in model training, model performance evaluation and reports. . This is a general API to label any assessment event using either individual transaction/event id or entities like user or payment instrument.

## Common label scenarios for Transaction (Purchase/Signup/LogIn/GenericEvent) 
- Any fraudulent transactions escalated by your customers 
- Fraudulent activity or account abuse identified by your review team
- Any offline analysis (like behavior analysis or discovered connections to existing fraud cases)
- TC40/SAFE signals received
- Reverse previous fraud signal after identifying it as non-fraud based on latest information available
- Chargebacks/refunds received
- Chargeback reversal after dispute
 

We recommend using the Chargeback and Refund API for providing information pertaining to chargebacks and refunds. For more information about all supported events, see <a href="https://go.microsoft.com/fwlink/?linkid=2084942" target="_blank">Dynamics 365 Fraud Protection API</a>.

## Account or payment instrument details 
- Fraudulent account or payment instrument info identified by your review team 
- Account takeover scenarios escalated by your customers 

API Schema:
| Attribute  | Type  | Description  | 
|------------|-------|--------------|
| labelObjectType/* |	Enum<p>Expected values:<p>PURCHASE, 
ACCOUNTCREATION, ACCOUNTLOGIN, ACCOUNT, PI, 
EMAIL	| Indicates how “widespread” you would like to flag a label, specifically, if you want to mark a single transaction as fraudulent, or if you want to mark the entire user as fraudulent. Depending on object type we will flag related transactions/events as fraud/non-fraud. For example, if labelObjectType is PURCHASE/ACCOUNTCREATION/ACCOUNTLOGIN then we will label specific transactions. Similarly, if value is ACCOUNT/PI then we flag all the transactions related to that user account or Payment Instrument. |
| labelObjectId/* | String  | The identifier corresponds to the value of the labelObjectType property. We use this value to find related transactions/events. You can find the id for each label object type here.<p>- PURCHASE, purchaseId<p>- ACCOUNTCREATION, signupId<p>- ACCOUNTLOGIN, loginId<p>- ACCOUNT, userId<p>- PI, merchantPaymentInstrumentId<p>This is very important attribute as we use it to identify the original assessment event, so value must match with the original transaction/event Ids. |
| labelSource | String  | Indicate source of label information, some suggested values are “ManualReview” if a fraud label is identified by the review team, “CustomerEscalation” if customer complaints about a falsely rejected transaction (False positive). TC40/SAFE data is another source for label data. |
| isFraud/*  |  Boolean   |  Specify if the label is fraud or non-fraud. Fraud Protection defaults to true If no value is provided.  |
| reasonText |  String  | Reason for labeling fraud or non-fraud. You can safely ignore them if you have limited information regarding your label sources, or you can map some scenarios to some of these values depending on your label workflows. |
|labelReasonCodes  |  String  | Normalized reason codes or reason codes received from payment processor. Safe to ignore if you don’t have reason details.<p>Some suggested values:<p>Processor Response Code, Bank Response Code, Fraud Refund, Account Takeover, Payment Instrument Fraud, Account Fraud, Abuse, Friendly Fraud, Account Credentials Leaked, or Passed Account Protection Checks |
|labelState | String   |  Indicate what kind of label you are sending, used especially if you are reversing previous fraud signal or False Positive. In both cases, you will set isFraud as false, but the state can help to identify False Positive labels.   |
|Processor  | String  |  Payment processor name.  |
|  eventTimeStamp/*  |  DateTime<p>ISO 8601 format  |   Label identified timestamp. If the API is integrated directly with the label detection process this can be the current timestamp. If you Call DFP label API as soon as the review agent flags a transaction as fraud. This is especially important for us to figure out the “order of events” when multiple labels occur – for example, if a purchase/Account creation transaction was labeled as “fraud” label, but then later receives a “non-Fraud” label, we will often refer to this property to see which of the two labels is the more recent – and therefore accurate one.|
|  effectiveStartDate  |  DateTime<p>ISO 8601 format  |  The effective start and end dates are intended to enrich labels that are wider than one transaction (usually “Account” labelObjectTypes) to “limit” the impact of that label down to a particular timeframe – for example, in account compromise scenario these dates will inform window of time that you would like to label transactions/events.|
|  effectiveEndDate  |  DateTime<p>ISO 8601 format  |  The effective start and end dates are intended to enrich labels that are wider than one transaction (usually “Account” labelObjectTypes) to “limit” the impact of that label down to a particular timeframe – for example, in account compromise scenario these dates will inform window of time that you would like to label transactions/events.|
| Amount	| Double	| Total fraud amount, you can skip this if not available. For example, in account creation/Login scenario there may not be any associated amount. In the purchase scenario, we will use transaction amount. |
| currency	| String	| ISO three-character currency code related to the amount. |

## Sample API payload for some common scenarios

  
### Scenario 1

Your review team identified suspicious transactions by looking at the payment information. 

```dfp
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

A user lost access to their account and a malicious actor logged in with the user’s credentials. Later the User recovered his credentials and reported a compromised time interval.
  
```dfp
"labelObjectType": "ACCOUNT",
"labelObjectId": "<userId>,
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
  
You blocked a suspicious user login and later the user calls the support team to unblock him. If the support team reviews the evidence and confirms legitimate user and unblocks, you need to send label with False Positive state. 
 
```dfp
"labelObjectType": "ACCOUNT",
"labelObjectId": "<userId>,
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


[!INCLUDE[footer-include](includes/footer-banner.md)]
