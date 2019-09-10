---
author: jegrif
description: This topic outlines the schemas that are required for signup under account creation assessment.
ms.author: v-jegrif
ms.service: crm-online
ms.date: 09/04/2019

ms.topic: conceptual
title: View account creation assessment schemas -  Sign-up
---

# View account creation assessment schemas - Sign-up

This topic outlines the schemas for the Signup data for account creation assessment. For SignupStatus, see [this accompanying page](signup-status-schema.md).

Note the following formatting guidelines throughout:

- The files are in CSV UTF-8 (comma delimited) format (\*.csv).
- The maximum file size is 10 gigabytes (GB).
- The **DateTime** columns are in ISO 8601 format. For example, **DateTime.UtcNow.ToString("o")** might have the result **"2019-03-14T20:18:11.254Z"**.
- The decimal precision is two decimal places.
- The following characters are escaped in all columns: commas, new line characters, and multiline characters.

## Signup schema

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| trackingId | string | The identifier of the Signup event. |

## Data

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| signUpId | string | The identifier of the Signup event (can match trackingId). |
| assessmentType | string | Indicates the assessment type for the event. Possible values are 'evaluate' or 'protect'. If not specified, the default is 'protect''. |
| customerLocalDate | dateTime | The Signup creation date in the customer's local time zone. The format is ISO 8601. |
| merchantLocalDate | dateTime | The Signup ingestion date in the merchant's time zone. The format is ISO 8601. |

### Data \ User

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| userId | string | The user identifier. This information is provided by the merchant. |

### Data \ User \ UserDetails

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| userId | string | The user identifier. This information is provided by the merchant. |
| creationDate | dateTime | The creation date of the user account. The format is ISO 8601. |
| updateDate | dateTime | The date when user data was last changed. The format is ISO 8601. |
| firstName | string | The user-provided first name on the account. |
| lastName | string | The user-provided last name on the account. |
| country | string | The user's country or region. The value should be a two-letter ISO country/region code (for example, US). |
| zipCode | string | The user's postal code. |
| timeZone | string | The user's time zone. |
| language | string | The user's language and territory (for example, EN-US). |
| phoneNumber | string | The user's phone number. The format should be the country/region code followed by a hyphen (-) and then the phone number (for example, for the US, +1-1234567890). |
| email | string | The user's email address. This value is case-insensitive. |
| membershipId | string | The membership ID, if the user already has an existing membership with the merchant. |
| profileType | string | The user's profile type. Possible values: Consumer, Developer, Seller, Publisher, Tenant |
| profileName | string | The profile name, depending on profileType. |
| authenticationProvider | string | The user's authentication provider, if different from the merchant's. Examples include Windows Live, Facebook, Google, etc. |
| displayName | string | The user's display name. Example: Xbox gamertag value |
| isEmailValidated | bool | A True/False value that indicates whether the user-provided email address has been verified as owned by the user. |
| emailValidatedDate | dateTime | The validation date of the user email. The format is ISO 8601. |
| isPhoneNumberValidated | bool | A True/False value that indicates whether the user-provided phone number has been verified as owned by the user. |
| phoneNumberValidatedDate | dateTime | The validation date of the user phone number. The format is ISO 8601. |

### Data \ User \ SignUpAddress

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| firstName | string | The user-provided first name associated with the address. |
| lastName | string | The user-provided last name associated with the address. |
| phoneNumber | string | The user-provided phone number associated with the address. |

### Data \ User \ SignUpAddressDetails

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| street1 | string | The first row that was provided for the address. |
| street2 | string | The second row that was provided for the address. (This value can be blank.) |
| street3 | string | The third row that was provided for the address. (This value can be blank.) |
| city | string | The city that was provided for the address. |
| state | string | The state or province that was provided for the address. |
| district | string | The district that was provided for the address. |
| zipCode | string | The postal code that was provided for the address. |
| country | string | The country/region code that was provided for the address. The value should be a two-letter ISO country/region code (for example, US). |

### Data \ PaymentInstrument

### Data \ PaymentInstrument \ PaymentInstrumentDetails

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| merchantPaymentInstrumentId | string | The identifier of the payment instrument. This information is provided by the merchant. |
| type | string | The type of payment: CreditCard, Paypal, Mobilepayment, Giftcard, etc. |
| creationDate | DateTime | The date of the first entry for the payment instrument in the merchant's system. The format is ISO 8601. |
| updateDate | DateTime | The date of the last update for the payment instrument in the merchant's system. The format is ISO 8601. |
| state | string | The current state of the PI in merchant's system. Sample: Active, Blocked, Expired |
| cardType | string | This attribute is used only for payments of the Credit/Debit Card type. |
| holderName | string | The name of the payment instrument's user. This attribute is used only for payments of the Credit/Debit Card type. |
| bin | string | This attribute is used only for payments of the Credit/Debit Card type. |
| expirationDate | string | The expiration date for the payment instrument in the merchant's system. The format is ISO 8601. This attribute is used only for payments of the Credit/Debit Card type. |
| lastFourDigits | string | This attribute is used only for payments of the Credit/Debit Card type. |
| email | string | The email address associated with the payment instrument. This attribute is used only for payments of the Paypal type. |
| billingAgreementId | string | This attribute is used only for payments of the Paypal type. |
| payerId | string | This attribute is used only for payments of the Paypal type. |
| payerStatus | string | A value that indicates whether PayPal has verified the payer. This attribute is used only for payments of the Paypal type. |
| addressStatus | string | A value that indicates whether PayPal has verified the payer's address. This attribute is used only for payments of the Paypal type. |
| imei | string | This attribute is used only for payments of the Mobilepayment type. |

### Data \ PaymentInstrument \ BillingAddress

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| firstName | string | The user-provided first name associated with the address. |
| lastName | string | The user-provided last name associated with the address. |
| phoneNumber | string | The user-provided phone number associated with the address. |

### Data \ PaymentInstrument \  BillingAddressDetails

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| street1 | string | The first row that was provided for the address. |
| street2 | string | The second row that was provided for the address. (This value can be blank.) |
| street3 | string | The third row that was provided for the address. (This value can be blank.) |
| city | string | The city that was provided for the address. |
| state | string | The state or province that was provided for the address. |
| district | string | The district that was provided for the address |
| zipCode | string | The postal code that was provided for the address. |
| country | string | The country/region code that was provided for the address. The value should be a two-letter ISO country/region code (for example, US). |

### Data \ MarketingContext

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| type | string | The marketing type. Possible values: None, Email, Referral, SearchEngine, Direct, SocialNetwork, Other |
| trafficSource | string | The source of this user if known. If via Referral, provide the MerchantUserId of the referrer. |
| incentiveType | string | The incentive type for the new user. Possible values: None, CashBack, Discount, FreeTrial, BonusPoints, Gift, Other |
| incentiveOffer | string | The exact incentive offer name. Examples: $5 off on first order, free shipping, 5000 points |

### Data \ StoreFrontContext

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| type | string | The type of the storefront. Possible values: None, Web, Console, MobileApp, ComputerApp, MobileWeb |
| storeName | string | The exact name of your storefront through which the customer is trying to sign up. |
| marketingContext | string | The region or market. The value should be a two-letter ISO country/region code (for example, US). |

### Data \ DeviceContext

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| deviceContextId | string | The customer's Session ID (mastered by GreenId), or the event ID if the session is not available. |
| ipAddress | string | The customer's IP address (as provided by the merchant). |

### Data \ DeviceContext \ DeviceContextDetails

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| provider | string | The provider of device info. Possible values are 'DFPFINGERPRINTING' or 'MERCHANT'. If not specified, the default is 'DFPFINGERPRINTING'. |
| deviceContextDC | string | The GreenID datacenter for the Customer's Session ID. |
| externalDeviceId | string | The customer's device ID, as provided and mastered by the merchant. |
| externalDeviceType | string | The customer's device type, as provided and mastered by the merchant. |
