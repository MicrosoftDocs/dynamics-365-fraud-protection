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

To enable your apps to access Dynamics 365 Fraud Protection APIs in your tenant, you must set up service-to-service API access and service-to-service roles.

[!NOTE] Sandbox (test) and production (live) versions are available.
    
1. To access Dynamics 365 Fraud Protection sandbox APIs, assign the Sandbox Risk_API role to the Azure AD app (you previously created) in the Dynamics 365 Fraud Protection sandbox environment.

|App role   |Description   |Rights   |
|---|---|---|
|Sandbox_Risk_API   |Enables access to the Production Risk APIs.   |A{PI access   |

To access Dynamics 365 Fraud Protection production APIs, assign the Risk API role to the Azure AD appl (you previously created) in the Dynamics 365 Fraud Protection production environment.

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

1. Get your ID(s): TenantID, AppID, ClientID, InstanceID?
1. To generate an access token, see [Use client assertion to get access tokens from Azure AD](https://docs.microsoft.com/azure/architecture/multitenant-identity/client-assertion).

[!NOTE]   You must generate this token and provide it dynamically as it expires every x hours.

![integrate TenantID](media/integrate-apis-images/tenantID.png)

1.	When calling Dynamics 365 Fraud Protection APIs, you must pass required HTTP headers on each request, as follows.

| Header name  |Header value   |
|---|---|
|Authorization   |To obtain an access token, use the Azure AD App (configured for you when you signed up and registered for Dynamics 365 Fraud Protection).

[!Note]   The access token will have a limited lifespan. We recommend that you cache it and re-use it until it is time to get a new one.

Format for this header (replace *token* with the actual token value):

- Access *token*|
|x-ms-correlation-id   |Send a new GUID value on each set of API calls that are made together.   |

1.	Generate an event-based payload. Populate the event data with the relevant information from your transactional system. All supported events are documented here [Dynamics 365 Fraud Protection API](https://go.microsoft.com/fwlink/?linkid=2084942).
1.	Combine the access token + header + payload, and send it to your specific Dynamics 365 Fraud Protection endpoint.
1.	In the Dynamics 365 Fraud Protection Evaluate experience, you can send over transactions and analyze the results from Dynamics 365 Fraud Protection.
1.	In the Dynamics 365 Fraud Protection Protect experience, you can send over transactions and honor decisions based on your configured rules.


