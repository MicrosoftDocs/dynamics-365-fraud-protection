---
author: jegrif
description: This topic outlines the schemas that are required for historical data upload
ms.author: v-jegrif
ms.service: fraud-protection
ms.date: 09/04/2019

ms.topic: conceptual
title: View purchase protection schemas
---

# View purchase protection schemas

This topic outlines the schemas for historical data that is bulk-uploaded into Microsoft Dynamics 365 Fraud Protection as comma-separated values (CSV) files. For information about the upload procedure, see [Upload historical data](data-upload.md). If data will be ingested via the application programming interface (API), see [Integrate Dynamics 365 Fraud Protection real-time APIs](integrate-real-time-api.md).

Note the following formatting guidelines throughout:

- The files are in CSV UTF-8 (comma delimited) format (\*.csv).
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
| MerchantLocalDate   | DateTime | The purchase ingestion date in the merchant's local time zone. The format is ISO 8601. |
| TotalAmount         | double   | The total amount that was charged to the customer including tax. This information is provided by the merchant. |
| SalesTax            | double   | The sales tax that was charged for the transaction. This information is provided by the merchant. |
| Currency            | string   | The currency of the original purchase as a three-character currency code (for example: **USD**, which is aligned with the OANDA currency code). This information is provided by the merchant. |
| DeviceContextId     | string   | The session ID of the event's session (provided by Microsoft Device Fingerprinting) or the transaction ID if the session isn't available. |
| IPAddress           | string   | The customer's IP address. This information is provided by Microsoft Device Fingerprinting. |
| UserId              | string   | The customer identifier. This information is provided by the merchant. |
| UserFirstName       | string   | The customer-provided first name on the customer account. |
| UserLastName        | string   | The customer-provided last name on the customer account. |
| UserEmail           | string   | The customer's email address. This value is case-insensitive. |
| UserCreationDate    | DateTime | The creation date of the customer account. The format is ISO 8601. |
| UserUpdateDate      | DateTime | The date when customer data was last changed. The format is ISO 8601. |
| UserZipCode         | string   | The customer's postal code. |
| UserCountryCode     | string   | The customer's country or region. The value should be a two-letter country or region code (for example: **US**). |
| UserTimeZone        | string   | An empty string. |
| UserLanguage        | string   | The customer's language and language territory (for example: **EN-US**). |
| UserPhoneNumber     | string   | The customer's phone number. The format should be the country or region code followed by a hyphen (-) and then the phone number (for example: for the US, **+1-1234567890**). |
| IsEmailValidated    | bool     | A **True**/**False** value that indicates whether the customer-provided email address has been verified as owned by the customer. |
| ShippingFirstName   | string   | The first name that was provided for the address. |
| ShippingLastName    | string   | The last name that was provided for the address. |
| ShippingPhoneNumber | string   | The phone number that was provided for the address. The format should be the country or region code followed by a hyphen (-) and then the phone number (for example: for the US, **+1-1234567890**). |
| Street1             | string   | The first row that was provided for the address. |
| Street2             | string   | The second row that was provided for the address. (This value can be blank.) |
| Street3             | string   | The third row that was provided for the address. (This value can be blank.) |
| City                | string   | The city that was provided for the address. |
| State               | string   | The state or province that was provided for the address. |
| ZipCode             | string   | The postal code that was provided for the address. |
| CountryCode         | string   | The country or region code that was provided for the address. The value should be a two-letter ISO country or region code (for example: **US**). |

### PaymentInstruments

| Attribute                   | Type     | Description |
|-----------------------------|----------|-------------|
| PurchaseId                  | string   | The identifier of the transaction (or purchase or order). |
| MerchantPaymentInstrumentId | string   | The identifier of the payment instrument. This information is provided by the merchant. |
| Type                        | string   | The type of payment: **credit_card**, **direct_debit**, **finance_leasing**, **invoice_credit**, **offline_bank_transfer**, **online_bank_transfer**, **Paypal**, **stored_value**, or **Mobilepayment**. |
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
| PhoneNumber                 | string   | The phone number that was provided for the address. The format should be the country or region code followed by a hyphen (-) and then the phone number (for example: for the US, **+1-1234567890**). |
| Street1                     | string   | The first row that was provided for the address. |
| Street2                     | string   | The second row that was provided for the address. (This value can be blank.) |
| Street3                     | string   | The third row that was provided for the address. (This value can be blank.) |
| City                        | string   | The city that was provided for the address. |
| State                       | string   | The state or province that was provided for the address. |
| ZipCode                     | string   | The postal code that was provided for the address. |
| CountryCode                 | string   | The country/region code that was provided for the address. The value should be a two-letter ISO country or region code (for example: **US**). |

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
| Category      | string | The category of product (for example: **Apparel**, **Shoes**, or **Accessories**). |
| Market        | string | The market where the product is offered. The value should be a two-letter ISO country or region code (for example: **US**). |
| Sku           | string | The product's stock keeping unit (SKU). |
| SalesPrice    | double | The price of the item that was sold excluding tax. This information is provided by the merchant. |
| Currency      | string | The currency of the original purchase as a three-character currency code (for example: **USD**, which is aligned with the OANDA currency code). This information is provided by the merchant.  | 
| COGS          | string | The cost of goods sold (that is, the raw material cost of the item). This information is provided by the merchant. |
| IsRecurring   | bool   | A value that indicates whether the product is a recurring subscription. |
| IsFree        | bool   | A value that indicates whether the product is offered for free. |
| Language      | string | The language and language territory (for example: **EN-US**). |

## Chargebacks

The following schema is used in the Diagnose, Evaluate, and Protect experiences.

| Attribute          | Type     | Description |
|--------------------|----------|-------------|
| ChargebackId       | string   | The chargeback identifier. |
| Reason             | string   | The reason that was provided by the bank. |
| Status             | string   | The status: **Accepted**, **CB_Dispute-Initiated**, **CB_Dispute-Lose**, **CB_Dispute-Win**, **Chargeback-CB1**, **Chargeback-CB2**, **Inquiry_Dispute-Win**, **Inquiry-Initiated**, **ResubmittedRequest**, or **Unknown**. |
| BankEventTimestamp | DateTime | The timestamp from the bank. The format is ISO 8601. |
| Amount             | double   | The chargeback amount. |
| Currency           | string   | The currency that is used for the chargeback amount. |
| UserId             | string   | The customer identifier. |
| PurchaseId         | string   | The identifier of the transaction (or purchase or order). |
| MerchantLocalDate  | DateTime | The purchase ingestion date in the merchant's local time zone. The format is ISO 8601. |

## Refunds

The following schema is used in the Evaluate and Protect experiences.

| Attribute          | Type     | Description |
|--------------------|----------|-------------|
| RefundId           | string   | The refund identifier. |
| Reason             | string   | The customer-provided reason. |
| Status             | string   | The refund status: **Approved**, **Declined**, **Failed**, **Offline_Approved**, **Pending**, **Reversed**, or **Unknown**. |
| BankEventTimestamp | DateTime | The timestamp from the bank. The format is ISO 8601. |
| Amount             | double   | The refund amount. |
| Currency           | string   | The currency that is used for the sales price amount. |
| UserId             | string   | The customer identifier. |
| PurchaseId         | string   | The identifier of the transaction (or purchase or order). |
| MerchantLocalDate  | DateTime | A date in ISO 8601 format. |

## PurchaseStatus

The following schema is used in the Evaluate and Protect experiences.

| Attribute         | Type     | Description |
|-------------------|----------|-------------|
| PurchaseId        | string   | The identifier of the transaction (or purchase or order). |
| StatusType        | string   | The type of status: **Approved**, **Challenge**, **Pending**, **Rejected**, **Review**, or **Unknown**. |
| StatusDate        | DateTime | The date and time when the status was applied. The format is ISO 8601. |
| Reason            | string   | The reason for the status transition. |
| MerchantLocalDate | DateTime | A date in ISO 8601 format. |

## BankEvents

The following schema is used in the Evaluate and Protect experiences.

| Attribute          | Type     | Description |
|--------------------|----------|-------------|
| BankEventId        | string   | The bank event identifier. |
| Type               | string   | The bank event type: **authorize**, **charge**, **refund**, **validate**, or **unknown**. |
| BankEventTimestamp | DateTime | The timestamp from the bank. The format is ISO 8601. |
| Status             | string   | The status: **approved**, **declined**, **failed**, **reversed**, **pending**, or **unknown**. |
| BankResponseCode   | string   | The bank code on the response. |
| PaymentProcessor   | string   | The processor name (for example: **FDC** or **Paypal**). |
| MRN                | string   | The Merchant Reference Number (MRN) that is used to identify the transaction on the merchant side. |
| MID                | string   | The merchant ID (MID) that is used for bank communication. |
| PurchaseId         | string   | The identifier of the transaction (or purchase or order). |
| MerchantLocalDate  | DateTime | A date in ISO 8601 format. |

## Account

The following schemas are used in the Evaluate and Protect experiences.

### UpdateAccount

| Attribute                | Type     | Description |
|--------------------------|----------|-------------|
| CustomerLocalDate        | DateTime | A date in ISO 8601 format. |
| UserId                   | string   | The customer identifier. |
| UsercreationDate         | DateTime | A date in ISO 8601 format. |
| UserupdateDate           | DateTime | A date in ISO 8601 format. |
| FirstName                | string   | The customer-provided first name on the customer account. |
| LastName                 | string   | The customer-provided last name on the customer account. |
| CountryCode              | string   | The customer's country or region. The value should be a two-letter country or region code (for example: **US**). |
| ZipCode                  | string   | The customer's postal code. |
| TimeZone                 | string   | This attribute is obsolete (deprecated). Provide an empty string as the value. |
| Language                 | string   | The customer's language and language territory (for example: **EN-US**). |
| PhoneNumber              | string   | The customer's phone number. The format should be the country/region code followed by a hyphen (-) and then the phone number (for example: for the US, **+1-1234567890**). |
| Email                    | string   | The customer's email address. This value is case-insensitive. |
| IsEmailValidated         | bool     | A value that indicates whether the customer-provided email has been verified as owned by the customer. |
| EmailValidatedDate       | DateTime | The date when the customer-provided email was verified as owned by the customer. The format is ISO 8601. |
| IsPhoneNumberValidated   | bool     | A value that indicates whether the customer-provided phone number has been verified as owned by the customer. |
| PhoneNumberValidatedDate | DateTime | The date when the customer-provided phone number was verified as owned by the customer. The format is ISO 8601. |
| DeviceContextId          | string   | The session ID of the event's session (provided by Microsoft Device Fingerprinting) or the transaction ID if the session isn't available. |
| Provider                 | string   | A value that indicates the source of the **deviceContextId** value: **DFP Fingerprinting** or **Merchant**. |
| DeviceContextDC          | string   | The Microsoft Device Fingerprinting data center for the customer's session ID. |
| ExternalDeviceId         | string   | The customer's device ID. This information is provided and mastered by the merchant. |
| ExternalDeviceType       | string   | The device type as identified by the merchant (for example: **PC** or **Mobile Device**). |
| IpAddress                | string   | The customer's IP address. This information is provided by Microsoft Device Fingerprinting. |
| MerchantLocalDate        | DateTime | A date in ISO 8601 format. |

### UpdateAddress

| Attribute       | Type   | Description |
|-----------------|--------|-------------|
| UserId          | string | The customer identifier. |
| Addresstype     | string | The address type: **Billing**, **Shipping**, **Account**, or **Unknown**. |
| FirstName       | string | The first name that was provided for the address. |
| LastName        | string | The last name that was provided for the address. |
| PhoneNumber     | string | The phone number that was provided for the address. |
| Street1         | string | The first row that was provided for the address. |
| Street2         | string | The second row that was provided for the address. (This value can be blank.) |
| Street3         | string | Third row that was provided for the address. (This value can be blank.) |
| City            | string | The city that was provided for the address. |
| State           | string | The state or province that was provided for the address. |
| District        | string | The district that was provided for the address. (This value can be blank.) |
| ZipCode         | string | The postal code that was provided for the address. |
| CountryCode     | string | The country or region code that was provided for the address. The value should be a two-letter ISO country or region code (for example: **US**). |

### UpdatePaymentInstrument

| Attribute                     | Type     | Description |
| ----------------------------- |----------|-------------|
| UserId                        | string   | The customer identifier. |
| MerchantPaymentInstrumentId   | string   | The identifier of the payment instrument. This information is provided by the merchant. |
| PaymentInstrumenttype         | string   | The type of payment: **CreditCard**, **Paypal**, **Mobilepayment**, or **Giftcard**. |
| PaymentInstrumentcreationDate | DateTime | The date of the first entry for the payment instrument in the merchant's system. The format is ISO 8601. |
| PaymentInstrumentupdateDate   | DateTime | The date of the last update for the payment instrument in the merchant's system. The format is ISO 8601. |
| PaymentInstrumentState        | string   | The state of the payment instrument: **Active**, **Block**, or **Expire**. |
| CardType                      | string   | This attribute is used only for payments of the **CreditCard** type. |
| HolderName                    | string   | The name of the customer of the payment instrument. This attribute is used only for payments of the **CreditCard** type. |
| BIN                           | string   | This attribute is used only for payments of the **CreditCard** type. |
| ExpirationDate                | string   | The expiration date for the payment instrument in the merchant's system. This attribute is used only for payments of the **CreditCard** type. |
| LastFourDigits                | string   | This attribute is used only for payments of the **CreditCard** type. |
| Email                         | string   | The email address that is associated with the payment instrument. This attribute is used only for payments of the **Paypal** type. |
| BillingAgreementId            | string   | This attribute is used only for payments of the **Paypal** type. |
| PayerId                       | string   | This attribute is used only for payments of the **Paypal** type. |
| PayerStatus                   | string   | A value that indicates whether PayPal has verified the payer. This attribute is used only for payments of the **Paypal** type. |
| AddressStatus                 | string   | A value that indicates whether PayPal has verified the payer's address. This attribute is used only for payments of the **Paypal** type. |
| IMEI                          | string   | This attribute is used only for payments of the **Mobilepayment** type. |
| BillingAddressfirstName       | string   | The first name that was provided for address. |
| BillingAddresslastName        | string   | The last name that was provided for address. |
| BillingAddressphoneNumber     | string   | The phone number that was provided for address. The format should be the country or region code followed by a hyphen (-) and then the phone number (for example: for the US, **+1-1234567890**). |
| Street1                       | string   | The first row that was provided for the address. |
| Street2                       | string   | The second row that was provided for the address. (This value can be blank.) |
| Street3                       | string   | Third row that was provided for the address. (This value can be blank.) |
| City                          | string   | The city that was provided for the address. |
| State                         | string   | The state or province that was provided for the address. |
| District                      | string   | The district that was provided for the address. (This value can be blank.) |
| ZipCode                       | string   | The postal code that was provided for the address. |
| CountryCode                   | string   | The country or region code that was provided for the address. The value should be a two-letter ISO country or region code (for example: **US**). |
