---
author: jackwi111
description: This topic explains how to integrate Microsoft Dynamics 365 Fraud Protection real-time APIs.
ms.author: v-jowigh
ms.service: crm-online
ms.date: 08/07/2019

ms.topic: conceptual
title: Integrate Dynamics 365 Fraud Protection real-time APIs
---

# Integrate Dynamics 365 Fraud Protection real-time APIs

To take advantage of the full suite of Microsoft Dynamics 365 Fraud Protection features, send your transaction data to the real-time APIs. In the Evaluate experience, this allows you to analyze the results of using Dynamics 365 Fraud Protection. In the Protect experience, you can also honor decisions based on the model operating points you have configured.

## Create Azure Active Directory applications

To acquire the tokens required to call the Dynamics 365 Fraud Protection APIs, your services will utilize Microsoft Azure Active Directory (Azure AD) applications. You can configure these by using the Real-time APIs tool, which leads you through the required steps. Or, you can [manually configure your Azure AD applications](azure-apps-portal-powershell.md). Note that to complete the process successfully, you must have the proper administrative privileges in your Azure tenant (Application Administrator, Cloud Application Administrator, or Global Administrator).

To use the Real-time APIs tool, select **Configuration** in the left-hand navigation, and then select **Real-time APIs**. Complete the form to create your app. We recommend creating one Azure AD application for each environment you operate. 

The following fields are required: 

- **Application display name**. Give your application a descriptive name. Maximum length is 93 characters. 
- **Environment**. Choose whether this application should call your production or integration (sandbox) endpoint. 
- **Authentication method**. Choose whether you would like to authenticate via certificate or a secret (password). For the certificate method, use the **Choose file** button to upload the public key. You will need the matching private key when you acquire tokens. If you choose the **Secret** method, a password will be generated for you after application creation. 

When you finish filling in the fields, select **Create application**. The confirmation screen summarizes your app's name, ID, and the certificate thumbprint or secret, depending on your authentication method. 

> [!IMPORTANT]
> If you chose the secret method, please save the information for future reference, because it will only be displayed once.

To create an additional app, select **Create another application**. You can create as many apps as necessary to run API calls in each of your environments. 

### Manage existing Azure AD applications 
Once you have created your Azure AD apps, you can manage them through the Azure portal. You can learn more about the tool from the [Azure documentation site](https://docs.microsoft.com/azure/azure-portal/). 

While using Dynamics 365 Fraud Protection, you can link to the Azure portal from the **Real-time APIs** page's Tips & help column by selecting **Visit the Azure portal**. 

## Call the Dynamics 365 Fraud Protection real-time APIs 
To integrate your systems with Dynamics 365 Fraud Protection, follow these steps. 

### Get your IDs 
The following IDs are required: 
- **Directory (tenant) ID**. The Directory ID is the globally unique identifier (GUID) for a tenant's domain in Azure. It appears in the Azure portal and on the **Account information** tile on the Dynamics 365 Fraud Protection dashboard. 
- **Application (client) ID**. This identifies the Azure AD app you created for calling APIs. Get the ID from the **Real-time APIs** confirmation screen or find it later in the Azure portal under **App registrations**. There will be one ID for each app you created.

### Identify your environment
You can find the API URIs for the sandbox and production environments on the **Account information** tile on the Dynamics 365 Fraud Protection dashboard or as printed below: 
- Sandbox: https://api.dfp.microsoft-int.com 
- Production: https://api.dfp.microsoft.com

### Authenticate with your environment
To begin using the sandbox or production APIs, be sure you have visited each environment's portal, signed in, and accepted the terms and conditions.
- Sandbox: https://dfp.microsoft-int.com 
- Production: https://dfp.microsoft.com (You might already have completed this step in production during initial sign-up.)

### Generate an access token
You must generate this token and provide it dynamically. Note that access tokens have a limited lifespan. We recommend that you cache it and reuse it until it's time to get a new access token. 

For more information, please refer to the Azure documentation: 
- [Use client assertion to get access tokens from Azure AD](https://docs.microsoft.com/azure/architecture/multitenant-identity/client-assertion)
- [Cache access tokens](https://docs.microsoft.com/en-us/azure/architecture/multitenant-identity/token-cache)

### Call the APIs
When calling the APIs, follow these steps.

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
   <li>Combine the header (which includes the access token) and the payload, and send them to your Dynamics 365 Fraud Protection endpoint.</li>
</ol>


## View the sample app 
For additional reference, view the [sample merchant app](https://go.microsoft.com/fwlink/?linkid=2085137) and the accompanying developer documentation. The sample app provides an example of how to call Dynamics 365 Fraud Protection APIs, including API events like sending customer account updates, refunds, and chargebacks in real time. The documentation for the sample app is linked to actual sample code whenever such links are possible. Otherwise, code samples exist directly in the documentation. 
