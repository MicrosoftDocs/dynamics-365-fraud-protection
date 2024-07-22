---
author: josaw1
description: This article describes how to set up customer accounts protection in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Set up customer accounts protection
---

# Set up customer accounts protection

Microsoft Dynamics 365 Fraud Protection includes account protection capabilities to help you assess whether any suspicious activity is occurring in your business ecosystem. These capabilities include risk assessment capabilities that you can use to block or challenge fraudulent attempts to create accounts or compromise existing accounts. Here are some examples:

-	APIs for real-time risk assessment
-	A rule and list experience that you can use to optimize your risk strategy according to your business needs
-	Monitoring dashboards that you can use to monitor fraud protection effectiveness and trends in your ecosystem

Account protection covers three types of account lifecycle events: *account creation*, *account login*, and *custom assessment*. For each event type, there are multiple lines of defense:

-	**Efficient bot detection**: When Fraud Protection detects an automated attempt to use a list of compromised credentials or brute force to create or modify accounts, its first line of defense is dynamic and robust **bot detection**. This advanced adaptive artificial intelligence (AI) quickly generates a score that is mapped to the probability that a bot is initiating the event.
-	**Real-time reinforced assessment**: As its next line of defense, Fraud Protection uses AI models to generate a **risk assessment score**. You can use this score with rules to approve, challenge, reject, or review sign-in and sign-up attempts, based on business needs.

## Goals for this document

This document guides you through the following activities:

-	[Step 1: Implement account protection APIs](promocode-set-up-account-protection.md#step-1-implement-account-protection-apis)
-	[Step 2: Create Microsoft Entra apps](promocode-set-up-account-protection.md#step-2-create-microsoft-entra-apps)
-	[Step 3: Understand account protection events](promocode-set-up-account-protection.md#step-3-understand-account-protection-events)

    After you complete these activities, you will be able to use account protection to block or challenge suspicious attempts to compromise existing accounts.

## Prerequisites

Before you begin the activities in this document, you must complete the following tasks:

-	Set up Fraud Protection in an Microsoft Entra tenant as described in [Set up a trial version of Fraud Protection](promocode-set-up-dfp-trial-version.md).
-	[Set up device fingerprinting](device-fingerprinting.md).

## Step 1: Implement account protection APIs

To take advantage of the full suite of features in Fraud Protection, send your transaction data to the real-time APIs.

-	In the evaluate experience, you can analyze the results of using Fraud Protection.
-	In the protect experience, you can honor decisions based on the rules that you've configured.

You can use different **account protection APIs** depending on how you want to use Fraud Protection. Examples of these APIs include: *AccountCreation*, *AccountLogin*, *AccountCreationStatu*s, *AccountLoginStatus*, *AccountUpdate*, *Label*, and *Custom Events*.

For more information about supported events, see [Dynamics 365 Fraud Protection API](https://go.microsoft.com/fwlink/?linkid=2084942).

## Step 2: Create Microsoft Entra apps

> [!IMPORTANT]
> To complete this step, you must be an application administrator, a cloud application administrator, or a global administrator in your Microsoft Entra tenant.

To acquire the tokens that are required to call the APIs, use Fraud Protection to configure Microsoft Entra applications.

### Configure a Microsoft Entra app

1.	In the [Fraud Protection portal](https://dfp.microsoft.com/), in the left navigation, select **Data**, and then select **API management**.
2.	On the **API management** page, select **Configuration**.
3.	Select **Creating applications**, and then fill in the fields to create your app. The following fields are required:

    - **Application display name** – Enter a descriptive name for your app. The maximum length is 93 characters.
    - **Environment** – Select the production endpoint.
    - **Authentication method** – Select whether a certificate or a secret (password protected) is used for authentication.
    
      - Select **Certificate**, and then select **Choose file** to upload the public key. When you acquire tokens, you will need the matching private key.
      - Select **Secret** to automatically generate a password after the application has been created.

4.	When you've finished filling in the fields, select **Create application**.

    The confirmation page summarizes the app's name and ID, and either the certificate thumbprint or the secret, depending on the authentication method that you selected.

> [!IMPORTANT]
> Save the information about your certificate thumbprint or secret for future reference. This information will be shown only once.

#### Create additional apps

You can create as many apps as you require to run API calls in your production environments.

1.	On the **Configuration** tab, select **Create another application**.
2.	Fill in the fields to create your app, and then select **Create application**.

### Call the Fraud Protection real-time APIs

Use the information in this section to integrate your systems with Fraud Protection.

#### Required IDs and information

-	**API Endpoint** – The URI for your environment appears on the **Account information** tile on the Fraud Protection dashboard.
-	**Directory (tenant) ID** – The directory ID is the globally unique identifier (GUID) for a tenant's domain in Azure. It appears in the Azure portal and on the **Account information** tile on the Fraud Protection dashboard.
-	**Application (client) ID** – The application ID identifies the Microsoft Entra app that you created to call APIs. You can find this ID on the confirmation page that appears after you select **Create application** on the **API Management** page. You can also find it later, under **App registrations** in the Azure portal. There will be one ID for each app that you create.
-	**Certificate thumbprint or secret** – You can find the certificate thumbprint or the secret on the confirmation page that appears after you select **Create application** on the **API Management** page.
-	**Instance ID** - The instance ID is the globally unique identifier (GUID) for your environment in Fraud Protection. It appears in the **Integration** tile on the Fraud Protection dashboard.

### Generate an access token

You must generate this token and provide it with each API call. Note that access tokens have a limited lifespan. We recommend that you cache and reuse each access token until it's time to get a new one.
The following C# code samples show how you can acquire a token by using your certificate or secret. Replace the placeholders with your own information.

**CERTIFICATE thumbprint**

```json
   public async Task<string> AcquireTokenWithCertificateAsync()
     {
          var x509Cert = CertificateUtility.GetByThumbprint("<Certificate thumbprint>");
          var clientAssertion = new ClientAssertionCertificate("<Client ID>", x509Cert);
          var context = new AuthenticationContext("<Authority URL. Typically https://login.microsoftonline.com/[Directory_ID]>");
          var authenticationResult = await context.AcquireTokenAsync("<API endpoint>", clientAssertion);
          
          return authenticationResult.AccessToken;
     }
```

**Secret**

```json
   public async Task<string> AcquireTokenWithSecretAsync()
     {
          var clientAssertion = new ClientCredential("<Client ID>", "<Client secret>");
          var context = new AuthenticationContext("<Authority URL. Typically https://login.microsoftonline.com/[Directory_ID]>");
          var authenticationResult = await context.AcquireTokenAsync("<API endpoint>", clientAssertion);
          
          return authenticationResult.AccessToken;
     }
```

**Response**

Behind the scenes, the preceding code generates an HTTP request and receives a response that resembles the following example.

```json
   HTTP/1.1 200 OK
     Content-Type: application/json; charset=utf-8
     Date: <date>
     Content-Length: <content length>
     {
          "token_type":"Bearer",
          "expires_in":"3599",
          "ext_expires_in":"3599",
          "expires_on":"<date timestamp>",
          "not_before":"<date timestamp>",
          "resource":"https://api.dfp.dynamics.com",
          "access_token":"<your access token; e.g.: eyJ0eXA...NFLCQ>"
     }
```

For more information about access tokens, see the following Azure documentation:

- [Use client assertion to get access tokens from Microsoft Entra ID](/azure/architecture/multitenant-identity/client-assertion)
- [Cache access tokens](/azure/architecture/multitenant-identity/token-cache)

### Call the APIs

1.	Pass the following required HTTP headers on each request.

| Header name	| Header value|
|----------------|------------------|
| Authorization	| <p>Use the following format for this header: Bearer *accesstoken*</p><p>In this format, accesstoken is the token that is returned by Microsoft Entra ID.</p>| 
| x-ms-correlation-id	| Send a new GUID value on each set of API calls that are made together.| 
| Content-Type	| application/json| 
| x-ms-dfpenvid       | Send the GUID value of your Instance ID. |

2.	Generate an event-based payload. Fill in the event data with the relevant information from your system. 

    For more information about supported events, see [Dynamics 365 Fraud Protection API](https://go.microsoft.com/fwlink/?linkid=2084942).
    
3.	Combine the header (which includes the access token) and the payload, and then send them to your Fraud Protection endpoint. (The API endpoint is the URI for your environment and appears on the Account information tile on the Fraud Protection dashboard.)

For more information about APIs, see [Dynamics 365 Fraud Protection API](https://go.microsoft.com/fwlink/?linkid=2084942).   
## Step 3: Understand account protection events

### Account Create

Use the **Account Create** event to send information and context about an incoming attempt to create a new account. The response contains a decision for the Account Creation API.

**URI**: \<API Endpoint\>/v1.0/action/account/create/\<signUpId\>

The value of **signUpId** should be unique per request. It should match the value in the metadata section in the sample that follows.

> [!IMPORTANT]
> The value of **deviceContextId** should match the value of **session_id** in the device fingerprinting settings.

#### Sample payload

```json
   {
          "device": {
               "deviceContextId": "2cf391cc-62d2-47d4-a9c1-78ec025293da",
               "ipAddress": "192.168.8.214",
               "provider": "DFPFingerprinting",
               "externalDeviceId": "1234567890",
               "externalDeviceType": "Tablet"
     },
     "user": {
          "userId": " cf4e1d39-1100-4791-a6cf-98580f3d91cb",
          "userType": "Consumer",
          "username": "kayla@contoso.com",
          "firstName": "Kayla",
          "lastName": "Goderich",
          "countryRegion": "US",
          "zipCode": "44329",
          "timeZone": "-08:00",
          "language": "en-us",
          "membershipId": " CC004567",
          "isMembershipIdUsername": false
     },
     "email": [
          {
          "emailType": "Primary",
          "emailValue": "kayla@contoso.com",
          "isEmailValidated": true,
          "emailValidatedDate": "2018-11-27T15:12:26.9733817-08:00",
          "isEmailUsername": true
          }
     ],
     "phone": [
          {
               "phoneType": "Alternative",
               "phoneNumber": "1-4985550190",
               "isPhoneNumberValidated": true,
               "phoneNumberValidatedDate": "2018-11-27T15:12:26.9739451-08:00",
               "isPhoneUsername": false
          }
     ],
     "address": [
          {
               "addressType": "Primary",
               "firstName": "Kayla",
               "lastName": "Goderich",
               "phoneNumber": "1-4985550190",
               "street1": "0123 Bechtelar Loop",
               "street2": "",
               "street3": "",
               "city": "Kubtown",
               "state": "SC",
               "district": "",
               "zipCode": "44329",
               "countryRegion": "US"
          }
     ],
     "paymentInstruments": [
          {
               "merchantPaymentInstrumentId": "6ac8406f-128a-41ce-a02d-1bbaa23fbe15",
               "type": "Credit Card",
               "creationDate": "2020-03-24T13:23:32.3247803-07:00",
               "updateDate": "2020-03-24T13:23:32.3248203-07:00"
          }
     ],
     "ssoAuthenticationProvider": {
          "authenticationProvider": "MerchantAuth",
          "displayName": "Kayla Goderich"
     },
     "metadata": {
          "signUpId": "f5085b48-0f9d-47f5-85d1-2c95e7842d39",
          "customerLocalDate": "2020-02-25T15:12:26.9653975-08:00",
          "assessmentType": "Protect",
          "trackingId": "d65544f0-f8b4-4249-a5e0-94b32a25548f",
          "merchantTimeStamp": "2020-11-27T15:12:26.9721842-08:00"
     },
     "name": "AP.AccountCreation",
     "version": "0.5"
     }
```

### Account Login

Use the **Account Login** event to send information and context about an incoming attempt to create a new account login. The response contains a decision for the Account Login API.

**URI**: \<API Endpoint\>/v1.0/action/account/login/<userId\>

The value of userId must match the value in the payload. Each user must have a unique value. A GUID value can be used here.

> [!IMPORTANT]
> The value of **deviceContextId** should match the value of **session_id** in the device fingerprinting settings.

#### Sample payload

```json
  {
     "device": {
          "deviceContextId": "2ef10376-2ba8-4f36-a911-da438e5e5e27",
          "ipAddress": "192.168.8.214",
          "provider": "DFPFingerprinting",
          "externalDeviceId": "1234567890",
     "externalDeviceType": "Computer"
     },
     "user": {
          "userId": "cf4e1d39-1100-4791-a6cf-98580f3d91cb",
          "userType": "Consumer",
          "username": "kayla@contoso.com",
          "firstName": "Kayla",
          "lastName": "Goderich",
          "countryRegion": "US",
          "zipCode": "44329",
          "timeZone": "-08:00",
          "language": "en-us",
          "membershipId": "CC004567",
          "isMembershipIdUsername": false
     },
     "recentUpdate": {
          "lastPhoneNumberUpdateDate": "2018-11-127T15:22:42.3412611-08:00",
          "lastEmailUpdateDate": "2018-11-127T15:22:42.3412611-08:00 ",
          "lastAddressUpdateDate": "2018-11-127T15:22:42.3412611-08:00",
          "lastPaymentInstrumentUpdateDate": "2018-11-127T15:22:42.3412611-08:00"
     },
     "ssoAuthenticationProvider": {
          "authenticationProvider": "MerchantAuth",
          "displayName": "Kayla Goderich"
     },
     "metadata": {
          "LogInId": "a15d4a5d-fadc-49ab-8022-712fec597e22",
          "customerLocalDate": "2020-02-25T15:22:42.3397533-08:00",
          "assessmentType": "Protect",
          "trackingId": "a14ebdca-9447-49b4-951e-26f6ccc4445c",
          "merchantTimeStamp": "2020-11-27T15:22:42.3405921-08:00"
     },
     "name": "AP.AccountLogin",
     "version": "0.5"
  }
```

### Account Create Status

Use the **Account Create Status** event to send information and context about an incoming attempt to create a new account status. The response contains a decision for the Account Create Status API.

**URI**: \<API Endpoint>/v1.0/observe/account/create/status/<signUpId\>
  

The value of **userId** must match the value in the payload. Each user must have a unique value. A GUID value can be used here.

#### Sample payload

```json
  {
     "metadata":{
          "signUpId":"a6221a3f-c38c-429e-8fde-3026d8c29ed3",
          "userId":"34f47dc4-9781-4033-99fd-185649c4b001",
          "trackingId":"697a6bee-2d30-4132-92a6-c137aaf49c0a",
          "merchantTimeStamp":"2020-04-03T13:23:32.3226335-07:00"
     },
     "statusDetails":{
          "statusType":"Rejected",
          "reasonType":"ChallengeAbandoned",
          "challengeType":"Email",
          "statusDate":"2020-04-03T13:23:32.3817714-07:00"
     },
     "name":"AP.AccountCreation.Status",
     "version":"0.5"
  }
```

### Account Login Status

Use the **Account Login Status** event to send information and context about an incoming attempt to create a new account login status. The response contains a decision for the Account Login Status API.

**URI**: \<API Endpoint>/v1.0/observe/account/login/status/<userId\>

The value of **signUpId** must match the value in the payload. Each must have a unique value. A GUID value can be used here.

#### Sample payload

```json
  {
     "metadata":{
          "loginId":"dc4ea331-a6e5-4aa0-8eba-16b4d516a07d",
          "userId":"34f47dc4-9781-4033-99fd-185649c4b001",
          "trackingId":"dcd65c87-d3db-4a42-8ed3-3e59f443b994",
          "merchantTimeStamp":"2020-04-03T13:23:32.3759321-07:00"
     },
     "statusDetails":{
          "statusType":"Rejected",
          "reasonType":"ChallengeAbandoned",
          "challengeType":"Email",
          "statusDate":"2020-04-03T13:23:32.3884589-07:00"
     },
     "name":"AP.AccountLogin.Status",
     "version":"0.5"
  }
```

### Label

Use the **Label** event to send additional information to Fraud Protection, besides the data that informs the virtual fraud analyst and monitoring features. The **Labe**l API provides the additional information for model training that is based on an additional set of fraud signals. It also sends information about transactions, account or payment instrument details, and reversals.

**URI**: \<API Endpoint>/v1.0/label/account/create/<userId\>

The value of **userId** must match the value in the corresponding Account Login API.

#### Sample payload

```json
  {
     "metadata": {
          "name": "AP.Label.Metadata",
          "userId": "34f47dc4-9781-4033-99fd-185649c4b001",
          "merchantTimeStamp": "2020-06-14T21:53:27.8822492-08:00",
          "trackingId": "34f47dc4-9781-4033-99fd-185649c4b001"
     },
     "label": {
          "eventTimeStamp": "2020-02-21T21:53:27.8822492-08:00",
          "labelObjectType": "Account",
          "labelObjectId": "userid",
          "labelSource": "ManualReview",
          "labelState": "AccountCompromised",
          "labelReasonCode": "AccountFraud"
     },
     "name": "AP.Label",
     "version": "0.5"
     }
     public enum LabelObjectTypeName
          {
               Purchase,
               AccountCreation,
               AccountLogin,
               AccountUpdate,
               CustomFraudEvaluation,
               Account,
               PaymentInstrument,
               Email
          }
     public enum LabelSourceName
          {
               CustomerEscalation,
               Chargeback,
               TC40_SAFE,
               ManualReview,
               Refund,
               OfflineAnalysis,
               AccountProtectionReview
          }
     public enum LabelStateName
          {
               InquiryAccepted,
               Fraud,
               Disputed,
               Reversed,
               Abuse,
               ResubmittedRequest,
               AccountCompromised,
               AccountNotCompromised
          }
     public enum LabelReasonCodeName
          {
               ProcessorResponseCode,
               BankResponseCode,
               FraudRefund,
               AccountTakeOver,
               PaymentInstrumentFraud,
               AccountFraud,
               Abuse,
               FriendlyFraud,
               AccountCredentialsLeaked,
               PassedAccountProtectionChecks
          }
```


Congratulations! You have successfully completed the training and are ready to use Fraud Protection's account protection capabilities.

## Next steps

For information about how to access and use other Fraud Protection capabilities, see the following documents:

- [Set up device fingerprinting](device-fingerprinting.md)
- [Protect purchases with Dynamics 365 Fraud Protection](promocode-set-up-purchase-protection.md)
- [Prevent loss with Dynamics 365 Fraud Protection](promocode-set-up-loss-prevention.md)
