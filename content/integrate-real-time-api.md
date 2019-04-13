---
author: jackwi111
description: Integrate Dynamics 365 Fraud Protection real-time APIs
ms.author: v-jowigh
ms.date: 03/01/2019
ms.service:
- crm-online
ms.topic: conceptual
title: Integrate Dynamics 365 Fraud Protection real-time APIs
---

# Integrate Dynamics 365 Fraud Protection real-time APIs

To securely integrate your existing systems with the real-time Dynamics 365 Fraud Protection APIs, follow these steps to:

- Create an app registration in the Azure portal, and use it to acquire an access token to your Dynamics 365 Fraud Protection API endpoints.

- Call the Dynamic 365 Fraud Protection real-time APIs.

## Create an Azure AD App registration in the Azure portal 

Follow these steps to create an Azure Active Directory App registration in the Azure portal.

1. Open the [Microsoft Azure portal](https://portal.azure.com).
1. Open **Azure Active Directory**.
1. Select **Manage>App registrations (preview)**. You can always return to this page to view your app registrations.
1. Select **New Registration**.
1. Provide any name (for example, API service account). Leave **Supported account types** at **Accounts in this organizational directory ONLY (<your_tenant_name>)**. The **Web URI** is optional [can be any https://].

For more information about configuring API access to your Dynamics 365 Fraud Protection endpoint via the Azure portal, see [How to: Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal).

Alternatively, if you prefer to use PowerShell, see the following instructions to [create an Azure AD App registration]( https://docs.microsoft.com/en-us/powershell/module/azurerm.resources/new-azurermadapplication?view=azurermps-6.13.0).

## Grant your Azure AD App access to the Dynamic 365 Fraud Protection real-time APIs

To assign the appropriate Dynamics 365 API role to your Azure AD Application, use the [PowerShell script](https://docs.microsoft.com/en-us/powershell/module/azuread/new-azureadserviceapproleassignment?view=azureadps-2.0), as shown in the following example.

Replace the *italicized* text with your Azure AD app name and the appropriate role name, as noted inline in the following script.

```$c_app_name = "your Azure AD application display name here"

# Pick a role to assign; use Risk_API for production or Sandbox_Risk_API for sandbox (test) access.
$c_app_role_name = "API role here"

################################################################
# -- there is no need to change the script below this line –- 
################################################################
$app_name = "Dynamics 365 Fraud Protection"
$sp = Get-AzureADServicePrincipal -Filter "displayName eq '$app_name'"

#Assign AppRole
$c_appRole = $sp.AppRoles | Where-Object { $_.DisplayName -eq $c_app_role_name }
$c_sp = Get-AzureADServicePrincipal -Filter "displayName eq '$c_app_name'"
New-AzureADServiceAppRoleAssignment -ObjectId $c_sp.ObjectId -PrincipalId $c_sp.ObjectId -ResourceId $sp.ObjectId -Id $c_appRole.Id 
```

## Call the Dynamic 365 Fraud Protection real-time APIs

To obtain real-time fraud protection by integrating your transactional sales systems with Dynamics 365 Fraud Protection using an event-based call, follow these instructions.

<ol>
    <li>Get your IDs:
      <ul><li>Directory (tenant) ID: Obtain it from the Azure portal. It is the GUID for a tenant's domain in Azure. It appears on the <b>Account Information</b> tile on the Dynamics 365 Fraud Protection dashboard. See the following screenshot for location.</li>
            <img src="media/integrate-apis-images/tenantID.png" alt="integrate TenantID" title="integrate TenantID" />
            <li>Sandbox Resource URI or Production Resource URI: First-party app ID that appears on the <b>Account Information</b> tile on the Dynamics 365 Fraud Protection dashboard.</li>
            <ul><li>[Sandbox]: (https://api.dfp.microsoft-int.com)</li>
                  <li>[Production]: (https://api.dfp.microsoft.com)</li></ul> 
            <li>Application (client) ID: To create this ID, see <i>Create an app in the Azure portal</i> in this topic. In the Azure portal, this ID is known as the Application (client) ID. To find this Application ID in Azure AD, select <b>App registrations (Preview)</b>.</li>
            <li>InstanceID: Your ID for using [device fingerprinting](https://go.microsoft.com/fwlink/?linkid=2085697). This ID identifies the instance of Dynamics 365 Fraud Protection that you will enter data. It appears on the <b>Account Information</b> tile on the Dynamics 365 Fraud Protection dashboard.<br/>
            
            </li>
      </ul>
    </li>
    <li>
        To generate an access token, see <a href="https://docs.microsoft.com/azure/architecture/multitenant-identity/client-assertion">Use client assertion to get access tokens from Azure AD</a>.
        <div class="alert">
            <p class="alert-title"><span class="docon docon-status-error-outline"></span> <b>Note</b></p>
            <p>You must generate this token and provide it dynamically. See <a href="https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-configurable-token-lifetimes#configurable-token-lifetime-properties">Configure token lifetimes</a>.</p>
        </div><br/>
    </li>
    <li>
        When calling Dynamics 365 Fraud Protection APIs, you must pass required HTTP headers on each request, as follows.
        <table>
            <tr>
                <th>Header name</th>
                <th>Header value</th>
            </tr>
            <tr>
                <td>Authorization</td>
                <td>
                    To obtain an access token, use the Azure AD app. <br /><br />
                    <b>Note</b> The access token will have a limited lifespan. We recommend that you cache it and re-use it until it is time to get a new one.<br /><br />
                    Format for this header (replace <i>accesstoken</i> with the actual token value):<br />
                    <ul><li> Bearer <i>accesstoken</i> where acccesstoken is the token returned by Azure Active Directory.</li></ul>
                </td>
            </tr>
            <tr>
                <td>x-ms-correlation-id</td>
                <td>Send a new GUID value on each set of API calls that are made together.</td>
            </tr>
        </table>
    </li>
    <li>Generate an event-based payload. Populate the event data with the relevant information from your transactional system. All supported events are documented here <a href="https://go.microsoft.com/fwlink/?linkid=2084942">Dynamics 365 Fraud Protection API</a>.</li>
    <li>Combine the header (that includes the access token) and payload, and send it to your specific Dynamics 365 Fraud Protection endpoint.</li>
    <li>In the Dynamics 365 Fraud Protection Evaluate experience, you can send over transactions and analyze the results from Dynamics 365 Fraud Protection.</li>
    <li>In the Dynamics 365 Fraud Protection Protect experience, you can send over transactions and honor decisions based on your configured rules.</li>
</ol>

For additional information about access tokens, see [How to: Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal).

## Add app to the Dynamics 365 app role and configure your credentials

To enable your apps to access Dynamics 365 Fraud Protection APIs in your tenant, you must set up service-to-service API access and service-to-service roles. Both the sandbox (test) and production (live) versions are available.

To access Dynamics 365 Fraud Protection sandbox APIs, assign the Sandbox Risk_API role to the Azure AD app (you previously created - see Create an app registration in the Azure portal in this topic) in the Dynamics 365 Fraud Protection sandbox environment.

|App role   |Description   |Rights   |
|---|---|---|
|Sandbox_Risk_API   |Enables access to the Sandbox Risk APIs.   |API access   |
      
To access Dynamics 365 Fraud Protection production APIs, assign the Risk API role to the Azure AD app (you previously created - see Create an app registration in the Azure portal in this topic) in the Dynamics 365 Fraud Protection production environment.
        
|App role   |Description   |Rights   |
|---|---|---|
|Risk_API   |Enables access to the Production Risk APIs.   |API access   |


