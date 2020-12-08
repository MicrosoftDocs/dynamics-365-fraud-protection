---
author: yvonnedeq
description: This topic outlines the schemas that are required for historical data upload.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 11/19/2020
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: View purchase protection schemas (INT only)

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
| UserId              | string   | The customer identifier. This information is provided by the merchant. This attribute is required.|
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
| CustomData          | object   | An optional user-defined JavaScript Object Notation (JSON) property bag. It's filled in when an API call is instantiated. The attributes can be referenced when you create purchase rules.<p>**Note:**</p><ul><li>The following primitive types are supported: **String (Unicode)**, **Int32**, **UInt32**, **Double**, **Boolean**, and **DateTime** (in Coordinated Universal Time \[UTC\], in conformance to .NET semantics).</li><li>The string data limit is 256 characters.</li><li>There is a limit of 100 custom attributes per payload.</li><li>Don't send sensitive or highly regulated data types. Here are some examples:<ul><li>Data that indicates a protected class (such as gender or race) or private/sensitive categories (such as religious views or sexual orientation)</li><li>Biometric data or any data that is related to health</li></ul></li><li>The custom data retention policy matches the retention policy of the purchase event (six months).</li></ul><p>For a sample that shows how to use purchase APIs with a custom data object in Fraud Protection, see the [Custom data sample](schema-INT.md#custom-data-sample) section at the end of this topic.</p>  |
| MerchantBusinessType  | string    |The business or industry vertical (for example: gaming, retail, dining, or social networking).  |
| MerchantIdentifier    |string     |The merchant ID (MID) is a specific identification number attached to a business that tells the payment processing systems involved in a transaction where to send which funds. You can think of it like an address for your business. For example, if you don't have a merchant ID, the networks involved won't know where to send your money.  |
| MerchantCategoryCode  |string     |The merchant category code (MCC) is a four-digit number listed in ISO 18245 for retail financial services. An MCC is used to classify a business by the types of goods or services it provides.  |
| MerchantBusinessSegment |string   |The subsection of a merchant’s overall operations in which there is an established, separate product line, business line, or child brand (for example: Xbox or Surface).  |
| MerchantProductCategory |string   |The merchant-defined product or service. |
| StoreId               |string     |The store identifier.  |
| StoreName             |string     |The store display name.  |
| StoreAddress          |string     |The full address (street, city, state, zip) of the store.  |
| IsTest               |bool        |A value that indicates whether the transaction is a test in production.  |
| IsFreeProductIncluded |bool      |A value that indicates whether a free product is included in the transaction.|
| IsGuestCheckout       |bool      |A value that indicates whether the purchase was made as a guest.  |
| IsPostAuthCheck       |bool      |A value that indicates whether there was a post-authentication check.  |
| IsRecurringCharge     |bool      |A value that indications whether the transaction was a subscription/recurring.  |
| RecurringChargeFrequencyInDays  |double    |How often the recurring purchase is being charged, for example, every 30 days, every half year, every year, etc.  |
| RecurringChargeStartDate |DateTime         |The start date for a recurring transaction.  |
| RecurringChargeEndDate   |DateTime         |The end date for a recurring transaction.  |
| IsPostpaid               |bool             |A value that indicates whether a transaction is postpaid or not.  |
| DiscountAmount           |double           |The discount amount applied to the transaction.  |
| TipAmount                |double           |The tip amount applied to the transaction.  |
| DistinctItemCount        |double           |The distinct/unique item count per transaction. For example, if a user purchases 10 of the same XBOX controllers, this item will be number **1**. Or, if a user purchase 5 different games and 10 of the same XBOX controllers, this item will be number 5+1, or **6**.  |
| TotalItemCount           |double           |The total item count per transaction. For example, if a user purchases 10 of the same XBOX controllers, this item will be number **10**. Or, if a user purchase 5 different games and 10 of the same XBOX controllers, this item will be number 5+10, or **15**. |
| IsLowLiabilityPIType     |bool             |A value that indicates low liability payment instruments (for example: Apple Pay , Alipay, or UnionPay).  |
| OrderType                |string           |The type of transaction (for example: takeout) .  |
| IsRetryOrder             |bool	            |A value that indicates whether the order was retried.  |

### PaymentInstruments

| Attribute                   | Type     | Description |
|-----------------------------|----------|-------------|
| PurchaseId                  | string   | The identifier of the transaction (or purchase or order). |
| MerchantPaymentInstrumentId | string   | The identifier of the payment instrument. This information is provided by the merchant. This is a required attribute.|
| Type                        | string   | The type of payment. For more information, see [Dynamics 365 Fraud Protection API](https://apidocs.microsoft.com/services/dynamics365fraudprotection#/v1.0/V1.0MerchantservicesEventsPurchasePost). |
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
| PISource                    | string   | The payment instrument source (for example: CustomerInput, FromSavedProfile, MobilePay). |

### Products

| Attribute     | Type   | Description |
|---------------|--------|-------------|
| PurchaseId    | string | The identifier of the transaction (or purchase or order). |
| ProductId     | string | The product identifier. This is a required attribute.|
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
| Status             | string   | The status. For more information, see [Dynamics 365 Fraud Protection API](https://apidocs.microsoft.com/services/dynamics365fraudprotection#/v1.0/V1.0MerchantservicesEventsPurchasePost). |
| BankEventTimestamp | DateTime | The timestamp from the bank. The format is ISO 8601. |
| Amount             | double   | The chargeback amount. |
| Currency           | string   | The currency that is used for the chargeback amount. |
| UserId             | string   | The customer identifier.|
| PurchaseId         | string   | The identifier of the transaction (or purchase or order). |
| MerchantLocalDate  | DateTime | The purchase ingestion date in the merchant's local time zone. The format is ISO 8601. |

## Refunds

The following schema is used in the Evaluate and Protect experiences.

| Attribute          | Type     | Description |
|--------------------|----------|-------------|
| RefundId           | string   | The refund identifier. |
| Reason             | string   | The customer-provided reason. |
| Status             | string   | The refund status. For more information, see [Dynamics 365 Fraud Protection API](https://apidocs.microsoft.com/services/dynamics365fraudprotection#/v1.0/V1.0MerchantservicesEventsPurchasePost). |
| BankEventTimestamp | DateTime | The timestamp from the bank. The format is ISO 8601. |
| Amount             | double   | The refund amount. |
| Currency           | string   | The currency that is used for the sales price amount. |
| UserId             | string   | The customer identifier. This is a required attribute.|
| PurchaseId         | string   | The identifier of the transaction (or purchase or order). |
| MerchantLocalDate  | DateTime | A date in ISO 8601 format. |

## PurchaseStatus

The following schema is used in the Evaluate and Protect experiences.

| Attribute         | Type     | Description |
|-------------------|----------|-------------|
| PurchaseId        | string   | The identifier of the transaction (or purchase or order). |
| StatusType        | string   | The type of status. For more information, see [Dynamics 365 Fraud Protection API](https://apidocs.microsoft.com/services/dynamics365fraudprotection#/v1.0/V1.0MerchantservicesEventsPurchasePost). |
| StatusDate        | DateTime | The date and time when the status was applied. The format is ISO 8601. |
| Reason            | string   | The reason for the status transition. |
| MerchantLocalDate | DateTime | A date in ISO 8601 format. |

## BankEvents

The following schema is used in the Evaluate and Protect experiences.

| Attribute          | Type     | Description |
|--------------------|----------|-------------|
| BankEventId        | string   | The bank event identifier. |
| Type               | string   | The bank event type. For more information, see [Dynamics 365 Fraud Protection API](https://apidocs.microsoft.com/services/dynamics365fraudprotection#/v1.0/V1.0MerchantservicesEventsPurchasePost). |
| BankEventTimestamp | DateTime | The timestamp from the bank. The format is ISO 8601. |
| Status             | string   | The status. For more information, see [Dynamics 365 Fraud Protection API](https://apidocs.microsoft.com/services/dynamics365fraudprotection#/v1.0/V1.0MerchantservicesEventsPurchasePost). |
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
| UserId                   | string   | The customer identifier. This is a required attribute.|
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
| UserId          | string | The customer identifier. This is a required attribute.|
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
| UserId                        | string   | The customer identifier. This is a required attribute.|
| MerchantPaymentInstrumentId   | string   | The identifier of the payment instrument. This information is provided by the merchant. This is a required attribute.|
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

## Labels

The following schema is used in the Evaluate and Protect experiences.

| Attribute | Type | Description |
| --- | --- | --- |
| TrackingId | String | The unique ID for each event/record. |
| MerchantLocalDate | DateTime | The date in the merchant&#39;s time zone. The format is ISO 8601.  |
| EventTimeStamp | DateTime | The date and time of the event. The format is ISO 8601. For more information, see [Dynamics 365 Fraud Protection API](https://apidocs.microsoft.com/services/dynamics365fraudprotection#/v1.0/V1.0MerchantservicesEventsPurchasePost). |
| LabelObjectType | String | This field indicates the type of label: Purchase, Signup, Custom Fraud Evaluation, Account, Payment instrument, or Email. |
| LabelObjectId | String | This is an identifier field for the type of object: PurchaseId, SignupId, UserId, MerchantPaymentInstrumentId, or Email.  |
| LabelSource | String | This field represents the source of the label. For more information, see [Dynamics 365 Fraud Protection API](https://apidocs.microsoft.com/services/dynamics365fraudprotection#/v1.0/V1.0MerchantservicesEventsPurchasePost). |
| LabelState | String | This field indicates the current status of the label. For more information, see [Dynamics 365 Fraud Protection API](https://apidocs.microsoft.com/services/dynamics365fraudprotection#/v1.0/V1.0MerchantservicesEventsPurchasePost).  |
| LabelReasonCodes | String | This field indicates the reason codes associated with each type of label. For more information, see [Dynamics 365 Fraud Protection API](https://apidocs.microsoft.com/services/dynamics365fraudprotection#/v1.0/V1.0MerchantservicesEventsPurchasePost). |
| Processor | String | The name of the bank or payment processor. For more information, see [Dynamics 365 Fraud Protection API](https://apidocs.microsoft.com/services/dynamics365fraudprotection#/v1.0/V1.0MerchantservicesEventsPurchasePost). |
| EffectiveStartDate | DateTime | The date from which this label is effective. The format is ISO 8601. |
| EffectiveEndDate | DateTime | The end date for this label. The format is ISO 8601. |

## Download sample data
You can download our [sample data file](https://download.microsoft.com/download/c/6/a/c6a37f61-1d4c-4357-8b3c-0a6d78bcb3a1/DFP_External_Sample_Data.zip) to explore options before using your own internal data.

### Custom data sample

The following sample shows how to use purchase APIs with a custom data object in Fraud Protection.

```json
{ 
"CustomData": { 
"EngagementDuration": 120.4, 
"GamerScore": 10, 
"InApp": true, 
"MiscSampleA": "abc" 
} 
}
```

