---
author: jegrif
description: Schema
ms.author: v-jegrif
ms.date: 02/25/2019
ms.service:
 - d365-fraud-protection
ms.topic: conceptual
title: Schema
---


# Schemas
The following document outlines the required schemas for data that will be manually uploaded into Dynamics 365 Fraud Protection.

## Transactions

### Purchase
Used in the Diagnose, Evaluate, and Protect experiences.
```
PurchaseId               string
,OriginalOrderId         string
,CustomerLocalDate       DateTime
,MerchantLocalDate       DateTime
,TotalAmount             string
,SalesTax                string
,Currency                string
,DeviceContextId         string
,IPAddress               string
,UserId                  string
,UserFirstName           string
,UserLastName            string
,UserEmail               string
,UserCreationDate        DateTime
,UserUpdateDate          DateTime
,UserZipCode             string
,UserCountry             string
,UserTimeZone            string
,UserLanguage            string
,UserPhoneNumber         string
,IsEmailValidated        bool
,ShippingFirstName       string
,ShippingLastName        string
,ShippingPhoneNumber     string
,Street1                 string
,Street2                 string
,Street3                 string
,City                    string
,State                   string
,ZipCode                 string
,Country                 string
```

### Payment instruments
Used in the Diagnose, Evaluate, and Protect experiences.
```
PurchaseId                    string
,MerchantPaymentInstrumentId  string
,Type                         string
,PurchaseAmount               string
,CreationDate                 DateTime
,UpdateDate                   DateTime
,CardType                     string
,HolderName                   string
,BIN                          string
,ExpirationDate               DateTime
,LastFourDigits               string
,Email                        string
,BillingAgreementId           string
,PayerId                      string
,PayerStatus                  string
,AddressStatus                string
,IMEI                         string
,FirstName                    string
,LastName                     string
,PhoneNumber                  string
,Street1                      string
,Street2                      string
,Street3                      string
,City                         string
,State                        string
,ZipCode                      string
,Country                      string
```

### Products
Used in the Diagnose, Evaluate, and Protect experiences.
```
PurchaseId   string
,ProductId      string
,PurchasePrice  string
,Margin         string
,Quantity       string
,ProductName    string
,Type           string
,Category       string
,Market         string
,Sku            string
,SalesPrice     string
,Currency       string
,COGS           string
,IsRecurring    bool
,IsFree         bool
```

## Chargeback
Used in the Diagnose, Evaluate, and Protect experiences.
```
"chargebackId": "string",
"reason": "string",
"status": "string",
"bankEventTimestamp": "2019-01-24T02:31:37.646Z",
"amount": 0,
"currency": "string",
"userId": "string"
"purchaseId": "string"
"merchantLocalDate": "2019-01-24T02:31:37.646Z"

```
## Refund
Used in the Evaluate and Protect experiences.
```
"refundId": "string",
"reason": "string",
"status": "string",
"bankEventTimestamp": "2019-01-24T02:37:09.371Z",
"amount": 0,
"currency": "string",
"userId": "string"
"purchaseId": "string"
"merchantLocalDate": "2019-01-24T02:37:09.371Z"
```

## Purchase status
Used in the Evaluate and Protect experiences.
```
"purchaseId": "string",
"statusType": "string",
"statusDate": "2019-01-24T02:38:12.319Z",
"reason": "string"
"merchantLocalDate": "2019-01-24T02:38:12.319Z"
```

## Bank event
Used in the Evaluate and Protect experiences.
```
"bankEventId": "string",
"type": "string",
"bankEventTimestamp": "2019-01-24T02:28:53.997Z",
"status": "string",
"bankResponseCode": "string",
"paymentProcessor": "string",
"mrn": "string",
"mid": "string",
"purchaseId": "string",
"merchantLocalDate": "2019-01-24T02:28:53.997Z"
```

## Account

### Update account
Used in the Evaluate and Protect experiences.
```
"customerLocalDate": "2019-01-24T02:32:58.101Z",
"userId": "string",
"usercreationDate": "2019-01-24T02:32:58.102Z",
"userupdateDate": "2019-01-24T02:32:58.102Z",
"firstName": "string",
"lastName": "string",
"country": "string",
"zipCode": "string",
"timeZone": "string",
"language": "string",
"phoneNumber": "string",
"email": "string",
"isEmailValidated": true,
"emailValidatedDate": "2019-01-24T02:32:58.102Z",
"isPhoneNumberValidated": true,
"phoneNumberValidatedDate": "2019-01-24T02:32:58.102Z",
"deviceContextId": "string",
"provider": "string",
"deviceContextDC": "string",
"externalDeviceId": "string",
"externalDeviceType": "string",
"ipAddress": "string"
"merchantLocalDate": "2019-01-24T02:32:58.102Z"
```


### Update address
Used in the Evaluate and Protect experiences.
```
"userId": "string",
"addresstype": "string",
"firstName": "string",
"lastName": "string",
"phoneNumber": "string",
"street1": "string",
"street2": "string",
"street3": "string",
"city": "string",
"state": "string",
"district": "string",
"zipCode": "string",
"country": "string"
```

### Update payment instruments
Used in the Evaluate and Protect experiences.
```
"userId": "string",
"merchantPaymentInstrumentId": "string",
"PaymentInstrumenttype": "string",
"PaymentInstrumentcreationDate": "2019-01-24T02:32:58.102Z",
"PaymentInstrumentupdateDate": "2019-01-24T02:32:58.102Z",
"state": "string",
"cardType": "string",
"holderName": "string",
"bin": "string",
"expirationDate": "string",
"lastFourDigits": "string",
"email": "string",
"billingAgreementId": "string",
"payerId": "string",
"payerStatus": "string",
"addressStatus": "string",
"imei": "string",
"billingAddress": {
"BillingAddressfirstName": "string",
"BillingAddresslastName": "string",
"BillingAddressphoneNumber": "string",
"street1": "string",
"street2": "string",
"street3": "string",
"city": "string",
"state": "string",
"district": "string",
"zipCode": "string",
"country": "string"
```
