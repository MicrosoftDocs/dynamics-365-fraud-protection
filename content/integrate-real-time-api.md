# Integrate Dynamics 365 Fraud Protection real-time APIs

Follow these steps to create an app in the Azure portal to integrate with the Dynamics 365 Fraud Protection [real-time event APIs](real-time-api.md).

1.	To create an app:

   a.	Open Azure portal.
  
   b.	Open Azure Active Directory.
  
   c.	Select **Manage>App registrations (preview)**.
  
   d.	Select **New Registration.**
  
   e.	Provide a name. Leave the Account Type at Accounts in this organizational directory ONLY (<tenant_name>). The Web URI is optional [can be any https://].
  
2.	Add this app to the Dynamics 365 app role and configure your app secret/credentials.

   a.	To enable your apps to access Dynamics 365 Fraud Protection APIs, you must set up service-to-service API access and service-to-service roles.
  
      i.	Production and Sandbox versions are available.
    
  To access Dynamics 365 Fraud Protection production APIs, assign an API role to an Azure AD application in the Dynamics 365 Fraud Protection production environment.

|Security Group   |App role   |Description   |Rights   |Authentication method   |
|---|---|---|---|---|
|Risk APIs   |Risk_API   |Enables access to the Production Risk APIs.   |?   |Azure AD Users and Groups   |

To access Dynamics 365 Fraud Protection sandbox APIs, assign an API role to an Azure AD application in the Dynamics 365 Fraud Protection sandbox environment.

|Security Group   |App role   |Description   |Rights   |Authentication method   |
|---|---|---|---|---|
|Sandbox Risk APIs   |Sandbox_Risk_API   |Enables access to the Production Risk APIs.   |?   |Azure AD Users and Groups   |

3.	To manually add user service-to-service API access  via the Azure portal, see [How to: Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal).

a.	The following sample PowerShell script assigns your Azure AD app access to one of these Dynamics 365 Fraud Protection API roles:

```# Enter merchant app name
# Enter merchant app name
$c_app_name = "your Azure AD application display name here"

# Pick an Application AppRole to assign
$c_app_role_name = "Risk_API"

#Get 1st Party App with AppRoles
$app_name = "Dynamics 365 Fraud Protection"
$sp = Get-AzureADServicePrincipal -Filter "displayName eq '$app_name'"

#Assign AppRole
$c_appRole = $sp.AppRoles | Where-Object { $_.DisplayName -eq $c_app_role_name }
$c_sp = Get-AzureADServicePrincipal -Filter "displayName eq '$c_app_name'"
New-AzureADServiceAppRoleAssignment -ObjectId $c_sp.ObjectId -PrincipalId $c_sp.ObjectId -ResourceId $sp.ObjectId -Id $c_appRole.Id```


To obtain real-time fraud protection by integrating your transactional sales systems with a simple event-based call to Dynamics 365 Fraud Protection, follow these instructions.


1. Get your ID(s)   [TBD: where is this?] TenantID, AppID, ClientID, InstanceID?
2. To generate a token, see [Use client assertion to get access tokens from Azure AD](https://docs.microsoft.com/en-us/azure/architecture/multitenant-identity/client-assertion).

[!NOTE]   You must generate this token and provide it dynamically as it expires every x hours.








