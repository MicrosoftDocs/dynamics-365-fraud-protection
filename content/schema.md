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

## Purchase
Used in the Diagnose, Evaluate, and Protect experiences.
```
"PurchaseId": "SamplePurchaseId",
"OriginalOrderId": "SampleOriginalOrderId",
"CustomerLocalDate": "2018-09-24T11:54:32.9915288-07:00",
"MerchantLocalDate": "2018-09-24T11:54:32.9915491-07:00",
"TotalAmount": 0,
"SalesTax": 0,
"Currency": "string",
"UserId": "SampleUserId",
"UserCreationDate": "2018-09-24T11:54:32.9935576-07:00",
"UserUpdateDate": "2018-09-24T11:54:32.9935693-07:00",
"FirstName": "string",
"LastName": "string",
"Country": "string",
"ZipCode": "string",
"TimeZone": "string",
"Language": "string",
"PhoneNumber": "string",
"Email": "string",
"IsEmailValidated": true,
"EmailValidatedDate": "2018-09-24T11:54:32.9936183-07:00",
"IsPhoneNumberValidated": true,
"PhoneNumberValidatedDate": "2018-09-24T11:54:32.9936366-07:00"
"DeviceContextId": "SampleDeviceContextId",
"DeviceContextDC": "string",
"ExternalDeviceId": "SampleExternalDeviceId",
"IPAddress": "string"
"ShippingAddressFirstName": "string",
"ShippingAddressLastName": "string",
"ShippingAddressPhoneNumber": "string",
"Street1": "string",
"Street2": "string",
"Street3": "string",
"City": "string",
"State": "string",
"District": "string",
"ZipCode": "string",
"Country": "string"
```

## Purchase: Payment instruments
Used in the Diagnose, Evaluate, and Protect experiences.
```
"PurchaseId": "SamplePurchaseId",
"MerchantPaymentInstrumentId": "string",
"PaymentInstrumentType": "string",
"PaymentInstrumentPurchaseAmount": 0,
"PaymentInstrumentCreationDate": "2018-09-24T11:54:32.9938265-07:00",
"PaymentInstrumentUpdateDate": "2018-09-24T11:54:32.9938370-07:00",
"State": "string",
"CardType": "string",
"HolderName": "string",
"BIN": "string",
"ExpirationDate": "string",
"LastFourDigits": "string",
"Email": "string",
"BillingAgreementId": "SampleBillingAgreementId",
"PayerId": "SamplePayerId",
"PayerStatus": "string",
"AddressStatus": "string",
"IMEI": "string",
"BillingAddress": 
"BillingAddressFirstName": "string",
"BillingAddressLastName": "string",
"BillingAddressPhoneNumber": "string",
"Street1": "string",
"Street2": "string",
"Street3": "string",
"City": "string",
"State": "string",
"District": "string",
"ZipCode": "string",
"Country": "string"
```

## Purchase: Products
Used in the Diagnose, Evaluate, and Protect experiences.
```
"PurchaseId": "SamplePurchaseId",
"ProductId": "SampleProductId",
"PurchasePrice": 0,
"Margin": 0,
"Quantity": 0,
"ProductName": "string",
"Type": "string",
"Sku": "string",
"Category": "string",
"Market": "string",
"SalesPrice": 0,
"Currency": "string",
"COGS": 0,
"IsRecurring": true,
"IsFree": true,
"Language": "string",
"MerchantLocalDate": "2019-01-31T22:24:31.521Z"
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
## Update account
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
## Update account: Address
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
## Update account: Payment instruments
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
