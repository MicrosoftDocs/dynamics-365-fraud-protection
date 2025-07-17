---
author: josaw1
description: This article explains how to integrate real-time APIs in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: how-to
search.audienceType:
  - admin
  - IT Pro
title: Integrate purchase protection APIs
ms.custom: sfi-ga-nochange
---

# Integrate purchase protection APIs

[!include[deprecation](includes/deprecation.md)]

This article explains how to integrate real-time application programming interfaces (APIs) in Microsoft Dynamics 365 Fraud Protection.

To take advantage of the full suite of Fraud Protection features, you must send your transaction data to the real-time Fraud Protection APIs. In the evaluate experience, sending your transaction data enables you to analyze the results of using Fraud Protection. In the protect experience, you can also honor decisions, based on the rules that you've configured.

Depending on how you use Fraud Protection, you might use different sets of the following purchase protection APIs: 

- Purchase
- PurchaseStatus
- BankEvent
- Chargeback
- Refund
- UpdateAccount
- Label

## API integration phases 

The integration of purchase protection APIs occurs in three phases: 

1. [Create Microsoft Entra applications](#create-microsoft-entra-applications) via Fraud Protection. 
1. [Generate an access token](#generate-an-access-token).
1. [Call the APIs](#call-the-apis).

## Sign in

> [!IMPORTANT]
> You must be a global administrator in your Azure tenant to complete the initial sign-in.

Visit the following portals for each environment that you intend to use. Sign in, and accept the terms and conditions if you're prompted to do so.

- [Sandbox environment](https://dfp.microsoft-int.com) 
- [Production environment](https://dfp.microsoft.com) (You might already have completed this step in production during initial sign-up.)

## Create Microsoft Entra applications

> [!IMPORTANT]
> You must be an application administrator, cloud application administrator, or global administrator in your Azure tenant to complete this step.

To acquire the tokens that are required to call the APIs, you must configure and use Microsoft Entra applications as described in this section.

### Configure Microsoft Entra applications

To configure Microsoft Entra applications, follow these steps.

1. In the Fraud Protection portal, in the left navigation pane, select **Integration \> Create Microsoft Entra Application \> Setup now**. 
1. Complete the page to create your app. We recommend that you create one Microsoft Entra application for each environment that you want to integrate with Fraud Protection. 
1. Enter or select values for the following required fields: 

    - **Application display name** – Give your application a descriptive name. The maximum length is 93 characters. 
    - **Authentication method** – Select whether you want to authenticate via a certificate or a secret (password). 

1. If you selected the certificate authentication method, follow these steps: 

    1. Select **Choose file** to upload the public key. (The matching private key is required when you acquire tokens.) 
    1. Select **Secret** to automatically generate a password after the application is created.

1. When you've finished setting the required fields, select **Create application**. The confirmation page summarizes your app's name, ID, and certificate thumbprint or secret, depending on the authentication method that you selected.

> [!IMPORTANT]
> Save your secret or certificate thumbprint information for future reference. The secret will only be displayed once.

### Create another application

To create another application, select **Create another application**. You can create as many apps as you require to run API calls in each of your environments. 

### Manage existing Microsoft Entra applications 

After you create your Microsoft Entra apps, you can manage them through the [Azure portal](https://portal.azure.com/#blade/Microsoft_Microsoft Entra ID_IAM/ActiveDirectoryMenuBlade/RegisteredApps). For more information, see [How and why applications are added to Microsoft Entra ID](/azure/active-directory/develop/active-directory-how-applications-are-added). 

## Generate an access token

To securely integrate your systems with Fraud Protection, obtain a Microsoft Entra token, and provide it in the header of each API call.

> [!NOTE]
> Access tokens have a limited lifespan of 60 minutes. We recommend that you cache and reuse a token until it's close to expiring. You can then get a new access token.

The following information is needed to obtain a token.

### Required IDs and information

- **Environment URI** – The URIs for your sandbox or production environment appear on the **Configuration** tab of the **API Management** page in the Fraud Protection portal.
- **Directory (tenant) ID** – This ID is the globally unique identifier (GUID) of a tenant's domain in Azure. It appears in the Azure portal and on the **Configuration** tab of the **API Management** page in the Fraud Protection portal. 
- **Application (client) ID** – This ID identifies the Microsoft Entra app that you've created to call APIs. Get the ID from the **Real-time APIs** confirmation page, or find it later under **App registrations** in the Azure portal. There will be one ID for each app that you created.
- **Certificate thumbprint or secret** – Get the thumbprint or secret from the Real-time APIs confirmation page.
- **Instance ID** – This ID is the GUID of your environment in Fraud Protection. It appears in the **Integration** tile on the Fraud Protection dashboard.

### Examples: Code samples that show how to acquire a token by using your certificate or secret

The following C# code samples provide examples of acquiring a token with your certificate or secret. Replace the placeholders with your specific information.
For both of the C# samples, you'll need to import the [Microsoft.Identity.Client NuGet package](https://www.nuget.org/packages/Microsoft.Identity.Client/).

For samples in other languages, see https://aka.ms/aaddev. 

#### Get an access token by using an app ID and private certificate key

```csharp
/// <summary>
/// Gets an access token using an app ID and private certificate key.
/// </summary>
/// <param name="tenantId">Directory (tenant) ID, in GUID format</param>
/// <param name="clientId">Application (client) ID</param>
/// <param name="certPath">File path to the certificate file (pfx) used to authenticate your application to Microsoft Entra ID</param>
/// <param name="certPassword">Password to access to the certificate file's private key</param>
public async Task<string> AcquireTokenWithCertificate(string tenantId, string clientId, string certPath, string certPassword)
{
    var certificate = new X509Certificate2(certPath, certPassword);

    var app = ConfidentialClientApplicationBuilder.Create(clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, tenantId)
            .WithCertificate(certificate)
            .Build();

    var scopes = new string[] { "<API endpoint for INT or PROD>; should be https://api.dfp.microsoft-int.com/.default or https://api.dfp.microsoft.com/.default" };

    try
    {
        var result = await app.AcquireTokenForClient(scopes).ExecuteAsync();
        return result.AccessToken;
    }
    catch (MsalServiceException ex)
    {
        //Handle authentication exceptions
        throw ex;
    }
}
```

#### Get an access token by using an app ID and secret

```csharp
/// <summary>
/// Gets an access token using an app ID and secret.
/// </summary>
/// <param name="tenantId">Directory (tenant) ID, in GUID format</param>
/// <param name="clientId">Application (client) ID</param>
/// <param name="clientSecret">The secret (password) used to authenticate the client (application) ID</param>
public async Task<string> AcquireTokenWithSecret(string tenantId, string clientId, string clientSecret)

{
    var app = ConfidentialClientApplicationBuilder.Create(clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, tenantId)
            .WithClientSecret(clientSecret)
            .Build();

    var scopes = new string[] { "<API endpoint for INT or PROD>; should be https://api.dfp.microsoft-int.com/.default or https://api.dfp.microsoft.com/.default" };

    try
    {
        var result = await app.AcquireTokenForClient(scopes).ExecuteAsync();
        return result.AccessToken;
    }
    catch (MsalServiceException ex)
    {
        //Handle authentication exceptions
        throw ex;
    }
}
```

The **AuthenticationResult** object in each case contains the **AccessToken** value and an **ExpiresOn** property that indicates when the token will become invalid. 

- POST request to:

    - `https://login.microsoftonline.com/<Microsoft Entra tenant ID>/oauth2/token`

- Headers:

    - Content-type: application/x-www-form-urlencoded 

- Body (key-value):

    - grant_type: client_credentials 
    - client_id: {Your Client ID from previous step} 
    - client_secret: {Your secret from previous step} 
    - resource: `https://api.dfp.microsoft.com` (for int, `https://api.dfp.microsoft-int.com`)

- Response:

    - Use the value of **access\_token** from the response for the next step.

For more information, see the following Azure documentation:

- [Overview of Microsoft Authentication Library (MSAL)](/azure/active-directory/develop/msal-overview)
- [Acquire and cache tokens using the Microsoft Authentication Library (MSAL)](/azure/active-directory/develop/msal-acquire-cache-tokens)

## Call the APIs

To call the APIs, follow these steps. 

1. Pass the following required HTTP headers on each request. 

    | Header name | Header value |
    |-------------|--------------|
    | Authorization | <p>Use the following format for this header. (Replace *accesstoken* with the actual token value that's returned by Microsoft Entra ID.)</p><p>Bearer *accesstoken* |
    | x-ms-correlation-id | Send a new GUID value on each set of API calls that are made together. |
    | x-ms-dfpenvid | Send the GUID value of your instance ID. |

2. Generate an event-based payload. Fill in the event data with the relevant information from your system. For documentation about all supported events, see [Dynamics 365 Fraud Protection API](https://go.microsoft.com/fwlink/?linkid=2084942).
3. Combine the header (which includes the access token) and the payload, and then send them to your Fraud Protection endpoint.

    - POST request to:

        - `<Base URL>/v1.0/merchantservices/events/purchase`

    - Headers:

        - x-ms-correlation-id: {A GUID, which must be unique per request}
        - content-type: application/json
        - Authorization: {The token from the previous step}
        - x-ms-dfpenvid: {The environment ID of the target environment}

    - Body:

        - Get the sample account protection request body from the shared [Swagger page](https://dfpswagger.azurewebsites.net/index.html). 

> [!NOTE]
> If you create a new environment, include the environment ID in the API header during integration, so that the transactions can be correctly routed.

The following options are acceptable for x-ms-dfpenvid in the API call and the behavior is identical. 

  - Use the environment ID for the environment you're calling. The ID is listed on the **Integration** page in the **Environment ID** field.
  - Use the full pat of the **Customer API ID** from the root to the child environment you're calling using the forward slash (**/**) as a divider. For example, **/primary/XYZ**.
  - Use the full path of the environment ID or customer API ID from the root to the child environment you're calling using the forward slash (**/**) as a divider. For example, **7b925ca8-d372-4245-bc5a-94b5fdb6c067/XYZ**.

To specify the customer API ID when you creat an environment, see the article, [Manage environments](manage-psp-environments.md#create-a-new-environment).
  
## Best practices 

- Each Microsoft Entra token remains valid for 60 minutes. We recommend that you cache it for a shorter duration and reuse it. 
- Ensure that your HttpClient has keep-alive connections. 
- Always pass the **x-ms-dfpenvid** header, and ensure that it points to the environment of the merchant that you want to send transactions on behalf of. 
- Store the secret in a secret store. 
- Always pass the **x-ms-correlation-id** header for future debugging sessions with Fraud Protection. 
- Ensure that the **x-ms-correlation-id** header is unique for every transaction that is sent to Fraud Protection.  

## View the sample app 

For additional reference, you can view the [sample merchant app](https://go.microsoft.com/fwlink/?linkid=2085137) and the accompanying developer documentation. The sample app provides an example of how to call Fraud Protection APIs, including API events such sending customer account updates, refunds, and chargebacks in real time. The documentation for the sample app is linked to actual sample code whenever such links are possible. Otherwise, code samples exist directly in the documentation.

For guidance about how to configure the sample site for your use, see [Configure the sample site](https://go.microsoft.com/fwlink/?linkid=2100635).

[!INCLUDE[footer-include](includes/footer-banner.md)]
