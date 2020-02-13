---
author: v-davido
description: This topic explains how to integrate Microsoft Dynamics 365 Fraud Protection real-time APIs.

ms.author: v-davido
ms.service: fraud-protection
ms.date: 01/14/2020
ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Integrate Dynamics 365 Fraud Protection real-time APIs


---

# Integrate Dynamics 365 Fraud Protection real-time APIs


To take advantage of the full suite of Microsoft Dynamics 365 Fraud Protection features, send your transaction data to the real-time APIs. In the *Evaluate* experience, this allows you to analyze the results of using Dynamics 365 Fraud Protection. In the *Protect* experience, you can also honor decisions based on the rules you have configured.

Depending on how you choose to use Dynamics 365 Fraud Protection, you may make use of different sets of APIs, as seen below: 

- **Purchase protection APIs**: Purchase, PurchaseStatus, BankEvent, Chargeback, Refund, UpdateAccount, Label
- **Account protection APIs**: SignUp, SignUpStatus, Label

For documentation about all supported events, see <a href="https://go.microsoft.com/fwlink/?linkid=2084942" target="_blank">Dynamics 365 Fraud Protection API</a>.


## Get set up

### Sign in
> [!IMPORTANT]
> You must be a Global Administrator in your Microsoft Azure tenant to complete the initial sign-in.

Visit the portal for each environment you intend to use, sign in, and accept the terms and conditions if prompted.
- Sandbox - <a href="https://dfp.microsoft-int.com" target="_blank">https://dfp.microsoft-int.com</a> 
- Production - <a href="https://dfp.microsoft.com" target="_blank">https://dfp.microsoft.com</a> (You might already have completed this step in production during initial sign-up.)

### Create Azure Active Directory applications
> [!IMPORTANT]
> You must be an Application Administrator, Cloud Application Administrator, or Global Administrator in your Azure tenant to complete this step.

To acquire the tokens required to call the APIs, you will need to utilize Azure Active Directory (Azure AD) applications. You can configure these by using the **Real-time APIs** page in Dynamics 365 Fraud Protection.

Select **Configuration** in the left navigation pane, and then select **Real-time APIs**. Complete the form to create your app. We recommend creating one Azure AD application for each environment that you operate. 

The following fields are required: 
- **Application display name** - Give your application a descriptive name. Maximum length is 93 characters. 
- **Environment** - Choose whether this application should call your production or integration (sandbox) endpoint. 
- **Authentication method** - Choose whether you would like to authenticate via certificate or a secret (password). For the certificate method, use the **Choose file** button to upload the public key. You will need the matching private key when you acquire tokens. If you select the **Secret** method, a password will be generated for you after application creation.

When you finish filling in the fields, select **Create application**. The confirmation screen summarizes your app's name, ID, and the certificate thumbprint or secret, depending on your authentication method. 

> [!IMPORTANT]
> Please save your secret or certificate thumbprint information for future reference. The secret will only be displayed once.

To create an additional application, select **Create another application**. You can create as many apps as necessary to run API calls in each of your environments. 

### Manage existing Azure AD applications 
After you have created your Azure AD apps, you can manage them through the <a href="https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps" target="_blank">Azure portal</a>. You can learn more from the <a href="https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added" target="_blank">Azure documentation site</a>. 

### Manually configure Azure AD applications
If you would like to set up your applications directly in Azure, see [Create Azure AD apps in Azure Portal or PowerShell](azure-apps-portal-powershell.md).

## Call the Dynamics 365 Fraud Protection real-time APIs 
To integrate your systems with Dynamics 365 Fraud Protection, follow these steps.

### Required IDs and information
- **Environment URI** - The URIs for your sandbox or production environment appear on the **Account information** tile on the Dynamics 365 Fraud Protection dashboard.
- **Directory (tenant) ID** - The Directory ID is the globally unique identifier (GUID) for a tenant's domain in Azure. It appears in the Azure portal and on the **Account information** tile on the Dynamics 365 Fraud Protection dashboard. 
- **Application (client) ID** - This identifies the Azure AD app you created for calling APIs. Get the ID from the **Real-time APIs** confirmation screen or find it later in the Azure portal under **App registrations**. There will be one ID for each app you created.
- **Certificate thumbprint or secret** - Get the thumbprint or secret from the Real-time APIs confirmation screen.

### Generate an access token
You must generate an Azure AD access token and provide it with each DFP API call. Note that access tokens have a limited lifespan. We recommend that you cache and reuse the token until it gets close to expiring, at which time you can get a new access token.
The following C# code samples provide examples of acquiring a token with your certificate or secret. Replace the placeholders with your specific information.
For both of these C# samples, you will need to import the following [Microsoft.Identity.Client NuGet package](https://www.nuget.org/packages/Microsoft.Identity.Client/).

For samples in other languages, see https://aka.ms/aaddev. 

**Certificate thumbprint**
```cs
public async Task<string> acquireTokenWithCertificate(string tenantId, string clientId, string certPath, string password)
{
  // tenantId: Directory (tenant ID)
  // clientId: Application (client) ID
  // certPath: path to the certificate file (pfx) used to authenticate your application to AAD
  // password: password for access to the certificate file's private key

	X509Certificate2 certificate = new X509Certificate2(certFilePath,certPassword);
	
	var app = ConfidentialClientApplicationBuilder.Create(clientId)
		   .WithAuthority(AzureCloudInstance.AzurePublic, new Guid(tenantId))
		   .WithCertificate(certificate)
		   .Build();

	string[] scopes = new string[] { "<API endpoint for INT or PROD>; should be https://api.dfp.microsoft-int.com/.default or https://api.dfp.microsoft.com/.default" };

	AuthenticationResult result = null;
	try
	{
		result = await app.AcquireTokenForClient(scopes)
						  .ExecuteAsync();
	}
	catch (MsalServiceException ex)
	{
		// Catches authentication exceptions
	}

	return result.AccessToken;
}
```

**Secret**
```cs
public async Task<string> acquireTokenWithSecret(string tenantId, string clientId, string clientSecret)
{
  // tenantId: Directory (tenant ID)
  // clientId: Application (client) ID
  // clientSecret: Symmetric key used to authenticate your application to AAD

	var app = ConfidentialClientApplicationBuilder.Create(clientId)
			.WithAuthority(AzureCloudInstance.AzurePublic, new Guid(tenantId))
			.WithClientSecret(clientSecret)
			.Build();

	string[] scopes = new string[] { "<API endpoint for INT or PROD>; should be https://api.dfp.microsoft-int.com/.default or https://api.dfp.microsoft.com/.default" };

	AuthenticationResult result = null;
	try
	{
		result = await app.AcquireTokenForClient(scopes)
					  .ExecuteAsync();
	}
	catch (MsalServiceException ex)
	{
		// Catches authentication exceptions
	}

	return result.AccessToken;
}
```
The AuthenticationResult object in each case contains the AccessToken itself, and an ExpiresOn property which indicates when the token will become invalid. 

For more information, refer to the Azure documentation: 
- <a href="https://docs.microsoft.com/azure/active-directory/develop/msal-overview" target="_blank">Overview of Microsoft Authentication Library (MSAL)</a>
- <a href="https://docs.microsoft.com/azure/active-directory/develop/msal-acquire-cache-tokens" target="_blank">Acquire and cache tokens using the Microsoft authentication library (MSAL)</a>

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
   <li>Combine the header (which includes the access token) and the payload, and then send them to your Dynamics 365 Fraud Protection endpoint.</li>
</ol>


## View the sample app 
For additional reference, view the <a href="https://go.microsoft.com/fwlink/?linkid=2085137" target="_blank">sample merchant app</a> and the accompanying developer documentation. The sample app provides an example of how to call Dynamics 365 Fraud Protection APIs, including API events like sending customer account updates, refunds, and chargebacks in real time. The documentation for the sample app is linked to actual sample code whenever such links are possible. Otherwise, code samples exist directly in the documentation.

For guidance on configuring the sample site for your use, view <a href="https://go.microsoft.com/fwlink/?linkid=2100635" target="_blank">Configure the sample site</a>.

