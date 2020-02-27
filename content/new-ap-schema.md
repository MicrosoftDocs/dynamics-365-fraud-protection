---
author: v-davido
description: This topic outlines the schemas that are used in account protection.
ms.author: kelsiefu 
ms.service: fraud-protection
ms.date: 02/24/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Account protection schemas

---

# Account protection schemas

[!include [banner](includes/preview-banner.md)]

This topic outlines the schemas for historical data that is uploaded in bulk into Microsoft Dynamics 365 Fraud Protection as comma-separated values (CSV) files. For information about the upload procedure, see [Upload historical data](https://docs.microsoft.com/dynamics365/fraud-protection/data-upload). If data will be ingested via the application programming interface (API), see [Integrate Dynamics 365 Fraud Protection real-time APIs](https://docs.microsoft.com/dynamics365/fraud-protection/integrate-real-time-api).

Note the following formatting guidelines throughout:

- The files are in CSV UTF-8 (comma-delimited) format (\*.csv).
- The maximum file size is 10 gigabytes (GB).
- The **DateTime** columns are in International Organization for Standardization (ISO) 8601 format. For example, **DateTime.UtcNow.ToString("o")** might have the result **"2019-03-14T20:18:11.254Z"**.
- The decimal precision is two decimal places.
- The following characters are escaped in all columns: commas, new line characters, and multiline characters.

## AccountCreation

The **AccountCreation** API lets you share information and context with Fraud Protection about incoming new account creation events for risk assessment.

| Object                              | Attribute                   | Type     | Description |
|-------------------------------------|-----------------------------|----------|-------------|
|                                     | Name                        | string   | The value is **"AP.AccountCreation"**. |
|                                     | Version                     | string   | The value is **"0.5"**. |
| MetaData                            | trackingId                  | string   | The identifier of the **Signup** event. |
| MetaData                            | signUpId                    | string   | The identifier of the **Signup** event. (This value can match the value of the **trackingId** attribute.) |
| MetaData                            | assessmentType              | string   | The assessment type for the event. Possible values are **'evaluate'** and **'protect'**. If no value is specified, the default value is **'protect'**. |
| MetaData                            | customerLocalDate           | dateTime | The creation date of the **Signup** event, in the customer's local time zone. The format is ISO 8601. |
| MetaData                            | merchantTimeStamp           | dateTime | The time stamp for the event. |
| DeviceContext                       | SessionID                   | string   | The customer's session ID. This information is mastered by DFP Device Fingerprinting Service. |
| DeviceContext                       | ipAddress                   | string   | The customer's IP address, as provided by the merchant. |
| DeviceContext                       | provider                    | string   | The provider of device information. Possible values are **'DFPFingerprinting'** and **'Merchant'**. If no value is specified, the default value is **'DFPFingerprinting'**. |
| DeviceContext                       | externalDeviceId            | string   | The customer's device ID, as provided and mastered by the merchant. |
| DeviceContext                       | externalDeviceType          | string   | The customer's device type, as provided and mastered by the merchant. Possible values are **'Mobile'**, **'Computer'**, **'MerchantHardware'**, **'Tablet'**, and **'GameConsole'**. |
| User                                | userId                      | string   | The user identifier. This information is provided by the merchant. |
| User                                | userType                    | string   | The user's profile type. Possible values are **'Consumer'**, **'Developer'**, **'Seller'**, **'Publisher'**, and **'Tenant'**. |
| User                                | UserName                    | string   | The user-provided user name that is unique in the merchant system. |
| User                                | passwordHash                | string   | The user-provided password that is hashed in the merchant system. |
| User                                | firstName                   | string   | The user-provided first name on the account. |
| User                                | lastName                    | string   | The user-provided last name on the account. |
| User                                | country                     | string   | The user's country or region. The value should be a two-letter ISO country/region code (for example, **US**). |
| User                                | zipCode                     | string   | The user's postal code. |
| User                                | timeZone                    | string   | The user's time zone. |
| User                                | language                    | string   | The user's language and territory (for example, **EN-US**). |
| User                                | membershipId                | string   | The membership ID, if the user already has an existing membership with the merchant. |
| User                                | isMembershipIdUserName      | bool     | A **True**/**False** value that indicates whether the **membershipId** value can be used as the user name. The default value is **False**. |
| User \\ phone                       | phoneType                   | enum     | The type of phone number. Possible values are **'Primary'** and **'Alternative'**. The default value is **'Primary'**. |
| User \\ phone                       | phoneNumber                 | string   | The user's phone number. The format should be the country/region code followed by a hyphen (\-) and then the phone number (for example, for the US, **+1-1234567890**). |
| User \\ phone                       | isPhoneNumberValidated      | bool     | A **True**/**False** value that indicates whether the user-provided phone number has been verified as owned by the user. |
| User \\ phone                       | phoneNumberValidatedDate    | dateTime | The validation date of the user's phone number. The format is ISO 8601. |
| User \\ phone                       | isPhoneUserName             | bool     | A **True**/**False** value that indicates whether the phone number can be used as the user name. The default value is **False**. |
| User \\ Email                       | emailType                   | enum     | The type of email address. Possible values are **'Primary'** and **'Alternative'**. |
| User \\ Email                       | email                       | string   | The user's email address. This value is case-insensitive. |
| User \\ Email                       | isEmailValidated            | bool     | A **True**/**False** value that indicates whether the user-provided email address has been verified as owned by the user. |
| User \\ Email                       | emailValidatedDate          | dateTime | The validation date of the user's email address. The format is ISO 8601. |
| User \\ Email                       | isEmailUserName             | bool     | A **True**/**False** value that indicates whether the email address can be used as the user name. The default value is **False**. |
| User \\ SSOAuthenticationProvider   | authenticationProvider      | string   | The user's single sign-on (SSO) authentication provider, if it differs from the merchant's SSO authentication provider. Possible values are **'MSA'**, **'Facebook'**, **'PSN'**, **'MerchantAuth'**, and **'Google'**. |
| User \\ SSOAuthenticationProvider   | displayName                 | string   | The user's display name for the SSO authentication provider (for example, the user name from a Microsoft account, Facebook, or Google). |
| User \\ Address                     | addressType                 | enum     | The type of address. Possible values are **'Primary'**, **'Billing'**, **'Shipping'**, and **'Alternative'**. The default value is **'Primary'**. |
| User \\ Address                     | firstName                   | string   | The user-provided first name that is associated with the address. |
| User \\ Address                     | lastName                    | string   | The user-provided last name that is associated with the address. |
| User \\ Address                     | phoneNumber                 | string   | The user-provided phone number that is associated with the address. |
| User \\ Address                     | street1                     | string   | The first row that was provided for the address. |
| User \\ Address                     | street2                     | string   | The second row that was provided for the address. (This value can be blank.) |
| User \\ Address                     | street3                     | string   | The third row that was provided for the address. (This value can be blank.) |
| User \\ Address                     | city                        | string   | The city that was provided for the address. |
| User \\ Address                     | state                       | string   | The state or province that was provided for the address. |
| User \\ Address                     | district                    | string   | The district that was provided for the address. |
| User \\ Address                     | zipCode                     | string   | The postal code that was provided for the address. |
| User \\ Address                     | country                     | string   | The country/region code that was provided for the address. The value should be a two-letter ISO country/region code (for example, **US**). |
| PaymentInstrument                   | merchantPaymentInstrumentId | string   | The identifier of the payment instrument. This information is provided by the merchant. |
| PaymentInstrument                   | type                        | string   | The type of payment. Possible values are **'CreditCard'**, **'DirectDebit'**, **'PayPal'**, **'MobileBilling'**, **'OnlineBankTransfer'**, **'Invoice'**, **'MerchantGiftCard'**, **'MerchantWallet'**, **'CashOnDelivery'**, **'Paytm'**, and **'CCAvenue'**. |
| PaymentInstrument                   | creationDate                | DateTime | The date of the first entry for the payment instrument in the merchant's system. The format is ISO 8601. |
| PaymentInstrument                   | updateDate                  | DateTime | The date of the last update for the payment instrument in the merchant's system. The format is ISO 8601. |
| PaymentInstrument                   | state                       | string   | The current state of the payment instrument in the merchant's system (for example, **Active**, **Blocked**, or **Expired**). |
| PaymentInstrument                   | cardType                    | string   | This attribute is used only for payments of the **Credit/Debit Card** type. Possible values are **'Visa'**, **'Mastercard'**, **'Amex'**, **'ACH'**, **'SEPA'**, **'UnionPay'**, **'Inicis'**, **'MobileBillingCarrier'**, **'Discover'**, **'AllPay'**, **'JCB'**, and **'DiscoverDiners'**. |
| PaymentInstrument                   | holderName                  | string   | The name of the payment instrument's user. This attribute is used only for payments of the **Credit/Debit Card** type. |
| PaymentInstrument                   | bin                         | string   | This attribute is used only for payments of the **Credit/Debit Card** type. |
| PaymentInstrument                   | expirationDate              | string   | The expiration date for the payment instrument in the merchant's system. The format is ISO 8601. This attribute is used only for payments of the **Credit/Debit Card** type. |
| PaymentInstrument                   | lastFourDigits              | string   | This attribute is used only for payments of the **Credit/Debit Card** type. |
| PaymentInstrument                   | email                       | string   | The email address that is associated with the payment instrument. This attribute is used only for payments of the **PayPal** type. |
| PaymentInstrument                   | billingAgreementId          | string   | This attribute is used only for payments of the **PayPal** type. |
| PaymentInstrument                   | payerId                     | string   | This attribute is used only for payments of the **PayPal** type. |
| PaymentInstrument                   | payerStatus                 | string   | A value that indicates whether PayPal has verified the payer. This attribute is used only for payments of the **PayPal** type. |
| PaymentInstrument                   | addressStatus               | string   | A value that indicates whether PayPal has verified the payer's address. This attribute is used only for payments of the **PayPal** type. |
| PaymentInstrument                   | imei                        | string   | This attribute is used only for payments of the **Mobilepayment** type. |
| PaymentInstrument \\ BillingAddress | addressType                 | enum     | The type of address. Possible values are **'Primary'**, **'Billing'**, **'Shipping'**, and **'Alternative'**. The default value is **'Billing'**. |
| PaymentInstrument \\ BillingAddress | firstName                   | string   | The user-provided first name that is associated with the address. |
| PaymentInstrument \\ BillingAddress | lastName                    | string   | The user-provided last name that is associated with the address. |
| PaymentInstrument \\ BillingAddress | phoneNumber                 | string   | The user-provided phone number that is associated with the address. |
| PaymentInstrument \\ BillingAddress | street1                     | string   | The first row that was provided for the address. |
| PaymentInstrument \\ BillingAddress | street2                     | string   | The second row that was provided for the address. (This value can be blank.) |
| PaymentInstrument \\ BillingAddress | street3                     | string   | The third row that was provided for the address. (This value can be blank.) |
| PaymentInstrument \\ BillingAddress | city                        | string   | The city that was provided for the address. |
| PaymentInstrument \\ BillingAddress | state                       | string   | The state or province that was provided for the address. |
| PaymentInstrument \\ BillingAddress | district                    | string   | The district that was provided for the address |
| PaymentInstrument \\ BillingAddress | zipCode                     | string   | The postal code that was provided for the address. |
| PaymentInstrument \\ BillingAddress | country                     | string   | The country/region code that was provided for the address. The value should be a two-letter ISO country/region code (for example, **US**). |
| MarketingContext                    | campaignType                | string   | The type of marketing campaign. Possible values are **'None'**, **'Email'**, **'Referral'**, **'SearchEngine'**, **'Direct'**, **'SocialNetwork'**, and **'Other'**. |
| MarketingContext                    | trafficSource               | string   | The source of this user, if it's known. If the user came via a referral, provide the **MerchantUserId** value of the referrer. |
| MarketingContext                    | incentiveType               | string   | The incentive type for the new user. Possible values are **'None'**, **'CashBack'**, **'Discount'**, **'FreeTrial'**, **'BonusPoints'**, **'Gift'**, and **'Other'**. |
| MarketingContext                    | incentiveOffer              | string   | The exact name of the incentive offer (for example, **$5 off on first order**, **free shipping**, or **5,000 points**). |

## AccountCreationStatus

The **AccountCreationStatus** API lets you share information and context with Fraud Protection about the status of an account creation event. This event is a data ingestion event only.

| Object   | Attribute         | Type     | Description |
|----------|-------------------|----------|-------------|
|          | Name              | string   | The value is **"AP.AccountCreation.Status"**. |
|          | Version           | string   | The value is **"0.5"**. |
| MetaData | trackingID        | string   | The identifier of the **SignupStatus** event. |
| MetaData | signupId          | string   | The identifier of the **Signup** event. |
| MetaData | merchantTimeStamp | DateTime | The time stamp for the event. |
| MetaData | userId            | string   | The user identifier. This information is provided by the merchant. |
| Status   | statusType        | string   | The type of status: **Approved**, **Rejected**, or **Pending**. |
| Status   | reasonType        | enum     | The type of reason: **challenge abandoned**, **challenge failed**, **challenge passed**, **challenge pending**, **review failed**, **review passed**, **review pending**, or **None**. The default value is **None**. |
| Status   | challengeType     | enum     | The type of review status: **SMS**, **Email**, **Phone**, **Other**, or **None**. The default value is **None**. |
| Status   | statusDate        | DateTime | The date and time when the status was applied. The format is ISO 8601. |

## AccountLogIn

The **AccountLogIn** API lets you share information and context with Fraud Protection about an incoming sign-in event for risk assessment.

| Object                            | Attribute                   | Type     | Description |
|-----------------------------------|-----------------------------|----------|-------------|
|                                   | Name                        | string   | The value is **"AP.AccountLogin"**. |
|                                   | Version                     | string   | The value is **"0.5"**. |
| MetaData                          | trackingId                  | string   | The identifier of the **Signup** event. |
| MetaData                          | LogInId                     | string   | The identifier of the **Signup** event (This value can match the value of the **trackingId** attribute.) |
| MetaData                          | assessmentType              | string   | The assessment type for the event. Possible values are **'evaluate'** and **'protect'**. If no value is specified, the default value is **'protect'**. |
| MetaData                          | customerLocalDate           | dateTime | The creation date of the **Signup** event, in the customer's local time zone. The format is ISO 8601. |
| MetaData                          | merchantTimeStamp           | dateTime | The time stamp for the event. |
| DeviceContext                     | SessionID                   | string   | The customer's session ID. This information is mastered by DFP Device Fingerprinting Service. |
| DeviceContext                     | ipAddress                   | string   | The customer's IP address, as provided by the merchant. |
| DeviceContext                     | provider                    | string   | The provider of device information. Possible values are **'DFPFingerprinting'** and **'Merchant'**. If no value is specified, the default value is **'DFPFingerprinting'**. |
| DeviceContext                     | externalDeviceId            | string   | The customer's device ID, as provided and mastered by the merchant. |
| DeviceContext                     | externalDeviceType          | string   | The customer's device type, as provided and mastered by the merchant. |
| User                              | userId                      | string   | The user identifier. This information is provided by the merchant. |
| User                              | userType                    | string   | The user's profile type. Possible values are **'Consumer'**, **'Developer'**, **'Seller'**, **'Publisher'**, and **'Tenant'**. |
| User                              | UserName                    | string   | The user-provided user name that is unique in the merchant system. |
| User                              | passwordHash                | string   | The user-provided password that is hashed in the merchant system. |
| User \\ SSOAuthenticationProvider | authenticationProvider      | string   | The user's SSO authentication provider, if it differs from the merchant's SSO authentication provider. Possible values are **'MSA'**, **'Facebook'**, **'PSN'**, **'MerchantAuth'**, and **'Google'**. |
| User \\ SSOAuthenticationProvider | displayName                 | string   | The user's display name for the SSO authentication provider (for example, the user name from a Microsoft account, Facebook, or Google). |
| User \\ RecentUpdate              | lastPhoneNumberUpdate       | dateTime | The date/time of the most recent update or creation of any phone number. |
| User \\ RecentUpdate              | lastEmailUpdate             | dateTime | The date/time of the most recent update or creation of any email address. |
| User \\ RecentUpdate              | lastAddressUpdate           | dateTime | The date/time of the most recent update or creation of any address. |
| User \\ RecentUpdate              | lastPaymentInstrumentUpdate | dateTime | The date/time of the most recent update or creation any payment instrument. |

## AccountLogInStatus

The **AccountLogInStatus** API lets you share information and context with Fraud Protection about the status of an account sign-in event. This event is a data ingestion event only.

| Object   | Attribute         | Type     | Description |
|----------|-------------------|----------|-------------|
|          | Name              | string   | The value is **"AP.AccountLogin.Status"**. |
|          | Version           | string   | The value is **"0.5"**. |
| MetaData | trackingID        | string   | The identifier of the **SignupStatus** event. |
| MetaData | logInId           | string   | The identifier of the **Signup** event. |
| MetaData | merchantTimeStamp | DateTime | The time stamp for the event. |
| MetaData | userId            | string   | The user identifier. This information is provided by the merchant. |
| Status   | statusType        | string   | The type of status: **Approved**, **Rejected**, or **Pending**. |
| Status   | reasonType        | enum     | The type of reason: **challenge abandoned**, **challenge failed**, **challenge passed**, **challenge pending**, **review failed**, **review passed**, **review pending**, or **None**. The default value is **None**. |
| Status   | challengeType     | enum     | The type of review status: **SMS**, **Email**, **Phone**, **Other**, or **None**. The default value is **None**. |
| Status   | statusDate        | DateTime | The date and time when the status was applied. The format is ISO 8601. |

## AccountUpdate

The **AccountUpdate** API lets you share account information updates with Fraud Protection. For example, the following information might be edited or added: user profile, address, payment instrument, phone number, email address, and SSO. This event is a data ingestion event only.

| Object                              | Attribute                   | Type     | Description |
|-------------------------------------|-----------------------------|----------|---------------------------|
|                                     | Name                        | string   | The value is **"AP.AccountUpdate"**. |
|                                     | Version                     | string   | The value is **"0.5"**. |
| MetaData                            | trackingId                  | string   | The identifier of the **Signup** event. |
| MetaData                            | signUpId                    | string   | The identifier of the **Signup** event (This value can match the value of the **trackingId** attribute.). |
| MetaData                            | customerLocalDate           | dateTime | The creation date of the **Signup** event, in the customer's local time zone. The format is ISO 8601. |
| MetaData                            | merchantTimeStamp           | dateTime | The time stamp for the event. |
| DeviceContext                       | SessionID                   | string   | The customer's session ID. This information is mastered by DFP Device Fingerprinting Service. |
| DeviceContext                       | ipAddress                   | string   | The customer's IP address, as provided by the merchant. |
| DeviceContext                       | provider                    | string   | The provider of device information. Possible values are **'DFPFingerprinting'** and **'Merchant'**. If no value is specified, the default value is **'DFPFingerprinting'**. |
| DeviceContext                       | externalDeviceId            | string   | The customer's device ID, as provided and mastered by the merchant. |
| DeviceContext                       | externalDeviceType          | string   | The customer's device type, as provided and mastered by the merchant. Possible values are **'Mobile'**, **'Computer'**, **'MerchantHardware'**, **'Tablet'**, and **'GameConsole'**. |
| User                                | userId                      | string   | The user identifier. This information is provided by the merchant. |
| User                                | userType                    | string   | The user's profile type. Possible values are **'Consumer'**, **'Developer'**, **'Seller'**, **'Publisher'**, and **'Tenant'**. |
| User                                | UserName                    | string   | The user-provided user name that is unique in the merchant system. |
| User                                | passwordHash                | string   | The user-provided password that is hashed in the merchant system. |
| User                                | firstName                   | string   | The user-provided first name on the account. |
| User                                | lastName                    | string   | The user-provided last name on the account. |
| User                                | country                     | string   | The user's country or region. The value should be a two-letter ISO country/region code (for example, **US**). |
| User                                | zipCode                     | string   | The user's postal code. |
| User                                | timeZone                    | string   | The user's time zone. |
| User                                | language                    | string   | The user's language and territory (for example, **EN-US**). |
| User                                | membershipId                | string   | The membership ID, if the user already has an existing membership with the merchant. |
| User                                | isMembershipIdUserName      | bool     | A **True**/**False** value that indicates whether the **membershipId** value can be used as the user name. The default value is **False**. |
| User \\ phone                       | phoneType                   | enum     | The type of phone number. Possible values are **'Primary'** and **'Alternative'**. The default value is **'Primary'**. |
| User \\ phone                       | phoneNumber                 | string   | The user's phone number. The format should be the country/region code followed by a hyphen (\-) and then the phone number (for example, for the US, **+1-1234567890**). |
| User \\ phone                       | isPhoneNumberValidated      | bool     | A **True**/**False** value that indicates whether the user-provided phone number has been verified as owned by the user. |
| User \\ phone                       | phoneNumberValidatedDate    | dateTime | The validation date of the user's phone number. The format is ISO 8601. |
| User \\ phone                       | isPhoneUserName             | bool     | A **True**/**False** value that indicates whether the phone number can be used as the user name. The default value is **False**. |
| User \\ Email                       | emailType                   | enum     | The type of email address. Possible values are **'Primary'** and **'Alternative'**. |
| User \\ Email                       | email                       | string   | The user's email address. This value is case-insensitive. |
| User \\ Email                       | isEmailValidated            | bool     | A **True**/**False** value that indicates whether the user-provided email address has been verified as owned by the user. |
| User \\ Email                       | emailValidatedDate          | dateTime | The validation date of the user's email address. The format is ISO 8601. |
| User \\ Email                       | isEmailUserName             | bool     | A **True**/**False** value that indicates whether the email address can be used as the user name. The default value is **False**. |
| User \\ SSOAuthenticationProvider   | authenticationProvider      | string   | The user's SSO authentication provider, if it differs from the merchant's SSO authentication provider. Possible values are **'MSA'**, **'Facebook'**, **'PSN'**, **'MerchantAuth'**, and **'Google'**. |
| User \\ SSOAuthenticationProvider   | displayName                 | string   | The user's display name for the SSO authentication provider (for example, the user name from a Microsoft account, Facebook, or Google). |
| User \\ Address                     | addressType                 | enum     | The type of address. Possible values are **'Primary'**, **'Billing'**, **'Shipping'**, and **'Alternative'**. The default value is **'Primary'**. |
| User \\ Address                     | firstName                   | string   | The user-provided first name that is associated with the address. |
| User \\ Address                     | lastName                    | string   | The user-provided last name that is associated with the address. |
| User \\ Address                     | phoneNumber                 | string   | The user-provided phone number that is associated with the address. |
| User \\ Address                     | street1                     | string   | The first row that was provided for the address. |
| User \\ Address                     | street2                     | string   | The second row that was provided for the address. (This value can be blank.) |
| User \\ Address                     | street3                     | string   | The third row that was provided for the address. (This value can be blank.) |
| User \\ Address                     | city                        | string   | The city that was provided for the address. |
| User \\ Address                     | state                       | string   | The state or province that was provided for the address. |
| User \\ Address                     | district                    | string   | The district that was provided for the address. |
| User \\ Address                     | zipCode                     | string   | The postal code that was provided for the address. |
| User \\ Address                     | country                     | string   | The country/region code that was provided for the address. The value should be a two-letter ISO country/region code (for example, **US**). |
| PaymentInstrument                   | merchantPaymentInstrumentId | string   | The identifier of the payment instrument. This information is provided by the merchant. |
| PaymentInstrument                   | type                        | string   | The type of payment. Possible values are **'CreditCard'**, **'DirectDebit'**, **'PayPal'**, **'MobileBilling'**, **'OnlineBankTransfer'**, **'Invoice'**, **'MerchantGiftCard'**, **'MerchantWallet'**, **'CashOnDelivery'**, **'Paytm'**, and **'CCAvenue'**. |
| PaymentInstrument                   | creationDate                | DateTime | The date of the first entry for the payment instrument in the merchant's system. The format is ISO 8601. |
| PaymentInstrument                   | updateDate                  | DateTime | The date of the last update for the payment instrument in the merchant's system. The format is ISO 8601. |
| PaymentInstrument                   | state                       | string   | The current state of the payment instrument in the merchant's system (for example, **Active**, **Blocked**, or **Expired**). |
| PaymentInstrument                   | cardType                    | string   | This attribute is used only for payments of the **Credit/Debit Card** type. Possible values are **'Visa'**, **'Mastercard'**, **'Amex'**, **'ACH'**, **'SEPA'**, **'UnionPay'**, **'Inicis'**, **'MobileBillingCarrier'**, **'Discover'**, **'AllPay'**, **'JCB'**, and **'DiscoverDiners'**. |
| PaymentInstrument                   | holderName                  | string   | The name of the payment instrument's user. This attribute is used only for payments of the **Credit/Debit Card** type. |
| PaymentInstrument                   | bin                         | string   | This attribute is used only for payments of the **Credit/Debit Card** type. |
| PaymentInstrument                   | expirationDate              | string   | The expiration date for the payment instrument in the merchant's system. The format is ISO 8601. This attribute is used only for payments of the **Credit/Debit Card** type. |
| PaymentInstrument                   | lastFourDigits              | string   | This attribute is used only for payments of the **Credit/Debit Card** type. |
| PaymentInstrument                   | email                       | string   | The email address that is associated with the payment instrument. This attribute is used only for payments of the **PayPal** type. |
| PaymentInstrument                   | billingAgreementId          | string   | This attribute is used only for payments of the **PayPal** type. |
| PaymentInstrument                   | payerId                     | string   | This attribute is used only for payments of the **PayPal** type. |
| PaymentInstrument                   | payerStatus                 | string   | A value that indicates whether PayPal has verified the payer. This attribute is used only for payments of the **PayPal** type. |
| PaymentInstrument                   | addressStatus               | string   | A value that indicates whether PayPal has verified the payer's address. This attribute is used only for payments of the **PayPal** type. |
| PaymentInstrument                   | imei                        | string   | This attribute is used only for payments of the **Mobilepayment** type. |
| PaymentInstrument \\ BillingAddress | addressType                 | enum     | The type of address. Possible values are **'Primary'**, **'Billing'**, **'Shipping'**, and **'Alternative'**. The default value is **'Billing'**. |
| PaymentInstrument \\ BillingAddress | firstName                   | string   | The user-provided first name that is associated with the address. |
| PaymentInstrument \\ BillingAddress | lastName                    | string   | The user-provided last name that is associated with the address. |
| PaymentInstrument \\ BillingAddress | phoneNumber                 | string   | The user-provided phone number that is associated with the address. |
| PaymentInstrument \\ BillingAddress | street1                     | string   | The first row that was provided for the address. |
| PaymentInstrument \\ BillingAddress | street2                     | string   | The second row that was provided for the address. (This value can be blank.) |
| PaymentInstrument \\ BillingAddress | street3                     | string   | The third row that was provided for the address. (This value can be blank.) |
| PaymentInstrument \\ BillingAddress | city                        | string   | The city that was provided for the address. |
| PaymentInstrument \\ BillingAddress | state                       | string   | The state or province that was provided for the address.|
| PaymentInstrument \\ BillingAddress | district                    | string   | The district that was provided for the address. |
| PaymentInstrument \\ BillingAddress | zipCode                     | string   | The postal code that was provided for the address. |
| PaymentInstrument \\ BillingAddress | country                     | string   | The country/region code that was provided for the address. The value should be a two-letter ISO country/region code (for example, **US**). |

## Labels

The **Labels** API lets you share additional information about the outcomes of transactions and events for model training that is based on an additional set of fraud signals. This information includes information that you receive from banks. This event is a data ingestion event only.

| Category | Attribute          | Type     | Description |
|----------|--------------------|----------|-------------|
|          | Name               | string   | The value is **"AP.AccountLabel"**. |
|          | Version            | string   | The value is **"0.5"**. |
| MetaData | TrackingId         | String   | The unique ID for each event/record. |
| MetaData | merchantTimeStamp  | DateTime | The date, in the merchant's time zone. The format is ISO 8601. |
| MetaData | userId             | string   | The user identifier. This information is provided by the merchant. |
| Label    | EventTimeStamp     | DateTime | The date and time of the event. Possible values are the chargeback date and the review date. The format is ISO 8601. |
| Label    | LabelObjectType    | String   | The type of label: **Purchase**, **Account Creation**, **Account Login**, **Account Update**, **Custom Fraud Evaluation**, **Account**, **Payment instrument**, or **Email**. |
| Label    | LabelObjectId      | String   | The identifier field for the object: **PurchaseId**, **AccountCreationId**, **AccountLoginId**, **AccountUpdateId**, **UserId**, **MerchantPaymentInstrumentId**, or **Email**. |
| Label    | LabelSource        | String   | The source of the label: **Customer Escalation**, **Chargeback**, **TC40\_SAFE**, **Manual Review**, **Refund**, **Offline Analysis**, or **Account Protection Review**. |
| Label    | LabelState         | String   | The current status of the label: **Inquiry Accepted**, **Fraud**, **Disputed**, **Reversed**, **Abuse**, **Resubmitted Request**, **AccountCompromised**, or **AccountNotCompromised**. |
| Label    | LabelReasonCodes   | String   | The reason codes that are associated with each type of label: **Processor/Bank Response Code**, **Fraud Refund**, **Account TakeOver**, **Payment Instrument Fraud**, **Account Fraud**, **Abuse**, **Friendly Fraud**, **Account Credentials Leaked**, or **Passed Account Protection Checks**. |
| Label    | Processor          | String   | The name of the bank or payment processor that generates the TC40 or System to Avoid Fraud Effectively (SAFE) information. |
| Label    | EffectiveStartDate | DateTime | The date when this label becomes effective. The format is ISO 8601. |
| Label    | EffectiveEndDate   | DateTime | The end date for this label. The format is ISO 8601. |
