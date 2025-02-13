---
author: yvonnedeq
description: This article outlines the account protection schemas for data uploaded in bulk as CSV files.
ms.author: josaw 
ms.date: 04/10/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Account protection schemas
---

# Account protection schemas

[!include[deprecation](includes/deprecation.md)]

This article outlines the schema via the application programming interface (API). For more information, see [Integrate Dynamics 365 Fraud Protection real-time APIs](/dynamics365/fraud-protection/integrate-real-time-api).


## AccountCreation

The **AccountCreation** API lets you share information and context with Microsoft Dynamics 365 Fraud Protection about incoming new account creation events for risk assessment.

| Object                              | Attribute                   | Type     | Description |
|-------------------------------------|-----------------------------|----------|-------------|
|                                     | Tenant ID                   | string   | TenantId is the GUID representing the Azure ActiveDirectory Tenant.  |
|                                     | Name                        | string   | The value is **AP.AccountCreation**. |
|                                     | Version                     | string   | The value is **0.5**. |
| MetaData                            | trackingId                  | string   | The identifier of the **AccountCreationId** event. |
| MetaData                            | SignupId                    | string   | The identifier of the **AccountCreationId** event. (This value can match the value of the **trackingId** attribute but is different from the **userId** attribute.) |
| MetaData                            | assessmentType              | string   | The assessment type for the event. Possible values are **evaluate** and **protect**. If no value is specified, the default value is **protect**. |
| MetaData                            | customerLocalDate           | dateTime | The creation date of the **AccountCreationId** event, in the customer's local time zone. The format is ISO 8601. |
| MetaData                            | merchantTimeStamp           | dateTime | The time stamp for the event. |
| DeviceContext                       | DeviceContextId             | string   | The customer's session ID. This information is mastered by DFP Device Fingerprinting Service. |
| DeviceContext                       | ipAddress                   | string   | The customer's IP address, as provided by the merchant. |
| DeviceContext                       | provider                    | string   | The provider of device information. Possible values are **DFPFingerprinting** and **Merchant**. If no value is specified, the default value is **DFPFingerprinting**. |
| DeviceContext                       | externalDeviceId            | string   | The customer's device ID, as provided and mastered by the merchant. |
| DeviceContext                       | externalDeviceType          | string   | The customer's device type, as provided and mastered by the merchant. Possible values are **Mobile**, **Computer**, **MerchantHardware**, **Tablet**, and **GameConsole**. |
| User                                | userId                      | string   | The user identifier. This information is provided by the merchant. |
| User                                | userType                    | string   | The user's profile type. Possible values are **Consumer**, **Developer**, **Seller**, **Publisher**, and **Tenant**. |
| User                                | UserName                    | string   | The user-provided user name that is unique in the merchant system. |
| User                                | firstName                   | string   | The user-provided first name on the account. |
| User                                | lastName                    | string   | The user-provided last name on the account. |
| User                                | CountryRegion               | string   | The user's country or region. The value should be a two-letter ISO country/region code (for example, **US**). |
| User                                | zipCode                     | string   | The user's postal code. |
| User                                | timeZone                    | string   | The user's time zone. |
| User                                | language                    | string   | The user's language and territory (for example, **EN-US**). |
| User                                | membershipId                | string   | The membership ID, if the user already has an existing membership with the merchant. |
| User                                | isMembershipIdUserName      | bool     | A **True**/**False** value that indicates whether the **membershipId** value can be used as the user name. The default value is **False**. |
| Phone                       | phoneType                   | enum     | The type of phone number. Possible values are **Primary** and **Alternative**. The default value is **Primary**. |
| Phone                       | phoneNumber                 | string   | The user's phone number. The format should be the country/region code followed by a hyphen (\-) and then the phone number (for example, for the US, **+1-1234567890**). |
| Phone                       | isPhoneNumberValidated      | bool     | A **True**/**False** value that indicates whether the user-provided phone number has been verified as owned by the user. |
| Phone                       | phoneNumberValidatedDate    | dateTime | The validation date of the user's phone number. The format is ISO 8601. |
| Phone                       | isPhoneUserName             | bool     | A **True**/**False** value that indicates whether the phone number can be used as the user name. The default value is **False**. |
| Email                       | emailType                   | enum     | The type of email address. Possible values are **Primary** and **Alternative**. |
| Email                       | emailValue                       | string   | The user's email address. This value is case-insensitive. |
| Email                       | isEmailValidated            | bool     | A **True**/**False** value that indicates whether the user-provided email address has been verified as owned by the user. |
| Email                       | emailValidatedDate          | dateTime | The validation date of the user's email address. The format is ISO 8601. |
| Email                       | isEmailUserName             | bool     | A **True**/**False** value that indicates whether the email address can be used as the user name. The default value is **False**. |
| SSOAuthenticationProvider   | authenticationProvider      | string   | The user's single sign-on (SSO) authentication provider, if it differs from the merchant's SSO authentication provider. Possible values are **MSA**, **Facebook**, **PSN**, **MerchantAuth**, and **Google**. |
| SSOAuthenticationProvider   | displayName                 | string   | The user's display name for the SSO authentication provider (for example, the user name from a Microsoft account, Facebook, or Google). |
| Address                     | addressType                 | enum     | The type of address. Possible values are **Primary**, **Billing**, **Shipping**, and **Alternative**. The default value is **Primary**. |
| Address                     | firstName                   | string   | The user-provided first name that is associated with the address. |
| Address                     | lastName                    | string   | The user-provided last name that is associated with the address. |
| Address                     | phoneNumber                 | string   | The user-provided phone number that is associated with the address. |
| Address                     | street1                     | string   | The first row that was provided for the address. |
| Address                     | street2                     | string   | The second row that was provided for the address. (This value can be blank.) |
| Address                     | street3                     | string   | The third row that was provided for the address. (This value can be blank.) |
| Address                     | city                        | string   | The city that was provided for the address. |
| Address                     | state                       | string   | The state or province that was provided for the address. |
| Address                     | district                    | string   | The district that was provided for the address. |
| Address                     | zipCode                     | string   | The postal code that was provided for the address. |
| Address                     | CountryRegion                     | string   | The country/region code that was provided for the address. The value should be a two-letter ISO country/region code (for example, **US**). |
| PaymentInstrument                   | merchantPaymentInstrumentId | string   | The identifier of the payment instrument. This information is provided by the merchant. |
| PaymentInstrument                   | type                        | enum     | The type of payment. Possible values are **CreditCard**, **DirectDebit**, **PayPal**, **MobileBilling**, **OnlineBankTransfer**, **Invoice**, **MerchantGiftCard**, **MerchantWallet**, **CashOnDelivery**, **Paytm**, and **CCAvenue**. |
| PaymentInstrument                   | creationDate                | DateTime | The date of the first entry for the payment instrument in the merchant's system. The format is ISO 8601. |
| PaymentInstrument                   | updateDate                  | DateTime | The date of the last update for the payment instrument in the merchant's system. The format is ISO 8601. |
| PaymentInstrument                   | state                       | string   | The current state of the payment instrument in the merchant's system (for example, **Active**, **Blocked**, or **Expired**). |
| PaymentInstrument                   | cardType                    | string   | This attribute is used only for payments of the **CreditCard** or **DirectDebit** types. Possible values are **Visa**, **Mastercard**, **Amex**, **ACH**, **SEPA**, **UnionPay**, **Inicis**, **MobileBillingCarrier**, **Discover**, **AllPay**, **JCB**, and **DiscoverDiners**. |
| PaymentInstrument                   | holderName                  | string   | The name of the payment instrument's user. This attribute is used only for payments of the **CreditCard** or **DirectDebit** types. |
| PaymentInstrument                   | bin                         | string   | This attribute is used only for payments of the **CreditCard** or **DirectDebit** types. |
| PaymentInstrument                   | expirationDate              | string   | The expiration date for the payment instrument in the merchant's system. The format is ISO 8601. This attribute is used only for payments of the **CreditCard** or **DirectDebit** types. |
| PaymentInstrument                   | lastFourDigits              | string   | This attribute is used only for payments of the **CreditCard** or **DirectDebit** types. |
| PaymentInstrument                   | email                       | string   | The email address that is associated with the payment instrument. This attribute is used only for payments of the **PayPal** type. |
| PaymentInstrument                   | billingAgreementId          | string   | This attribute is used only for payments of the **PayPal** type. |
| PaymentInstrument                   | payerId                     | string   | This attribute is used only for payments of the **PayPal** type. |
| PaymentInstrument                   | payerStatus                 | string   | A value that indicates whether PayPal has verified the payer. This attribute is used only for payments of the **PayPal** type. |
| PaymentInstrument                   | addressStatus               | string   | A value that indicates whether PayPal has verified the payer's address. This attribute is used only for payments of the **PayPal** type. |
| PaymentInstrument                   | imei                        | string   | This attribute is used only for payments of the **MobileBilling** type. |
| PaymentInstrument \\ BillingAddress | addressType                 | enum     | The type of address. Possible values are **Primary**, **Billing**, **Shipping**, and **Alternative**. The default value is **Billing**. |
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
| PaymentInstrument \\ BillingAddress | CountryRegion                     | string   | The country/region code that was provided for the address. The value should be a two-letter ISO country/region code (for example, **US**). |
| MarketingContext                    | campaignType                | enum     | The marketing campaign type. Possible values are **Direct**, **Email**, **Referral**, **PaidSearch**, **OrganicSearch**, **Advertising**, **SocialNetwork**, **General Marketing**, **Unknown**, **Other**. |
| MarketingContext                    | trafficSource-referrer      | string   | The source of this user if known. If via existing user referral, provide the original MerchantUserId of the referrer.                            |
| MarketingContext                    | trafficSource-referralLink | string   | The source of this user if known. If via other campaign types instead of existing user referral, provide the source URL link.                    |
| MarketingContext                    | trafficSource-referralSite | string   | The source site of the traffic. Possible values are **Facebook**, **Instagram**, **Twitter**, **Bing**, **Google**, **Pinterest**, **WhatsApp**, etc.          |
| MarketingContext                    | IncentiveType            | enum     | The incentive type for the new user. Possible values are **None**, **CashBack**, **Discount**, **FreeTrial**, **BonusPoints**, **Gift**, **Unknown**, **Other**. |
| MarketingContext                    | incentiveOffer              | string   | The exact incentive offer name. For examples, $5 off on first order, free shipping, 5000 points. |
| MarketingContext                    | CampaignStartDate           | date     | The date of the campaign starting on the incentive collection.                                   |
| MarketingContext                    | CampaignExpireDate          | date     | The date of the campaign expiration on the incentive collection.                                 |
| MarketingContext                    | IncentiveQuantityLimit      | string   | The incentive quantity limit set by merchant. For example, max on three 5000 points per user per day.    |


## AccountCreationStatus

The **AccountCreationStatus** API lets you share information and context with Fraud Protection about the status of an account creation event. This event is a data ingestion event only.

| Object   | Attribute         | Type     | Description |
|----------|-------------------|----------|-------------|
|          | Tenant ID         | string   | TenantId is the GUID representing the Azure ActiveDirectory Tenant. |
|          | Name              | string   | The value is **AP.AccountCreation.Status**. |
|          | Version           | string   | The value is **0.5**. |
| MetaData | trackingID        | string   | The identifier of the **SignupStatus** event. |
| MetaData | signupId          | string   | The identifier of the **Signup** event. |
| MetaData | merchantTimeStamp | DateTime | The time stamp for the event. |
| MetaData | userId            | string   | The user identifier. This information is provided by the merchant. |
| StatusDetails   | statusType        | enum   | The type of status: **Approved**, **Rejected**, or **Pending**. |
| StatusDetails   | reasonType        | enum     | The type of reason: **challenge abandoned**, **challenge failed**, **challenge passed**, **challenge pending**, **review failed**, **review passed**, **review pending**, or **None**. The default value is **None**. |
| StatusDetails   | challengeType     | enum     | The type of review status: **SMS**, **Email**, **Phone**, **Other**, or **None**. The default value is **None**. |
| StatusDetails   | statusDate        | DateTime | The date and time when the status was applied. The format is ISO 8601. |


## AccountLogIn

The **AccountLogIn** API lets you share information and context with Fraud Protection about an incoming sign-in event for risk assessment.

| Object                            | Attribute                   | Type     | Description |
|-----------------------------------|-----------------------------|----------|-------------|
|                                   | Name                        | string   | The value is **AP.AccountLogin**. |
|                                   | Version                     | string   | The value is **0.5**. |
| MetaData                          | trackingId                  | string   | The identifier of the **Login** event. |
| MetaData                          | LogInId                     | string   | The identifier of the **Signup** event. (This value can match the value of the **trackingId** attribute.) |
| MetaData                          | assessmentType              | string   | The assessment type for the event. Possible values are **evaluate** and **protect**. If no value is specified, the default value is **protect**. |
| MetaData                          | customerLocalDate           | dateTime | The creation date of the **Signup** event, in the customer's local time zone. The format is ISO 8601. |
| MetaData                          | merchantTimeStamp           | dateTime | The time stamp for the event. |
| DeviceContext                     | DeviceContextId                   | string   | The customer's session ID. This information is mastered by DFP Device Fingerprinting Service. |
| DeviceContext                     | ipAddress                   | string   | The customer's IP address, as provided by the merchant. |
| DeviceContext                     | provider                    | string   | The provider of device information. Possible values are **DFPFingerprinting** and **Merchant**. If no value is specified, the default value is **DFPFingerprinting**. |
| DeviceContext                     | externalDeviceId            | string   | The customer's device ID, as provided and mastered by the merchant. |
| DeviceContext                     | externalDeviceType          | string   | The customer's device type, as provided and mastered by the merchant. |
| User                              | userId                      | string   | The user identifier. This information is provided by the merchant. |
| User                              | userType                    | string   | The user's profile type. Possible values are **Consumer**, **Developer**, **Seller**, **Publisher**, and **Tenant**. |
| User                              | UserName                    | string   | The user-provided user name that is unique in the merchant system. |
| SSOAuthenticationProvider | authenticationProvider      | string   | The user's SSO authentication provider, if it differs from the merchant's SSO authentication provider. Possible values are **MSA**, **Facebook**, **PSN**, **MerchantAuth**, and **Google**. |
| SSOAuthenticationProvider | displayName                 | string   | The user's display name for the SSO authentication provider. For example, the user name from a Microsoft account, Facebook, or Google. |
| RecentUpdate              | lastPhoneNumberUpdate       | dateTime | The date/time of the most recent update or creation of any phone number. |
| RecentUpdate              | lastEmailUpdate             | dateTime | The date/time of the most recent update or creation of any email address. |
| RecentUpdate              | lastAddressUpdate           | dateTime | The date/time of the most recent update or creation of any address. |
| RecentUpdate              | lastPaymentInstrumentUpdate | dateTime | The date/time of the most recent update or creation of any payment instrument. |
| MarketingContext                    | campaignType                | enum     | The marketing campaign type. Possible values are **Direct**, **Email**, **Referral**, **PaidSearch**, **OrganicSearch**, **Advertising**, **SocialNetwork**, **General Marketing**, **Unknown**, **Other**. |
| MarketingContext                    | trafficSource-referrer      | string   | The source of this user if known. If via existing user referral, provide the original MerchantUserId of the referrer.      |
| MarketingContext                    | trafficSource-referralLink | string   | The source of this user if known. If via other campaign types instead of existing user referral, provide the source URL link.          |
| MarketingContext                    | trafficSource-referralSite | string   | The source site of the traffic. Possible values are **Facebook**, **Instagram**, **Twitter**, **Bing**, **Google**, **Pinterest**, **WhatsApp**, etc.          |
| MarketingContext                    | IncentiveType               | enum     | The incentive type for the new user. Possible values are **None**, **CashBack**, **Discount**, **FreeTrial**, **BonusPoints**, **Gift**, **Unknown**, **Other**. |
| MarketingContext                    | incentiveOffer              | string   | The exact incentive offer name. For examples, $5 off on first order, free shipping, 5000 points. |
| MarketingContext                    | CampaignStartDate           | date     | The date of the campaign starting on the incentive collection.     |
| MarketingContext                    | CampaignExpireDate          | date     | The date of the campaign expiration on the incentive collection.     |
| MarketingContext                    | IncentiveQuantityLimit      | string   | The incentive quantity limit set by merchant. For example, max on three 5000 points per user per day.    |


## AccountLogInStatus

The **AccountLogInStatus** API lets you share information and context with Fraud Protection about the status of an account sign-in event. This event is a data ingestion event only.

| Object   | Attribute         | Type     | Description |
|----------|-------------------|----------|-------------|
|          | Name              | string   | The value is **AP.AccountLogin.Status**. |
|          | Version           | string   | The value is **0.5**. |
| MetaData | trackingID        | string   | The identifier of the **LoginStatus** event. |
| MetaData | logInId           | string   | The identifier of the **Login** event. |
| MetaData | merchantTimeStamp | DateTime | The time stamp for the event. |
| MetaData | userId            | string   | The user identifier. This information is provided by the merchant. |
| StatusDetails   | statusType        | string   | The type of status: **Approved**, **Rejected**, or **Pending**. |
| StatusDetails   | reasonType        | enum     | The type of reason: **challenge abandoned**, **challenge failed**, **challenge passed**, **challenge pending**, **review failed**, **review passed**, **review pending**, or **None**. The default value is **None**. |
| StatusDetails   | challengeType     | enum     | The type of review status: **SMS**, **Email**, **Phone**, **Other**, or **None**. The default value is **None**. |
| StatusDetails   | statusDate        | DateTime | The date and time when the status was applied. The format is ISO 8601. |


## AccountUpdate

The **AccountUpdate** API lets you share account information updates with Fraud Protection. For example, the following information might be edited or added: user profile, address, payment instrument, phone number, email address, and SSO. This event is a data ingestion event only.

| Object                              | Attribute                   | Type     | Description |
|-------------------------------------|-----------------------------|----------|---------------------------|
|                                     | Name                        | string   | The value is **AP.AccountUpdate**. |
|                                     | Version                     | string   | The value is **0.5**. |
| MetaData                            | trackingId                  | string   | The identifier of the **AccountUpdate** event. |
| MetaData                            | SignupId                    | string   | The identifier of the **AccountUpdateId** event. (This value can match the value of the **trackingId** attribute.) |
| MetaData                            | customerLocalDate           | dateTime | The creation date of the **AccountUpdate** event, in the customer's local time zone. The format is ISO 8601. |
| MetaData                            | merchantTimeStamp           | dateTime | The time stamp for the event. |
| DeviceContext                       | DeviceContextId             | string   | The customer's session ID. This information is mastered by DFP Device Fingerprinting Service. |
| DeviceContext                       | ipAddress                   | string   | The customer's IP address, as provided by the merchant. |
| DeviceContext                       | provider                    | string   | The provider of device information. Possible values are **DFPFingerprinting** and **Merchant**. If no value is specified, the default value is **DFPFingerprinting**. |
| DeviceContext                       | externalDeviceId            | string   | The customer's device ID, as provided and mastered by the merchant. |
| DeviceContext                       | externalDeviceType          | string   | The customer's device type, as provided and mastered by the merchant. Possible values are **Mobile'**, **Computer**, **MerchantHardware**, **Tablet**, and **GameConsole**. |
| User                                | userId                      | string   | The user identifier. This information is provided by the merchant. |
| User                                | userType                    | string   | The user's profile type. Possible values are **Consumer**, **Developer**, **Seller**, **Publisher**, and **Tenant**. |
| User                                | UserName                    | string   | The user-provided user name that is unique in the merchant system. |
| User                                | firstName                   | string   | The user-provided first name on the account. |
| User                                | lastName                    | string   | The user-provided last name on the account. |
| User                                | CountryRegion                     | string   | The user's country or region. The value should be a two-letter ISO country/region code (for example, **US**). |
| User                                | zipCode                     | string   | The user's postal code. |
| User                                | timeZone                    | string   | The user's time zone. |
| User                                | language                    | string   | The user's language and territory (for example, **EN-US**). |
| User                                | membershipId                | string   | The membership ID, if the user already has an existing membership with the merchant. |
| User                                | isMembershipIdUserName      | bool     | A **True**/**False** value that indicates whether the **membershipId** value can be used as the user name. The default value is **False**. |
| Phone                       | phoneType                   | enum     | The type of phone number. Possible values are **Primary** and **Alternative**. The default value is **Primary**. |
| Phone                       | phoneNumber                 | string   | The user's phone number. The format should be the country/region code followed by a hyphen (\-) and then the phone number (for example, for the US, **+1-1234567890**). |
| Phone                       | isPhoneNumberValidated      | bool     | A **True**/**False** value that indicates whether the user-provided phone number has been verified as owned by the user. |
| Phone                       | phoneNumberValidatedDate    | dateTime | The validation date of the user's phone number. The format is ISO 8601. |
| Phone                       | isPhoneUserName             | bool     | A **True**/**False** value that indicates whether the phone number can be used as the user name. The default value is **False**. |
| Email                       | emailType                   | enum     | The type of email address. Possible values are **Primary** and **Alternative**. |
| Email                       | emailValue                       | string   | The user's email address. This value is case-insensitive. |
| Email                       | isEmailValidated            | bool     | A **True**/**False** value that indicates whether the user-provided email address has been verified as owned by the user. |
| Email                       | emailValidatedDate          | dateTime | The validation date of the user's email address. The format is ISO 8601. |
| Email                       | isEmailUserName             | bool     | A **True**/**False** value that indicates whether the email address can be used as the user name. The default value is **False**. |
| SSOAuthenticationProvider   | authenticationProvider      | string   | The user's SSO authentication provider, if it differs from the merchant's SSO authentication provider. Possible values are **MSA**, **Facebook**, **PSN**, **MerchantAuth**, and **Google**. |
| SSOAuthenticationProvider   | displayName                 | string   | The user's display name for the SSO authentication provider (for example, the user name from a Microsoft account, Facebook, or Google). |
| Address                     | addressType                 | enum     | The type of address. Possible values are **Primary**, **Billing**, **Shipping**, and **Alternative**. The default value is **Primary**. |
| Address                     | firstName                   | string   | The user-provided first name that is associated with the address. |
| Address                     | lastName                    | string   | The user-provided last name that is associated with the address. |
| Address                     | phoneNumber                 | string   | The user-provided phone number that is associated with the address. |
| Address                     | street1                     | string   | The first row that was provided for the address. |
| Address                     | street2                     | string   | The second row that was provided for the address. (This value can be blank.) |
| Address                     | street3                     | string   | The third row that was provided for the address. (This value can be blank.) |
| Address                     | city                        | string   | The city that was provided for the address. |
| Address                     | state                       | string   | The state or province that was provided for the address. |
| Address                     | district                    | string   | The district that was provided for the address. |
| Address                     | zipCode                     | string   | The postal code that was provided for the address. |
| Address                     | CountryRegion                     | string   | The country/region code that was provided for the address. The value should be a two-letter ISO country/region code (for example, **US**). |
| PaymentInstrument                   | merchantPaymentInstrumentId | string   | The identifier of the payment instrument. This information is provided by the merchant. |
| PaymentInstrument                   | type                        | enum   | The type of payment. Possible values are **CreditCard**, **DirectDebit**, **PayPal**, **MobileBilling**, **OnlineBankTransfer**, **Invoice**, **MerchantGiftCard**, **MerchantWallet**, **CashOnDelivery**, **Paytm**, and **CCAvenue**. |
| PaymentInstrument                   | creationDate                | DateTime | The date of the first entry for the payment instrument in the merchant's system. The format is ISO 8601. |
| PaymentInstrument                   | updateDate                  | DateTime | The date of the last update for the payment instrument in the merchant's system. The format is ISO 8601. |
| PaymentInstrument                   | state                       | string   | The current state of the payment instrument in the merchant's system (for example, **Active**, **Blocked**, or **Expired**). |
| PaymentInstrument                   | cardType                    | string   | This attribute is used only for payments of the **CreditCard** or **DirectDebit** types. Possible values are **Visa**, **Mastercard**, **Amex**, **ACH**, **SEPA**, **UnionPay**, **Inicis**, **MobileBillingCarrier**, **Discover**, **AllPay**, **JCB**, and **DiscoverDiners**. |
| PaymentInstrument                   | holderName                  | string   | The name of the payment instrument's user. This attribute is used only for payments of the **CreditCard** **DirectDebit** types. |
| PaymentInstrument                   | bin                         | string   | This attribute is used only for payments of the **CreditCard** or **DirectDebit** types. |
| PaymentInstrument                   | expirationDate              | string   | The expiration date for the payment instrument in the merchant's system. The format is ISO 8601. This attribute is used only for payments of the **CreditCard** or **DirectDebit** types. |
| PaymentInstrument                   | lastFourDigits              | string   | This attribute is used only for payments of the **CreditCard** or **DirectDebit** types. |
| PaymentInstrument                   | email                       | string   | The email address that is associated with the payment instrument. This attribute is used only for payments of the **PayPal** type. |
| PaymentInstrument                   | billingAgreementId          | string   | This attribute is used only for payments of the **PayPal** type. |
| PaymentInstrument                   | payerId                     | string   | This attribute is used only for payments of the **PayPal** type. |
| PaymentInstrument                   | payerStatus                 | string   | A value that indicates whether PayPal has verified the payer. This attribute is used only for payments of the **PayPal** type. |
| PaymentInstrument                   | addressStatus               | string   | A value that indicates whether PayPal has verified the payer's address. This attribute is used only for payments of the **PayPal** type. |
| PaymentInstrument                   | imei                        | string   | This attribute is used only for payments of the **MobileBilling** type. |
| PaymentInstrument \\ BillingAddress | addressType                 | enum     | The type of address. Possible values are **Primary**, **Billing**, **Shipping**, and **Alternative**. The default value is **Billing**. |
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
| PaymentInstrument \\ BillingAddress | CountryRegion                     | string   | The country/region code that was provided for the address. The value should be a two-letter ISO country/region code (for example, **US**). |


## Labels

The **Labels** API lets you share additional information about the outcomes of transactions and events for model training that is based on an additional set of fraud signals. This information includes information that you receive from banks. This event is a data ingestion event only.

| Category | Attribute          | Type     | Description |
|----------|--------------------|----------|-------------|
|          | Name               | string   | The value is **AP.AccountLabel**. |
|          | Version            | string   | The value is **0.5**. |
| MetaData | TrackingId         | String   | The unique ID for each event/record. |
| MetaData | merchantTimeStamp  | DateTime | The date, in the merchant's time zone. The format is ISO 8601. |
| MetaData | userId             | string   | The user identifier. This information is provided by the merchant. |
| Label    | EventTimeStamp     | DateTime | The date and time of the event. Possible values are the chargeback date and the review date. The format is ISO 8601. |
| Label    | LabelObjectType    | enum   | The type of label: **Purchase**, **Account Creation**, **Account Login**, **Account Update**, **Custom Fraud Evaluation**, **Account**, **Payment instrument**, or **Email**. |
| Label    | LabelObjectId      | String   | The identifier field for the object: **PurchaseId**, **AccountCreationId**, **AccountLoginId**, **AccountUpdateId**, **UserId**, **MerchantPaymentInstrumentId**, or **Email**. |
| Label    | LabelSource        | enum   | The source of the label: **Customer Escalation**, **Chargeback**, **TC40\_SAFE**, **Manual Review**, **Refund**, **Offline Analysis**, or **Account Protection Review**. |
| Label    | LabelState         | enum   | The current status of the label: **Inquiry Accepted**, **Fraud**, **Disputed**, **Reversed**, **Abuse**, **Resubmitted Request**, **AccountCompromised**, or **AccountNotCompromised**. |
| Label    | LabelReasonCodes   | enum   | The reason codes that are associated with each type of label: **Processor/Bank Response Code**, **Fraud Refund**, **Account TakeOver**, **Payment Instrument Fraud**, **Account Fraud**, **Abuse**, **Friendly Fraud**, **Account Credentials Leaked**, or **Passed Account Protection Checks**. |
| Label    | Processor          | String   | The name of the bank or payment processor that generates the TC40 or System to Avoid Fraud Effectively (SAFE) information. |
| Label    | EffectiveStartDate | DateTime | The date when this label becomes effective. The format is ISO 8601. |
| Label    | EffectiveEndDate   | DateTime | The end date for this label. The format is ISO 8601. |
