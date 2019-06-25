---
author: jegrif
description: This topic outlines the schemas that are required for historical data View schemas
ms.author: v-jegrif
ms.service: crm-online
ms.date: 04/22/2019

ms.topic: conceptual
title: View data upload schemas
---

# View data upload schemas

This topic outlines the schemas for historical data that is bulk-uploaded into Microsoft Dynamics 365 Fraud Protection as comma-separated values (CSV) files. For information about the upload procedure, see [Upload historical data](data-upload.md). If data will be ingested via the application programming interface (API), see [Send real-time data](send-real-time-api.md).

Note the following formatting guidelines throughout:

- The files are in CSV format.
- The maximum file size is 10 gigabytes (GB).
- The **DateTime** columns are in ISO 8601 format. For example, **DateTime.UtcNow.ToString("o")** might have the result **"2019-03-14T20:18:11.254Z"**.
- The decimal precision is two decimal places.
- The following characters are escaped in all columns: commas, new line characters, and multiline characters.

## Transactions

The following schemas are used in the Diagnose, Evaluate, and Protect experiences.

### Purchases

| Attribute           | Type     | Description |
|---------------------|----------|-------------|
| PurchaseId          | string   | The identifier of the transaction (or purchase or order). |
| OriginalOrderId     | string   | The original order identifier for payments of recurring billing, such as monthly subscription billing. |
| CustomerLocalDate   | DateTime | The purchase creation date in the customer's local time zone. The format is ISO 8601. |
| MerchantLocalDate   | DateTime | The purchase ingestion date in the merchant's time zone. The format is ISO 8601. |
| TotalAmount         | double   | The total amount that was charged to the customer, including tax. This information is provided by the merchant. |
| SalesTax            | double   | The sales tax that was charged for the transaction. This information is provided by the merchant. |
| Currency            | string   | The currency of the original purchase as a three-character currency code (for example, **USD**, which is aligned with the OANDA currency code). This information is provided by merchant. |
| DeviceContextId     | string   | The session ID of the event's session (provided by Microsoft Device Fingerprinting), or the transaction ID if the session isn't available. |
| IPAddress           | string   | The customer's IP address. This information is provided by Microsoft Device Fingerprinting. |
| UserId              | string   | The customer identifier. This information is provided by the merchant. |
| UserFirstName       | string   | The customer-provided first name on the customer account. |
| UserLastName        | string   | The customer-provided last name on the customer account. |
| UserEmail           | string   | The customer's email address. This value is case-insensitive. |
| UserCreationDate    | DateTime | The creation date of the customer account. The format is ISO 8601. |
| UserUpdateDate      | DateTime | The date when customer data was last changed. The format is ISO 8601. |
| UserZipCode         | string   | The customer's postal code. |
| UserCountry         | string   | The customer's country or region. The value should be a two-letter country/region code (for example, **US**). |
| UserTimeZone        | string   | An empty string. |
| UserLanguage        | string   | The customer's language and language territory (for example, **EN-US**). |
| UserPhoneNumber     | string   | The customer's phone number. The format should be the country/region code followed by a hyphen (-) and then the phone number (for example, for the US, **+1-1234567890**). |
| IsEmailValidated    | bool     | A **True**/**False** value that indicates whether the customer-provided email address has been verified as owned by the customer. |
| ShippingFirstName   | string   | The first name that was provided for the address. |
| ShippingLastName    | string   | The last name that was provided for the address. |
| ShippingPhoneNumber | string   | The phone number that was provided for the address. The format should be the country/region code followed by a hyphen (-) and then the phone number (for example, for the US, **+1-1234567890**). |
| Street1             | string   | The first row that was provided for the address. |
| Street2             | string   | The second row that was provided for the address. (This value can be blank.) |
| Street3             | string   | The third row that was provided for the address. (This value can be blank.) |
| City                | string   | The city that was provided for the address. |
| State               | string   | The state or province that was provided for the address. |
| ZipCode             | string   | The postal code that was provided for the address. |
| Country             | string   | The country/region code that was provided for the address. The value should be a two-letter ISO country/region code (for example, **US**). |

### Payment instruments

| Attribute                   | Type     | Description |
|-----------------------------|----------|-------------|
| PurchaseId                  | string   | The identifier of the transaction (or purchase or order). |
| MerchantPaymentInstrumentId | string   | The identifier of the payment instrument. This information is provided by the merchant. |
| Type                        | string   | The type of payment: **CreditCard**, **Paypal**, **Mobilepayment**, or **Giftcard**. |
| PurchaseAmount              | double   | The total purchase amount that uses this payment instrument for the transaction. |
| CreationDate                | DateTime | The date of the first entry for the payment instrument in the merchant's system. The format is ISO 8601. |
| UpdateDate                  | DateTime | The date of the last update for the payment instrument in the merchant's system. The format is ISO 8601. |
| CardType                    | string   | This attribute is used only for payments of the **CreditCard** type. |
| HolderName                  | string   | The name of the customer of the payment instrument. This attribute is used only for payments of the **CreditCard** type. |
| BIN                         | string   | This attribute is used only for payments of the **CreditCard** type. |
| ExpirationDate              | string   | The expiration date for the payment instrument in the merchant's system. The format is ISO 8601. This attribute is used only for payments of the **CreditCard** type. |
| LastFourDigits              | string   | This attribute is used only for payments of the **CreditCard** type. |
| Email                       | string   | The email address that is associated with the payment instrument. This attribute is used only for payments of the **Paypal** type. |
| BillingAgreementId          | string   | This attribute is used only for payments of the **Paypal** type. |
| PayerId                     | string   | This attribute is used only for payments of the **Paypal** type. |
| PayerStatus                 | string   | A value that indicates whether PayPal has verified the payer. This attribute is used only for payments of the **Paypal** type. |
| AddressStatus               | string   | A value that indicates whether PayPal has verified the payer's address. This attribute is used only for payments of the **Paypal** type. |
| IMEI                        | string   | This attribute is used only for payments of the **Mobilepayment** type. |
| FirstName                   | string   | The first name that was provided for the address. |
| LastName                    | string   | The last name that was provided for the address. |
| PhoneNumber                 | string   | The phone number that was provided for the address. The format should be the country/region code followed by a hyphen (-) and then the phone number (for example, for the US, **+1-1234567890**). |
| Street1                     | string   | The first row that was provided for the address. |
| Street2                     | string   | The second row that was provided for the address. (This value can be blank.) |
| Street3                     | string   | The third row that was provided for the address. (This value can be blank.) |
| City                        | string   | The city that was provided for the address. |
| State                       | string   | The state or province that was provided for the address. |
| ZipCode                     | string   | The postal code that was provided for the address. |
| Country                     | string   | The country/region code that was provided for the address. The value should be a two-letter ISO country/region code (for example, **US**). |

### Products

| Attribute     | Type   | Description |
|---------------|--------|-------------|
| PurchaseId    | string | The identifier of the transaction (or purchase or order). |
| ProductId     | string | The product identifier. |
| PurchasePrice | double | The price for the line item of the purchase. |
| Margin        | string | The margin that was gained by the sale of the item. |
| Quantity      | Int32  | The number of items that were purchased. |
| ProductName   | string | The customer-readable product name. |
| Type          | string | A value that indicates whether the goods were physical or digital. |
| Category      | string | The category of product (for example, **Apparel**, **Shoes**, or **Accessories**). |
| Market        | string | The market where the product is offered. The value should be a two-letter ISO country/region code (for example, **US**). |
| Sku           | string | The product's stock keeping unit (SKU). |
| SalesPrice    | double | The price of the item that was sold, excluding tax. This information is provided by the merchant. |
| COGS          | string | The cost of goods sold (that is, the raw material cost of the item). This information is provided by the merchant. |
| IsRecurring   | bool   | A value that indicates whether the product is a recurring subscription. |
| IsFree        | bool   | A value that indicates whether the product is offered for free. |
| Language      | string | The language and language territory (for example, **EN-US**). |

## Chargebacks

The following schema is used in the Diagnose, Evaluate, and Protect experiences.

| Attribute          | Type     | Description |
|--------------------|----------|-------------|
| chargebackId       | string   | The chargeback identifier. |
| reason             | string   | The reason that was provided by the bank. |
| status             | string   | The status: **INITIATED**, **LOST**, or **WON**. |
| bankEventTimestamp | DateTime | The timestamp from the bank. The format is ISO 8601. |
| amount             | double   | The chargeback amount. |
| currency           | string   | The currency that is used for the chargeback amount. |
| userId             | string   | The customer identifier. |
| purchaseId         | string   | The identifier of the transaction (or purchase or order). |
| merchantLocalDate  | DateTime | The date when the purchase was ingested, in the merchant's time zone. The format is ISO 8601. |

## Refunds

The following schema is used in the Evaluate and Protect experiences.

| Attribute          | Type     | Description |
|--------------------|----------|-------------|
| refundId           | string   | The refund identifier. |
| reason             | string   | The customer-provided reason. |
| status             | string   | The refund status: **INITIATED** or **COMPLETED**. |
| bankEventTimestamp | DateTime | The timestamp from the bank. The format is ISO 8601. |
| amount             | double   | The refund amount. |
| currency           | string   | The currency that is used for the sales price amount. |
| userId             | string   | The customer identifier. |
| purchaseId         | string   | The identifier of the transaction (or purchase or order). |
| merchantLocalDate  | DateTime | A date in ISO 8601 format. |

## Purchase status

The following schema is used in the Evaluate and Protect experiences.

| Attribute         | Type     | Description |
|-------------------|----------|-------------|
| purchaseId        | string   | The identifier of the transaction (or purchase or order). |
| statusType        | string   | The type of status: **APPROVED**, **CANCELED**, **HELD**, or **FULFILLED**. |
| statusDate        | DateTime | The date and time when the status was applied. The format is ISO 8601. |
| reason            | string   | The reason for the status transition. |
| merchantLocalDate | DateTime | A date in ISO 8601 format. |

## Bank events

The following schema is used in the Evaluate and Protect experiences.

| Attribute          | Type     | Description |
|--------------------|----------|-------------|
| bankEventId        | string   | The bank event identifier. |
| type               | string   | The bank event type: **AUTH** or **CHARGE**. |
| bankEventTimestamp | DateTime | The timestamp from the bank. The format is ISO 8601. |
| status             | string   | The status: **APPROVED** or **REJECTED**. |
| bankResponseCode   | string   | The bank code on the response. |
| paymentProcessor   | string   | The processor name (for example, **FDC** or **PAYPAL**). |
| mrn                | string   | The Merchant Reference Number (MRN) that is used to identify the transaction on the merchant side. |
| mid                | string   | The merchant ID (MID) that is used for bank communication. |
| purchaseId         | string   | The identifier of the transaction (or purchase or order). |
| merchantLocalDate  | DateTime | A date in ISO 8601 format. |

## Account

The following schemas are used in the Evaluate and Protect experiences.

### Update account

| Attribute                | Type     | Description |
|--------------------------|----------|-------------|
| customerLocalDate        | DateTime | A date in ISO 8601 format. |
| userId                   | string   | The customer identifier. |
| usercreationDate         | DateTime | A date in ISO 8601 format. |
| userupdateDate           | DateTime | A date in ISO 8601 format. |
| firstName                | string   | The customer-provided first name on the customer account. |
| lastName                 | string   | The customer-provided last name on the customer account. |
| country                  | string   | The customer's country or region. The value should be a two-letter country/region code (for example, **US**). |
| zipCode                  | string   | The customer's postal code. |
| timeZone                 | string   | This attribute is obsolete (deprecated). Provide an empty string as the value. |
| language                 | string   | The customer's language and language territory (for example, **EN-US**). |
| phoneNumber              | string   | The customer's phone number. The format should be the country/region code followed by a hyphen (-) and then the phone number (for example, for the US, **+1-1234567890**). |
| email                    | string   | The customer's email address. This value is case-insensitive. |
| isEmailValidated         | bool     | A value that indicates whether the customer-provided email has been verified as owned by the customer. |
| emailValidatedDate       | DateTime | The date when the customer-provided email was verified as owned by the customer. The format is ISO 8601. |
| isPhoneNumberValidated   | bool     | A value that indicates whether the customer-provided phone number has been verified as owned by the customer. |
| phoneNumberValidatedDate | DateTime | The date when the customer-provided phone number was verified as owned by the customer. The format is ISO 8601. |
| deviceContextId          | string   | The session ID of the event's session (provided by Microsoft Device Fingerprinting), or the transaction ID if the session isn't available. |
| provider                 | string   | A value that indicates the source of the **deviceContextId** value: **DFP Fingerprinting** or **Merchant**. |
| deviceContextDC          | string   | The Microsoft Device Fingerprinting data center for the customer's session ID. |
| externalDeviceId         | string   | The customer's device ID. This information is provided and mastered by the merchant. |
| externalDeviceType       | string   | The device type, as identified by the merchant (for example, **PC** or **Mobile Device**). |
| ipAddress                | string   | The customer's IP address. This information is provided by Microsoft Device Fingerprinting. |
| merchantLocalDate        | DateTime | A date in ISO 8601 format. |

### Update address

| Attribute   | Type   | Description |
|-------------|--------|-------------|
| userId      | string | The customer identifier. |
| addresstype | string | The address type: **BILLING**, **SHIPPING**, or **ACCOUNT**. |
| firstName   | string | The first name that was provided for the address. |
| lastName    | string | The last name that was provided for the address. |
| phoneNumber | string | The phone number that was provided for the address. |
| street1     | string | The first row that was provided for the address. |
| street2     | string | The second row that was provided for the address. (This value can be blank.) |
| street3     | string | Third row that was provided for the address. (This value can be blank.) |
| city        | string | The city that was provided for the address. |
| state       | string | The state or province that was provided for the address. |
| district    | string | The district that was provided for the address. (This value can be blank.) |
| zipCode     | string | The postal code that was provided for the address. |
| country     | string | The country/region code that was provided for the address. The value should be a two-letter ISO country/region code (for example, **US**). |

### Update payment instrument

| Attribute                     | Type     | Description |
| ----------------------------- |----------|-------------|
| userId                        | string   | The customer identifier. |
| merchantPaymentInstrumentId   | string   | The identifier of the payment instrument. This information is provided by the merchant. |
| PaymentInstrumenttype         | string   | The type of payment: **CreditCard**, **Paypal**, **Mobilepayment**, or **Giftcard**. |
| PaymentInstrumentcreationDate | DateTime | The date of the first entry for the payment instrument in the merchant's system. The format is ISO 8601. |
| PaymentInstrumentupdateDate   | DateTime | The date of the last update for the payment instrument in the merchant's system. The format is ISO 8601. |
| PaymentInstrumentState        | string   | The state of the payment instrument: **Active**, **Block**, or **Expire**. |
| cardType                      | string   | This attribute is used only for payments of the **CreditCard** type. |
| holderName                    | string   | The name of the customer of the payment instrument. This attribute is used only for payments of the **CreditCard** type. |
| bin                           | string   | This attribute is used only for payments of the **CreditCard** type. |
| expirationDate                | string   | The expiration date for the payment instrument in the merchant's system. This attribute is used only for payments of the **CreditCard** type. |
| lastFourDigits                | string   | This attribute is used only for payments of the **CreditCard** type. |
| email                         | string   | The email address that is associated with the payment instrument. This attribute is used only for payments of the **Paypal** type. |
| billingAgreementId            | string   | This attribute is used only for payments of the **Paypal** type. |
| payerId                       | string   | This attribute is used only for payments of the **Paypal** type. |
| payerStatus                   | string   | A value that indicates whether PayPal has verified the payer. This attribute is used only for payments of the **Paypal** type. |
| addressStatus                 | string   | A value that indicates whether PayPal has verified the payer's address. This attribute is used only for payments of the **Paypal** type. |
| imei                          | string   | This attribute is used only for payments of the **Mobilepayment** type. |
| BillingAddressfirstName       | string   | The first name that was provided for address. |
| BillingAddresslastName        | string   | The last name that was provided for address. |
| BillingAddressphoneNumber     | string   | The phone number that was provided for address. The format should be the country/region code followed by a hyphen (-) and then the phone number (for example, for the US, **+1-1234567890**). |
| street1                       | string   | The first row that was provided for the address. |
| street2                       | string   | The second row that was provided for the address. (This value can be blank.) |
| street3                       | string   | Third row that was provided for the address. (This value can be blank.) |
| city                          | string   | The city that was provided for the address. |
| state                         | string   | The state or province that was provided for the address. |
| district                      | string   | The district that was provided for the address. (This value can be blank.) |
| zipCode                       | string   | The postal code that was provided for the address. |
| country                       | string   | The country/region code that was provided for the address. The value should be a two-letter ISO country/region code (for example, **US**). |
