---
author: kelsiefu
description: This topic explains how to integrate Microsoft Dynamics 365 Fraud Protection real-time APIs.

ms.author: kelsiefu 
ms.service: fraud-protection
ms.date: 02/24/2020
ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Integrate account protection APIs


---

# Integrate account protection APIs

[!include [banner](includes/preview-banner.md)]

To take advantage of the full suite of Microsoft Dynamics 365 Fraud Protection features, send your transaction data to the real-time APIs. In the evaluate experience, this allows you to analyze the results of using Fraud Protection. In the protect experience, you can also honor decisions based on the rules you have configured.

Depending on how you choose to use Fraud Protection, you may make use of different APIs, as seen below: 

- **Account protection APIs**: AccountCreation, AccountLogin,	AccountCreationStatus, AccountLoginStatus,	AccountUpdate, Label


For documentation about all supported events, see [Dynamics 365 Fraud Protection API](https://go.microsoft.com/fwlink/?linkid=2084942).


## Get set up

### Sign in
> [!IMPORTANT]
> You must be a Global Administrator in your Microsoft Azure tenant to complete the initial API onboarding.

Visit the [portal](https://dfp.microsoft.com), sign in, and accept the terms and conditions if prompted. This will make sure that Fraud Protection is properly configured within your Azure tenant. (You might already have completed this step during initial sign-up.)

### Create Azure Active Directory applications
> [!IMPORTANT]
> You must be an Application Administrator, Cloud Application Administrator, or Global Administrator in your Azure tenant to complete this step.

To acquire the tokens required to call the APIs, you will need to utilize Azure Active Directory (Azure AD) applications. You can configure these by using the **Real-time APIs** page in Fraud Protection.

Select **Configuration** in the left navigation pane, and then select **Real-time APIs**. Complete the form to create your app.

The following fields are required: 
- **Application display name**: Give your application a descriptive name. Maximum length is 93 characters. 
- **Environment** - Choose the production endpoint. 
- **Authentication method**: Choose whether you would like to authenticate via certificate or a secret (password). For the certificate method, use the **Choose file** button to upload the public key. You will need the matching private key when you acquire tokens. If you select the **Secret** method, a password will be generated for you after application creation.

When you finish filling in the fields, select **Create application**. The confirmation screen summarizes your app's name, ID, and the certificate thumbprint or secret, depending on your authentication method. 

> [!IMPORTANT]
> Please save your secret or certificate thumbprint information for future reference. The secret will only be displayed once.

To create an additional application, select **Create another application**. You can create as many apps as necessary to run API calls in your production environments. 

### Manage existing Azure AD applications 
After you have created your Azure AD apps, you can manage them through the [Azure portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps). You can learn more from the [Azure documentation site](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).

### Manually configure Azure AD applications
If you would like to set up your applications directly in Azure, see [Create Azure AD apps in Azure Portal or PowerShell](azure-apps-portal-powershell.md).

## Call the Fraud Protection real-time APIs 
To integrate your systems with Fraud Protection, follow these steps.

### Required IDs and information
- **API Endpoint**: The URI for your environment appear on the **Account information** tile on the Fraud Protection dashboard.
- **Directory (tenant) ID**: The Directory ID is the globally unique identifier (GUID) for a tenant's domain in Azure. It appears in the Azure portal and on the **Account information** tile on the Fraud Protection dashboard. 
- **Application (client) ID**: This identifies the Azure AD app you created for calling APIs. Get the ID from the **Real-time APIs** confirmation screen or find it later in the Azure portal under **App registrations**. There will be one ID for each app you created.
- **Certificate thumbprint or secret**: Get the thumbprint or secret from the Real-time APIs confirmation screen.

### Generate an access token
You must generate this token and provide it with each API call. Note that access tokens have a limited lifespan. We recommend that you cache and reuse it until it's time to get a new access token.

The following C# code samples provide examples of acquiring a token with your certificate or secret. Replace the placeholders with your specific information.

**Certificate thumbprint**
```cs
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
```cs
public async Task<string> AcquireTokenWithSecretAsync()
{
    var clientAssertion = new ClientCredential("<Client ID>", "<Client secret>");
    var context = new AuthenticationContext("<Authority URL. Typically https://login.microsoftonline.com/[Directory_ID]>");
    var authenticationResult = await context.AcquireTokenAsync("<API endpoint>", clientAssertion);

    return authenticationResult.AccessToken;
}
```


Behind the scenes, the code above generates an HTTP request and receives a response like the following.

**Response**
```http
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


For more information, refer to the Azure documentation: 
- <a href="https://docs.microsoft.com/azure/architecture/multitenant-identity/client-assertion" target="_blank">Use client assertion to get access tokens from Azure AD</a>
- <a href="https://docs.microsoft.com/azure/architecture/multitenant-identity/token-cache" target="_blank">Cache access tokens</a>

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
For additional reference, view the <a href="https://go.microsoft.com/fwlink/?linkid=2085137" target="_blank">sample merchant app</a> and the accompanying developer documentation. The sample app provides an example of how to call Fraud Protection APIs in real time. The documentation for the sample app is linked to actual sample code whenever such links are possible. Otherwise, code samples exist directly in the documentation.

For guidance on configuring the sample site for your use, view <a href="https://go.microsoft.com/fwlink/?linkid=2100635" target="_blank">Configure the sample site</a>.
