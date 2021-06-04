---
author: yvonnedeq
description: This topic outlines the schemas that are required for historical data upload.
ms.author: mapowath
ms.date: 03/08/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: View purchase protection schemas

---

# View purchase protection schemas

This topic outlines the schemas for real-time APIs and historical data that is bulk-uploaded into Microsoft Dynamics 365 Fraud Protection as comma-separated values (CSV) files. For information about the upload procedure, see [Upload historical data](data-upload.md). If data will be ingested via the application programming interface (API), see [Integrate Dynamics 365 Fraud Protection real-time APIs](integrate-real-time-api.md).

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
|MerchantBusinessType  | string    |The business or industry vertical (for example: gaming, retail, dining, or social networking).  |
 |MerchantIdentifier    |string     |The merchant ID (MID) is a specific identification number attached to a business that tells the payment processing systems involved in a transaction where to send which funds. You can think of it like an address for your business. For example, if you don't have a merchant ID, the networks involved won't know where to send your money.  |
 |MerchantCategoryCode  |string     |The merchant category code (MCC) is a four-digit number listed in ISO 18245 for retail financial services. An MCC is used to classify a business by the types of goods or services it provides.  |
 |MerchantBusinessSegment |string   |The subsection of a merchant’s overall operations in which there is an established, separate product line, business line or child brand (for example: Xbox or Surface).  |
 | MerchantProductCategory |string   |The merchant-defined product or service category. |
 |StoreId               |string     |The store identifier.  |
 |StoreName             |string     |The store display name.  |
 |StoreAddress          |string     |The full address (street, city, state, zip) of the store.  |
 |IsTest               |bool        |A value that indicates whether the transaction is a test in production.  |
 |IsFreeProductIncluded |bool      |A value that indicates whether a free product is included in the transaction.|
 |IsGuestCheckout       |bool      |A value that indicates whether the purchase was made as a guest.  |
 |IsPostAuthCheck       |bool      |A value that indicates whether there was a post-authentication check.  |
 |IsRecurringCharge     |bool      |A value that indications whether the transaction was a subscription/recurring.  |
 |RecurringChargeFrequencyInDays  |double    |How often the recurring purchase is being charged, for example, every 30 days, every half year, every year, etc.  |
 |RecurringChargeStartDate |DateTime         |The start date for a recurring transaction.  |
 |RecurringChargeEndDate   |DateTime         |The end date for a recurring transaction.  |
 |IsPostpaid               |bool             |A value that indicates whether a transaction is postpaid or not.  |
|DiscountAmount           |double           |The discount amount applied to the transaction. For example, if a user purchases 10 of the same XBOX controllers, this item will be number **1**. Or, if a user purchase 5 different games and 10 of the same XBOX controllers, this item will be number 5+1, or **6**. |
|TipAmount                |double           |The tip amount applied to the transaction.  |
|DistinctItemCount        |double           |The distinct/unique item count per transaction.  |
|TotalItemCount           |double           |The total item count per transaction. For example, if a user purchases 10 of the same XBOX controllers, this item will be number **10**. Or, if a user purchase 5 different games and 10 of the same XBOX controllers, this item will be number 5+10, or **15**. |
|IsLowLiabilityPIType     |bool             |A value that indicates low liability payment instruments (for example: Apple Pay, Alipay, or UnionPay).  |
|OrderType               |string            |The type of transaction (for example: takeout).  |
|IsRetryOrder             |bool	           |A value that indicates whether the order was retried.  |
| AttemptId                |string           |The identifier for each transaction retry.  |
| ShippingDate             |DateTime         |The date that the order was shipped.  |
| OrderInitiatedChannel    |string           |The channel where the transaction was created (for example: ‘AppStore', 'Web', MobileWeb, 'App', ‘InGamePurchase’).  | 
| OrderInitiatedChannelName   |string        |The App Name or Web URL where the transaction was created.  |
| OrderInitiatedChannelRegionORCountry |string        |The market where the transaction was created (for example: App market).  |
| MerchantBusinessSubSegmentL2   |string       |The second level (L2) business or industry segment.  |
| midName  |  String  |  The merchant name associated with the MID (merchant identifier). | 
| transactionProcessingOrder  |  String  |  The order in which the fraud assessment was made during the transaction flow. | 
| recurringSubscriptionId  |  String  |  The unique ID for the recurring charge | 
| recurringChargeSequence  |  Int32  |  The nth (1, 2, 3...) time the recurring charge has occurred for this customer. | 
| transactionDescription  |  String  |  The transaction processing type | 
| organizationLevel1  |  Object  |  The top level of the organization hierarchy. | 
| organizationLevel2  |  Object  |  The middle level of the organization hierarchy. | 
| organizationLevel3  |  Object  |  The lowest level of the organization hierarchy. | 
| threeDS  |  Object  |  refer to threeDS section | 
| recipientUser  |  Object  |  refer to user section | 
| travelOverview  |  Object  |  refer to Vertical Specific Attributes travelOverview Section | 
| cloudBusiness  |  Object  |  refer to Vertical Specific Attributes clouldBusiness Section | 
| membershipType  |  String  |  The customer's membership status or type. Different levels in paid can be specified such as Premium,Executive. | 
| authenticationMethod  |  String  |  The way in which the customer was authenticated prior/during purchase. | 
| loginInputMethod  |  String  |  The way in which the customer input their credentials. | 
| lastPasswordUpdatedDate  |  DateTimeOffset  |  When the customer's password was last updated. | 
| firstPurchaseDate  |  DateTimeOffset  |  When the customer made their first purchase | 
| loginChallengeType  |  String  |  The type of challenge-response test that was initiated. | 
| httpSignature  |  String  |  The digital signature of the HTTP message. | 
| httpUserAgent  |  String  |  The request header used to identify the application, operating system, vendor, and/or version. | 
| browserHeader  |  String  |  The full list of request headers sent by the browser. | 
| browserResolution  |  String  |  The browser resolution. | 
| browserLanguage  |  String  |  The browser default language preference. | 
| tcpSignature  |  String  |  The TCP application signature. | 
| sslSignature  |  String  |  The SSL signature. | 
| enabledCookies  |  Boolean  |  A True/False value that indicates whether cookies are enabled. | 
| enabledFlash  |  Boolean  |  A True/False value that indicates whether Flash is enabled. | 
| enabledJavaScript  |  Boolean  |  A True/False value that indicates whether javascript is enabled. | 
| screenAspectRatio  |  String  |  The aspect ratio of the browser. | 
| screenColorDepth  |  String  |  The color depth of the screen. | 
| screenResolution  |  String  |  Resolution of device screen in pixels | 
| siteHostName  |  String  |  The site's hostname. | 
| os  |  String  |  The device operating system. | 
| oSFonts  |  String  |  The operating system's default font. | 
| deviceProcessor  |  String  |  The device processor. | 
| sessionId  |  String  |  The unique session ID. | 
| trueIp  |  String  |  True IP address of device identified by device fingerprinting​ | 
| proxyIp  |  String  |  IP address of proxy device. | 
| deviceId  |  String  |  Unique GUID per device generated by device fingerprinting | 
| timeZone  |  String  |  Offset of the local time zone, in hours, with respect to GMT | 
| userAgentDetails  |  String  |  Additional user agent or browser details. | 
| appVersion  |  String  |  Application version. | 
| browserPackagesList  |  String  |  List of packages installed on the device. | 
| buildManufacturer  |  String  |  Manufacturer of the device. | 
| buildModel  |  String  |  User visible name for the end product. | 
| buildSdkVersion  |  String  |  Build version. | 
| dataNetworkType  |  String  |  Type of mobile data network. | 
| deviceModelName  |  String  |  Device model. | 
| deviceSystemName  |  String  |  Device name of the machine. | 
| deviceSystemVersion  |  String  |  Device version. | 
| isBluetoothEnabled  |  Boolean  |  A True/False value that indicates whether bluetooth has been enabled. | 
| simNetworkCountryISO  |  String  |  ISO country code for the mobile service provider. | 
| simNetworkType  |  String  |  Mobile network type. | 
| systemUpTime  |  String  |  The duration of time that the device has been working and available. | 
| paymentMethod  |  String  |  The top-level payment method category. | 
| isLowLiabilityPIType  |  Boolean  |  A True/False value indicating whether the payment method is a low liability. | 
| holderCompanyName  |  Boolean  |  Name of the organization providing the business or company card (for business purchases only). | 
| settlementApprovalRequired  |  Boolean  |  A True/False value inidcating whether or not approval was required for a SEPA transaction. | 
| paymentCheckoutProvider  |  String  |  The eWallet checkout provider. | 
| binName  |  String  |  The BIN display name. | 
| binCountryISO  |  String  |  The ISO country code associated with the BIN. | 
| binCardType  |  String  |  The BIN card type. | 
| binCardAssociation  |  String  |  The BIN card association. | 
| binBankGroup  |  String  |  The BIN bank group. | 
| currency  |  String  |  Currency code for the selected payment instrument. | 
| isInternationalMoneyTransfer  |  Boolean  |  A True/False value indicating whether an international money transfer occurred. | 
| bankIdentifierCode  |  String  |   Bank Identifier Code (BIC or SWIFT code)  | 
| bankName  |  String  |  The bank name | 
| bankZipCode  |  String  |  The bank zip code | 
| bankState  |  String  |  The bank state | 
| bankCountryISO  |  String  |  The bank ISO country | 
| paymentCollectionDate  |  DateTimeOffset  |  The estimated date for payment collection (primarily used for payment service providers). | 
| instantPaymentSettlement  |  Boolean  |  A True/False value indicating bank redirects (used to support CSV payments). | 
| autoCaptureEnabled  |  Boolean  |  A True/False value indicating whether the payment was automatically captured for card payments. For redirect payments this is simply an indicator to the partner bank whether to withdraw funds automatically or not.  | 
| accountType  |  String  |  Indicates the type of account to charge for the transaction. UNSPECIFIED is the default.   | 
| CHEQUE_ACCOUNT uses the card as a debit card. CREDIT_FACILITY uses the card as a credit card. | 
| authorizationType  |  String  |  The authorization type. Mastercard and Visa now require merchants to define authorization attempts as either a pre-authorization or a final-authorization. | 
| authorizationResultCode  |  String  |  Bank response from the authorization decision.  | 
| authorizationResultText  |  String  |  Reasons for the authorization decision; especially for declined or pending transactions.  | 
| acquirerId  |  String  |  Acquiring institution identification code. | 
| acquirerCountryISO  |  String  |  Acquiring institution country code | 
| cvvVerify  |  String  |  Indicates whether CVV verification is available and/or successfully verified.<ul><li>Y = Successfully verified</li><li>N = Not successfully verified</li><li>U = Unavailable</li><li>A = Available, but no verification</li></ul> |  
| avsVerify  |  String  |  Indicates whether addres verification is available and/or sucessfully verified.<ul><li>Y = Successfully verified</li><li>N = Not successfully verified</li><li>U = Unavailable</li><li>A = Available, but no verification</li></ul> | 
| cavVerify  |  String  |  Indicates whether cardholder authentication verification is available and/or sucessfully verified.<ul><li>Y = Successfully verified</li><li>N = Not successfully verified</li><li>U = Unavailable</li><li>A = Available, but no verification</li></ul> | 
| encryptedCreditCardNumber  |  String  |  The hashed or encrypted credit card number. | 
| organizationId  |  String  |  The unique identifier for the merchant or organizaiton. | 
| name  |  String  |  The name of the organization | 
| zipCode  |  String  |  The zipcode at where the organization is located | 
| state  |  String  |  The state at where the organization is located | 
| countryISO  |  String  |  The countryISO at where the organization is located | 
| productBrand  |  String  |  Brand name of the product | 
| buyItAgainOrder  |  Boolean  |  True when users re-order a previous order (not just a product from that order) | 
| preOrderAvailabilityDate  |  DateTimeOffset  |  When the product was first available for preorder | 
| terminalId  |  String  |  The unique identifier for the point of sale terminal  | 
| terminalName  |  String  |  The point of sale terminal name | 
| isThreeDSAuth  |  Boolean  |  A True/False value that indicates whether this transaction is authenticated via 3DS. | 
| messageCategory  |  String  |  Identifies the category of the message for a specific use case. |
| deviceChannel  |  String  |  Indicates the type of channel interface being used to initiate the transaction. |
| threeDSServerTransId  |  String  |  Universally unique transaction identifier assigned by the 3DS Server to identify a single transaction. | 
| threeDSRequestorAuthenticationInd  |  String  | Indicates the type of Authentication request. |
| threeRIInd  |  String  |  Indicates the type of 3RI request. | 
| threeDSReqPriorAuthMethod  |  String  |  Mechanism used by the Cardholder to previously authenticate to the 3DS Requestor. | 
| transStatus  |  String  |  Indicates whether a transaction qualifies as an authenticated transaction or account verification.  | 
| transStatusReason  |  String  |  Provides information on why the Transaction Status field has the specified value. | 
| threeDSCompInd  |  String  |  Indicates whether the 3DS Method successfully completed. | 
| acsChallengeMandated  |  String  |  Indication of whether a challenge is required for the transaction to be authorised due to local/regional mandates or other variable.  | 
| threeDSRequestorChallengeInd  |  String  |  Indicates whether a challenge is requested for this transaction. | 
| challengeCompletionInd  |  String  |  Indicator of the state of the ACS challenge cycle and whether the challenge has completed or will require additional messages. | 
| Values accepted: | 
| eci  |  String  |  Electronic Commerce Indicator (ECI). Payment System-specific value provided by the ACS or DS to indicate the results of the attempt to authenticate the Cardholder.  | 
| shipNameIndicator  |  String  |  Indicates if the Cardholder Name on the account is identical to the shipping Name used for this transaction. | 
| Values accepted: | 
| suspiciousAccActivity  |  String  |  Indicates whether the 3DS Requestor has experienced suspicious activity (including previous fraud) on the cardholder account. | 
| chAccPwChangeInd  |  String  |  Indicates the length of time since the cardholder’s account with the 3DS Requestor had a password change or account reset. | 
| chAccAgeInd  |  String  |  Length of time that the cardholder has had the account with the 3DS Requestor. | 
| provisionAttemptsDay  |  String  |  Number of Add Card attempts in the last 24 hours. | 
| Length: maximum 3 characters <p>Example values:<p><ul><li>2</li><li>02</li><li>002</li></ul> | 
| exemptionRaised  |  String  |  <p>PSD2 exemption requests</p><ul><li>Y - exempted</li><li>N- Not exempted</li></ul> |  


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
 | PISource                     | string   | The payment instrument source (for example: CustomerInput, FromSavedProfile, MobilePay). |

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
| COGS          | double | The cost of goods sold (that is, the raw material cost of the item). This information is provided by the merchant. |
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
| MerchantPaymentInstrumentId | string | Multiple PI scenario & PI change scenario. |
| PaymentMethod | string | Groupings/categories of payment methods. |
| CardType | string | The type of payment. |
| UpdatedPI | string | Used different PI than the one in Purchase? |
| CvvVerify | string | Indicates whether CVV verification is available and/or sucessfully verified.<ul><li>Y = Successfully verified</li><li>N = Not successfully verified</li><li>U = Unavailable</li><li>A = Available, but no verification</li></ul> |
| AvsVerify | string | Indicates whether address verification is available and/or successfully verified.<ul><li>Y = Successfully verified</li><li>N = Not successfully verified</li><li>U = Unavailable</li><li>A = Available, but no verification</li></ul> |
| CavVerify | string | Indicates whether cardholder authentication verification is available and/or sucessfully verified.<ul><li>Y = Successfully verified</li><li>N = Not successfully verified</li><li>U = Unavailable</li><li>A = Available, but no verification</li></ul> |
| AuthorizationResultCode | string | Bank response from the authorization decision. |
| AuthorizationResultText | string | Reasons for the authorization decision; especially for declined or pending transactions. |
| ThreeDS | string | *Refer to Purchase threeDS section in Purchase sheet.* |

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
| MembershipType | string  | The customer's membership status or type.  |
| LoginInputMethod | string |  The method the customer uses to input their credentials. |
| LastPasswordUpdatedDate | string | When the customer's password was last updated. |
| FirstPurchaseDate | string | When the customer made their first purchase. |
| LoginChallengeType | string | The type of challenge-response test that was initiated. |
| AddressList | string | *Refer to Purchase address section.* |
| PaymentInstrumentList | string | *Refer to Purchase paymentInstrumentList section.*  |
| DeviceContext | string | *Refer to Purchase deviceContext section.*  |

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
| Amount           | double   | The amount that was charged to the customer. This information is provided by the merchant. |
| Currency         | string   | The currency of the original purchase as a three-character currency code. (For example: USD, which is aligned with the OANDA currency code). This information is provided by the merchant. |

## Vertical-specific attributes


| Attribute | Vertical | Type | Description |
|--- |--- |--- |---  |
| **travelOverview**  |    |    |   | 
| carRentalIncluded  |  Travel  |  bool  |  A True/False value indicating whether a car rental is included. | 
| lodgingIncluded  |  Travel  |  bool  |  A True/False value indicating whether lodging is included. | 
| travelType  |  Travel  |  string  |  The travel category or type. | 
| isRoundTrip  |  Travel  |  bool  |  A True/False value indicating whether the travel is round trip. | 
| isDiscountOffered  |  Travel  |  bool  |  A True/False value indicating whether a discount was offered. | 
| travelDateTime  |  Travel  |  DateTimeOffset  |  The travel start date and time. | 
| returnDateTime  |  Travel  |  DateTimeOffset  |  The travel end or return date and time. | 
| fromCity  |  Travel  |  string  |  The city where the customer is travelling from. | 
| fromState  |  Travel  |  string  |  The state where the customer is travelling from. | 
| fromCountryISO  |  Travel  |  string  |  The ISO country where the customer is travelling from. | 
| fromZipCode  |  Travel  |  string  |  The zip code where the customer is travelling from. | 
| toCity  |  Travel  |  string  |  The city where the customer is travelling to. | 
| toState  |  Travel  |  string  |  The state where the customer is travelling to. | 
| toCountryISO  |  Travel  |  string  |  The ISO country where the customer is travelling to. | 
| toZipCode  |  Travel  |  string  |  The zip code where the customer is travelling to. | 
| travelDuration  |  Travel  |  string  |  Deprecating (Don't use) | 
| isPackagedTour  |  Travel  |  bool  |  A True/False value indicating whether this was a packaged tour. | 
| bookingType  |  Travel  |  string  |  The booking type. | 
| webUrl  |  Travel  |  string  |  The URL where the travel was booked. | 
| issueDateTime  |  Travel  |  DateTimeOffset  |  The date and time when the tickets were issued. | 
| flightDetails  |  Travel  |  object  |  refer to flightDetails section | 
| lodgingDetails  |  Travel  |  object  |  refer to lodgingDetails section | 
| carRentalDetails  |  Travel  |  object  |  refer to carRentalDetails section | 
| travelAgent  |  Travel  |  object  |  refer to travelAgent section | 
| **flightDetails**  |    |    |   | 
| ticketNumber  |  Travel  |  string  |  The unique ticket number. | 
| placeOfIssue  |  Travel  |  string  |  The location where the ticket was issued. | 
| isRestrictedTicket  |  Travel  |  bool  |  A True/False value indicating whether the ticket is restricted. | 
| rewardsOrVoucherApplied  |  Travel  |  bool  |  A True/False value indicating whether rewards or vouchers were applied to the order. | 
| totalRewardsApplied  |  Travel  |  int32  |  The total rewards which were applied to the order. | 
| totalFees  |  Travel  |  decimal  |  The total fees applied to the order. | 
| passengerCount  |  Travel  |  Int32  |  The total number of passengers. | 
| numberOfStops  |  Travel  |  Int32  |  The number of stops or layovers for the flight. | 
| purchaserProfileType  |  Travel  |  string  |  The customer's profile or membership type. | 
| isThirdParty  |  Travel  |  bool  |  A True/False value indicating whether the order was placed through a third party site. | 
| isPurchaserFrequentFlyer  |  Travel  |  bool  |  A True/False value indicating whether the customer is a frequent flyer. | 
| flightSegments  |  Travel  |  object  |  refer to flightSegements section | 
| passengers  |  Travel  |  object  |  refer to passengers section | 
| **flightSegments**  |    |    |   | 
| airlineCode  |  Travel  |  string  |  The airline code. | 
| airlineName  |  Travel  |  string  |  The airline name. | 
| segmentSequence  |  Travel  |  Int32  |  The sequence number of the given flight leg (e.g. 2 for the second leg of the flight) | 
| travelClass  |  Travel  |  string  |  The seat class or cabin. | 
| operatedBy  |  Travel  |  string  |  The organization operating the flight. | 
| flightNumber  |  Travel  |  string  |  The flight number. | 
| fromAirportCode  |  Travel  |  string  |  The airport code where the flight is flying from. | 
| toAirportCode  |  Travel  |  string  |  The airport code where the flight is flying to. | 
| departureDateTime  |  Travel  |  DateTimeOffset  |  The departure date and time. | 
| arrivalDateTime  |  Travel  |  DateTimeOffset  |  The arrival date and time. | 
| fromAirportCity  |  Travel  |  string  |  The airport city where the customer is travelling from. | 
| fromAirportState  |  Travel  |  string  |  The  airport state where the customer is travelling from. | 
| fromAirportZipcode  |  Travel  |  string  |  The airport zip code where the customer is travelling from. | 
| fromAirportCountryISO  |  Travel  |  string  |  The airport ISO country where the customer is travelling from. | 
| toAirportCity  |  Travel  |  string  |  The airport city where the customer is travelling to. | 
| toAirportState  |  Travel  |  string  |  The airport state where the customer is travelling to. | 
| toAirportZipcode  |  Travel  |  string  |  The airport zip code where the customer is travelling to. | 
| toAirportCountryISO  |  Travel  |  string  |  The airport ISO country where the customer is travelling to. | 
| **passengers**  |    |    |   | 
| firstName  |  Travel  |  string  |  The passenger first name. | 
| lastName  |  Travel  |  string  |  The passenger last name. | 
| **carRentalDetails**  |    |    |   | 
| pickupLocation  |  Travel  |  string  |  The car rental pickup location. | 
| pickupDateTime  |  Travel  |  DateTimeOffset  |  The car rental pickup date and time. | 
| dropOffLocation  |  Travel  |  string  |  The car rental drop-off location. | 
| dropOffDateTime  |  Travel  |  DateTimeOffset  |  The car rental drop-off date and time | 
| discountProgram  |  Travel  |  string  |  The discount program applied to the car rental order. | 
| carType  |  Travel  |  string  |  The car type or category. | 
| isPrepaid  |  Travel  |  bool  |  A True/False value indicating whether the car rental was prepaid. | 
| insuranceIncluded  |  Travel  |  bool  |  A True/False value indicating whether insurance was included. | 
| contactEmail  |  Travel  |  string  |  The car renter's email address. | 
| contactPhoneNumber  |  Travel  |  string  |  The car renter's phone number. | 
| pickupAddress  |  Travel  |  object  |  refer to address section | 
| dropOffAddress  |  Travel  |  object  |  refer to address section | 
| **travelAgent**  |    |    |   | 
| agencyCode  |  Travel  |  string  |  The travel agency code. | 
| agencyName  |  Travel  |  string  |  The travel agency name. | 
| agentCode  |  Travel  |  string  |  The trave agent code. | 
| agencyLocation  |  Travel  |  object  |  refer to agentAddress section | 
| **agentAddress**  |    |    |   | 
| street1  |  Travel  |  string  |  The first row that was provided for the address | 
| street2  |  Travel  |  string  |  The second row that was provided for the address. (This value can be blank.) | 
| street3  |  Travel  |  string  |  The third row that was provided for the address. (This value can be blank.) | 
| city  |  Travel  |  string  |  The city that was provided for the address. | 
| state  |  Travel  |  string  |  The state or province that was provided for the address. | 
| district  |  Travel  |  string  |  The district that was provided for the address. | 
| zipCode  |  Travel  |  string  |  The postal code that was provided for the address. | 
| country  |  Travel  |  string  |  The country/region code that was provided for the address. The value should be a two-letter ISO country/region code (for example, US). | 
| agencyContactPhone  |  Travel  |  string  |  The agency contact phone number | 
| agencyContactEmail  |  Travel  |  string  |  The agency contact email address | 
| **lodgingDetails**  |    |    |   | 
| folioNumber  |  Lodging  |  string  |  The unique identifier of the lodging property. | 
| CheckInDate  |  Lodging  |  DateTimeOffset  |  The check-in date for the lodging stay. | 
| CheckOutDate  |  Lodging  |  DateTimeOffset  |  The check-out date for the lodging stay. | 
| reservationConfirmed  |  Lodging  |  bool  |  A True/False value indicating whether the reservation has been confirmed. | 
| membershipDetails  |  Lodging  |  string  |  Additional details on the customer's membership status. | 
| discountProgram  |  Lodging  |  string  |  The discount program applied to the lodging order. | 
| adultCount  |  Lodging  |  Int32  |  The number of adults included in the stay. | 
| kidCount  |  Lodging  |  Int32  |  The number of kids included in the stay. | 
| nightsCount  |  Lodging  |  Int32  |  The number of nights included in the stay. | 
| roomCount  |  Lodging  |  Int32  |  The number of rooms included in the stay. | 
| bedType  |  Lodging  |  string  |  The bed type or category. | 
| roomType  |  Lodging  |  string  |  The room type or category. | 
| paymentDescription  |  Lodging  |  string  |  Additional details on the loding payment. | 
| facility  |  Lodging  |  object  |  refer to facility section | 
| **facility**  |    |    |   | 
| name  |  Lodging  |  string  |  The facility name. | 
| type  |  Lodging  |  string  |  The facility type. | 
| contactPhoneNumber  |  Lodging  |  string  |  The phone number used to contact the facility. | 
| contactEmail  |  Lodging  |  string  |  The email address used to contact the facility. | 
| dailyRoomRate  |  Lodging  |  decimal  |  The daily room rate for the facility. | 
| currency  |  Lodging  |  string  |  The currency supported by the facility. | 
| dailyRoomTaxAmount  |  Lodging  |  decimal  |  The daily room tax amount charged by the facility. | 
| address  |  Lodging  |  object  |  refer to address section | 
| **address**  |    |    |   | 
| street1  |  Car Rental  |  string  |  The first row that was provided for the address | 
| street2  |  Car Rental  |  string  |  The second row that was provided for the address. (This value can be blank.) | 
| street3  |  Car Rental  |  string  |  The third row that was provided for the address. (This value can be blank.) | 
| city  |  Car Rental  |  string  |  The city that was provided for the address. | 
| state  |  Car Rental  |  string  |  The state or province that was provided for the address. | 
| district  |  Car Rental  |  string  |  The district that was provided for the address. | 
| zipCode  |  Car Rental  |  string  |  The postal code that was provided for the address. | 
| country  |  Car Rental  |  string  |  The country/region code that was provided for the address. The value should be a two-letter ISO country/region code (for example, US). | 
| **cloudBusiness**  |    |    |   | 
| organizationId  |  CloudBusiness  |  string  |  The unique identifier for the cloud service or organization. | 
| companyName  |  CloudBusiness  |  string  |  The cloud service name. | 
| companyType  |  CloudBusiness  |  string  |  The cloud company type. | 
| companySize  |  CloudBusiness  |  Int32  |  The cloud company size. | 
| entityId  |  CloudBusiness  |  string  |  The unique identifier for the legal entity under the organization. | 
| primaryContactFirstName  |  CloudBusiness  |  string  |  The first name of the primary contact for the business. | 
| primaryContactLastName  |  CloudBusiness  |  string  |  The last name of the primary contact for the business. | 
| primaryContactEmail  |  CloudBusiness  |  string  |  The email address of the primary contact for the business. | 
| primaryContactPhoneNumber  |  CloudBusiness  |  string  |  The phone number of the primary contact for the business. | 
| subscriptionCount  |  CloudBusiness  |  Int32  |  The total number of subscriptions available. | 
| companyAddress  |  CloudBusiness  |  object  |  Refer to address section | 

## Download sample data

You can download our sample data files to explore options before using your own internal data.
- For samples you can use with loss prevention, select [Loss prevention sample data file](https://download.microsoft.com/download/3/1/6/316b5f40-287d-48a3-ab3c-bf4c7a171cfc/LP1.zip.).
- For samples you can use with purchase protection, select [Purchase protection sample data file](https://download.microsoft.com/download/c/6/a/c6a37f61-1d4c-4357-8b3c-0a6d78bcb3a1/PP1.zip).


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



[!INCLUDE[footer-include](includes/footer-banner.md)]
