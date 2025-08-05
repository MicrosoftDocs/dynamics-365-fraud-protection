---
author: josaw1
description: This article explains how to integrate Microsoft Dynamics 365 Fraud Protection real-time application programming interfaces (APIs).
ms.author: josaw
ms.date: 04/10/2024
ms.topic: how-to
search.audienceType:
  - admin
title: Integrate account protection APIs 
ms.custom: sfi-ga-nochange
---

# Integrate account protection APIs

[!include[deprecation](includes/deprecation.md)]

To take advantage of the full suite of features in Microsoft Dynamics 365 Fraud Protection, send your transaction data to the real-time application programming interfaces (APIs). In the evaluate experience, you can then analyze the results of using Fraud Protection. In the protect experience, you can also honor decisions that are based on the rules that you've configured.

Depending on how you choose to use Fraud Protection, you can use different **account protection APIs**. For example, *AccountCreation*, *AccountLogin*, *AccountCreationStatus*, *AccountLoginStatus*, *AccountUpdate*, and *Label*.

For information about all supported events, see [Dynamics 365 Fraud Protection API](https://go.microsoft.com/fwlink/?linkid=2084942).

## Set up

### Sign in

> [!IMPORTANT]
> To complete the initial API onboarding, you must be a Global Administrator in your Microsoft Azure tenant.

#### To sign in to Fraud Protection:

- Go to the [Fraud Protection portal](https://dfp.microsoft.com), sign in, and accept the terms and conditions if you're prompted to accept them.

    This step ensures that Fraud Protection is correctly configured in your Azure tenant. (You might already have completed this step during initial sign-up.)

### Create Microsoft Entra applications

> [!IMPORTANT]
> To complete this step, you must be an Application Administrator, a Cloud Application Administrator, or a Global Administrator in your Azure tenant.

To acquire the tokens that are required to call the APIs, you must use Microsoft Entra applications. You can configure these apps by using the **Real-time APIs** page in Fraud Protection.

#### To configure Microsoft Entra apps:

1. In the left navigation pane, select **Configuration**, and then select **Real-time APIs**. 

1. Fill in the fields to create your app. The following fields are required:

    - **Application display name** – Enter a descriptive name for your app. The maximum length is 93 characters.
    - **Environment** – Select the production endpoint.
    - **Authentication method** – Select whether a certificate or a secret (password) is used for authentication. If you select **Certificate**, select **Choose file** to upload the public key. When you acquire tokens, you will need the matching private key. If you select **Secret**, a password is generated for you after the app is created.

1. When you've finished filling in the fields, select **Create application**. 

    The confirmation page summarizes the app's name and ID, and either the certificate thumbprint or the secret, depending on the authentication method that you selected.

> [!IMPORTANT]
> Save the information about your certificate thumbprint or secret for future reference. The secret will be shown only one time.

You can create as many apps as you require to run API calls in your production environments.

#### To create another app:

1. Select **Create another application**. 
2. Fill in the fields to create your app, and then select **Create application**.

### Manage existing Microsoft Entra applications

After you've created your Microsoft Entra apps, you can manage them through the [Azure portal](https://portal.azure.com/#blade/Microsoft_Microsoft Entra ID_IAM/ActiveDirectoryMenuBlade/RegisteredApps). For more information, see the [Azure documentation site](/azure/active-directory/develop/active-directory-how-applications-are-added).


## Call the Fraud Protection real-time APIs

Use the information in this section to integrate your systems with Fraud Protection.

### Required IDs and information

- **API Endpoint** – The URI for your environment appears on the **Account information** tile on the Fraud Protection dashboard.
- **Directory (tenant) ID** – The directory ID is the globally unique identifier (GUID) for a tenant's domain in Azure. It appears in the Azure portal and on the **Account information** tile on the Fraud Protection dashboard.
- **Application (client) ID** – The application ID identifies the Microsoft Entra app that you created to call APIs. You can find this ID on the confirmation page that appears after you select **Create application** on the **Real-time APIs** page. You can also find it later, under **App registrations** in the Azure portal. There will be one ID for each app that you created.
- **Certificate thumbprint or secret** – You can find the certificate thumbprint or the secret on the confirmation page that appears after you select **Create application** on the **Real-time APIs** page.
- **Instance ID** - The instance ID is the globally unique identifier (GUID) for your environment in Fraud Protection. It appears in the **Integration** tile on the Fraud Protection dashboard.

### Generate an access token

You must generate this token and provide it with each API call. Note that access tokens have a limited lifespan. We recommend that you cache and reuse each access token until it's time to get a new access token.

The following C\# code samples provide examples that show how to acquire a token by using your certificate or secret. Replace the placeholders by using your own information.

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

**Response**

Behind the scenes, the preceding code generates an HTTP request and receives a response that resembles the following example.

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

For more information, see the Azure documentation:

- [Use client assertion to get access tokens from Microsoft Entra ID](/azure/architecture/multitenant-identity/client-assertion)
- [Cache access tokens](/azure/architecture/multitenant-identity/token-cache)

### Call the APIs

To call the APIs, follow these steps.

1. Pass the following required HTTP headers on each request.

    | Header name         | Header value |
    |---------------------|--------------|
    | Authorization       | Use the following format for this header: **Bearer *accesstoken***, where *accesstoken* is the token that is returned by Microsoft Entra ID. |
    | x-ms-correlation-id | Send a new GUID value on each set of API calls that are made together. |
    | x-ms-dfpenvid       | Send the GUID value of your Instance ID. |

2. Generate an event-based payload. Fill in the event data with the relevant information from your system. For information about all supported events, see [Dynamics 365 Fraud Protection API](https://go.microsoft.com/fwlink/?linkid=2084942).
3. Combine the header (which includes the access token) and the payload, and then send them to your Fraud Protection endpoint.

> [!NOTE]
> If you create a new environment, include the environment ID in the API header during integration, so that the transactions can be correctly routed. 

## View the sample app

For additional reference, view the [sample merchant app](https://go.microsoft.com/fwlink/?linkid=2085137) and see the accompanying developer documentation. The sample app provides an example that shows how to call Fraud Protection APIs in real time. The documentation for the sample app is linked to actual sample code whenever links are possible. Otherwise, code samples are included directly in the documentation.

For information about how to configure the sample site so that you can use it, see [Configure the sample site](https://go.microsoft.com/fwlink/?linkid=2100635).


[!INCLUDE[footer-include](includes/footer-banner.md)]
