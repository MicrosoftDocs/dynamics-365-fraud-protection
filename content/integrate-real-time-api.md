---
author: josaw1
description: This topic explains how to integrate Microsoft Dynamics 365 Fraud Protection real-time APIs.
ms.author: josaw
ms.date: 11/19/2020
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Integrate purchase protection APIs
---

# Integrate purchase protection APIs

To take advantage of the full suite of Microsoft Dynamics 365 Fraud Protection features, send your transaction data to the real-time APIs. In the evaluate experience, this allows you to analyze the results of using Fraud Protection. In the protect experience, you can also honor decisions based on the rules you have configured.

Depending on how you choose to use Fraud Protection, you may make use of different sets of APIs, as shown below: 

- **Purchase protection APIs**: Purchase, PurchaseStatus, BankEvent, Chargeback, Refund, UpdateAccount, Label
- **Account protection APIs**: SignUp, SignUpStatus, Label

For documentation about all supported events, see <a href="https://go.microsoft.com/fwlink/?linkid=2084942" target="_blank">Dynamics 365 Fraud Protection API</a>.


## Set up

### Sign in
> [!IMPORTANT]
> You must be a Global Administrator in your Microsoft Azure tenant to complete the initial sign-in.

Visit the portal for each environment you intend to use, sign in, and accept the terms and conditions if prompted.
- Sandbox - <a href="https://dfp.microsoft-int.com" target="_blank">https://dfp.microsoft-int.com</a> 
- Production - <a href="https://dfp.microsoft.com" target="_blank">https://dfp.microsoft.com</a> (You might already have completed this step in production during initial sign-up.)

### Create Azure Active Directory applications
> [!IMPORTANT]
> You must be an Application Administrator, Cloud Application Administrator, or Global Administrator in your Azure tenant to complete this step.

To acquire the tokens required to call the APIs, you must use Azure Active Directory (Azure AD) applications. You can configure these by applications using the **Real-time APIs** page in Fraud Protection.

#### To configure Azure AD applications:

1. In the left navigation, select **Data**, select **API management**, and then select **Configuration**. 
1. Complete the form to create your app. We recommend creating one Azure AD application for each environment that you operate. 

   The following fields are required: 
    - **Application display name** - Give your application a descriptive name. Maximum length is 93 characters. 
    - **Environment** - Choose whether this application should call your production or integration (sandbox) endpoint. 
    - **Authentication method** - Choose whether you would like to authenticate via certificate or a secret (password). 

1. For the certificate method, select: 
    1. **Choose file** to upload the public key. (The matching private key is required when you acquire tokens.) 
    1. **Secret** to automatically generate a password after the application has been created.

1. When you finish filling in the fields, select **Create application**. 

  The confirmation screen summarizes your app's name, ID, and the certificate thumbprint or secret, depending on your authentication method. 

> [!IMPORTANT]
> Please save your secret or certificate thumbprint information for future reference. The secret will only be displayed once.

#### To create an additional application:

- Select **Create another application**. 

You can create as many apps as necessary to run API calls in each of your environments. 

### Manage existing Azure AD applications 
After you create your Azure AD apps, you can manage them through the <a href="https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps" target="_blank">Azure portal</a>. For more information, see <a href="/azure/active-directory/develop/active-directory-how-applications-are-added" target="_blank">Azure documentation site</a>. 

### Manually configure Azure AD applications
To set up your applications directly in Azure, see [Create Azure AD apps in Azure Portal or PowerShell](azure-apps-portal-powershell.md). 

## Call the Fraud Protection real-time APIs 
To integrate your systems with Fraud Protection, complete the following sections.

### Required IDs and information
- **Environment URI** - The URIs for your sandbox or production environment appear on the **Configuration** tab of the **API Management** page in the Fraud Protection portal.
- **Directory (tenant) ID** - The Directory ID is the globally unique identifier (GUID) for a tenant's domain in Azure. It appears in the Azure portal and on the **Configuration tab** of the **API Management** page in the Fraud Protection portal. 
- **Application (client) ID** - This identifies the Azure AD app you've created for calling APIs. Get the ID from the **Real-time APIs** confirmation screen or find it later in the Azure portal under **App registrations**. There will be one ID for each app you created.
- **Certificate thumbprint or secret** - Get the thumbprint or secret from the Real-time APIs confirmation screen.

### Generate an access token
You must generate an Azure AD access token and provide it with each DFP API call. Note that access tokens have a limited lifespan. We recommend that you cache and reuse the token until it gets close to expiring, at which time you can get a new access token.
The following C# code samples provide examples of acquiring a token with your certificate or secret. Replace the placeholders with your specific information.
For both of these C# samples, you will need to import the following [Microsoft.Identity.Client NuGet package](https://www.nuget.org/packages/Microsoft.Identity.Client/).

For samples in other languages, see https://aka.ms/aaddev. 

**Certificate thumbprint**
```cs
/// <summary>
/// Gets an access token using an app ID and private certificate key.
/// </summary>
/// <param name="tenantId">Directory (tenant) ID, in GUID format</param>
/// <param name="clientId">Application (client) ID</param>
/// <param name="certPath">File path to the certificate file (pfx) used to authenticate your application to AAD</param>
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

**Secret**
```cs

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
The AuthenticationResult object in each case contains the AccessToken itself, and an ExpiresOn property which indicates when the token will become invalid. 

For more information, refer to the Azure documentation: 

- [Overview of Microsoft Authentication Library (MSAL)](/azure/active-directory/develop/msal-overview)
- [Acquire and cache tokens using the Microsoft authentication library (MSAL)](/azure/active-directory/develop/msal-acquire-cache-tokens)


### Call the APIs
To call the APIs, follow these steps:

<ol>
 <li> 
    Pass the following required HTTP headers on each request. 
    <table> 
    <tr> 
    <th>Header name</th> 
    <th>Header value</th> 
    </tr> 
    <tr> 
    <td>Authorization</td> 
    <td>
    Use the following format for this header (replace <i>accesstoken</i> with the actual token value):<br /> 
        <ul><li> Bearer <i>accesstoken</i>, where accesstoken is the token that is returned by Azure AD.</li></ul> 
    </td> 
    </tr> 
    <tr> 
    <td>x-ms-correlation-id</td> 
    <td>Send a new GUID value on each set of API calls that are made together.</td> 
    </tr> 
    </table> 
    </li> 
   <li>Generate an event-based payload. Fill in the event data with the relevant information from your system. For documentation about all supported events, see <a href="https://go.microsoft.com/fwlink/?linkid=2084942">Dynamics 365 Fraud Protection API</a>. 
    </li> 
   <li>Combine the header (which includes the access token) and the payload, and then send them to your Fraud Protection endpoint.</li>
</ol>


## View the sample app 
For additional reference, view the <a href="https://go.microsoft.com/fwlink/?linkid=2085137" target="_blank">sample merchant app</a> and the accompanying developer documentation. The sample app provides an example of how to call Fraud Protection APIs, including API events like sending customer account updates, refunds, and chargebacks in real time. The documentation for the sample app is linked to actual sample code whenever such links are possible. Otherwise, code samples exist directly in the documentation.

For guidance on configuring the sample site for your use, view <a href="https://go.microsoft.com/fwlink/?linkid=2100635" target="_blank">Configure the sample site</a>.



[!INCLUDE[footer-include](includes/footer-banner.md)]
