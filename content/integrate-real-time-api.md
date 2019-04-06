---
author: jackwi111
description: Integrate Dynamics 365 Fraud Protection real-time APIs
ms.author: v-jowigh
ms.date: 03/01/2019
ms.service:
 - d365-fraud-protection
ms.topic: conceptual
title: Integrate Dynamics 365 Fraud Protection real-time APIs
---

# Integrate Dynamics 365 Fraud Protection real-time APIs

To securely integrate your existing systems with the real-time Dynamics 365 Fraud Protection APIs, follow these steps to:

- Create an app in the Azure portal to provide an access token within your tenant which enables access to your Dynamics 365 Fraud Protection API endpoints.

- Call the Dynamic 365 Fraud Protection real-time APIs.

## Create an app in the Azure portal

To configure API access to your Dynamics 365 Fraud Protection endpoint via the Azure portal, see [How to: Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal).

1.	Open Azure portal.
1.	Open **Azure Active Directory**.
1.	Select **Manage>App registrations (preview)**.
1.	Select **New Registration**.
1.	Provide a name. Leave the **Account Type** at **Accounts in this organizational directory ONLY (<your_tenant_name>)**. The **Web URI** is optional [can be any https://].

## Add app to the Dynamics 365 app role and configure your credentials

To enable your apps to access Dynamics 365 Fraud Protection APIs in your tenant, you must set up service-to-service API access and service-to-service roles. Both the sandbox (test) and production (live) versions are available.

To access Dynamics 365 Fraud Protection sandbox APIs, assign the Sandbox Risk_API role to the Azure AD app (you previously created) in the Dynamics 365 Fraud Protection sandbox environment.

|App role   |Description   |Rights   |
|---|---|---|
|Sandbox_Risk_API   |Enables access to the Sandbox Risk APIs.   |API access   |
      
To access Dynamics 365 Fraud Protection production APIs, assign the Risk API role to the Azure AD app (you previously created) in the Dynamics 365 Fraud Protection production environment.
        
|App role   |Description   |Rights   |
|---|---|---|
|Risk_API   |Enables access to the Production Risk APIs.   |API access   |

## Assign Azure AD app access using PowerShell

The following sample PowerShell script assigns your Azure AD app access to one of these Dynamics 365 Fraud Protection API roles:

```# Enter merchant app name
# Enter merchant app name
$c_app_name = "your Azure AD application display name here"

# Pick an Application AppRole to assign
$c_app_role_name = "Risk_API"

# Get 1st Party App with AppRoles
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
    <li>Get your ID:
      <ul><li>TenantID: Obtain it from the Azure portal. It is the GUID for a tenant's domain in Azure. It appears on the <b>Account Information</b> tile on the Dynamics 365 Fraud Protection dashboard. See the following screenshot for location.</li>
            <li>Sandbox Resource URI or Production Resource URI: First-party app ID that appears on the <b>Account Information</b> tile on the Dynamics 365 Fraud Protection dashboard.</li>
            <li>Azure AD ClientID: To create this ID, see <i>Create an app in the Azure portal</i> in this topic. In the Azure portal, this ID is known as the Azure AD Application ID.</li>
            <li>InstanceID: Your ID for using [device fingerprinting](https://go.microsoft.com/fwlink/?linkid=2085697). This ID identifies the instance of Dynamics 365 Fraud Protection that you will enter data. It appears on the <b>Account Information</b> tile on the Dynamics 365 Fraud Protection dashboard.<br/>
            <img src="media/integrate-apis-images/tenantID.png" alt="integrate TenantID" title="integrate TenantID" />
            </li>
      </ul>
    </li>
    <li>
        To generate an access token, see <a href="https://docs.microsoft.com/azure/architecture/multitenant-identity/client-assertion">Use client assertion to get access tokens from Azure AD</a>.
        <div class="alert">
            <p class="alert-title"><span class="docon docon-status-error-outline"></span> <b>Note</b></p>
            <p>You must generate this token and provide it dynamically. See <a href="https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-configurable-token-lifetimes#configurable-token-lifetime-properties">Configure lifetime tokens</a>.</p>
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
                    To obtain an access token, use the Azure AD app. For instructions, see [How to: Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal).<br /><br />
                    <b>Note</b> The access token will have a limited lifespan. We recommend that you cache it and re-use it until it is time to get a new one.<br /><br />
                    Format for this header (replace <i>token</i> with the actual token value):<br />
                    <ul><li> Access <i>token</i></li></ul>
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
