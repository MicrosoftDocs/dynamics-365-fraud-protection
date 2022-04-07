---
author: jackwi111
description: This topic explains how to create Azure AD apps in Azure Portal or PowerShell for use with Dynamics 365 Fraud Protection.
ms.author: v-ydequadros
ms.date: 07/01/2019

ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Create Azure AD apps in Azure Portal or PowerShell 
---

# Create Azure AD apps in Azure Portal or PowerShell 

You can create Microsoft Azure Active Directory (Azure AD) apps within Microsoft Dynamics 365 Fraud Protection on the Real-time APIs page. For reference, see [Integrate Dynamics 365 Fraud Protection real-time APIs](integrate-real-time-api.md). If you want to set them up directly in the Azure portal, follow these steps to create an Azure AD app registration. 

## Create an Azure AD app registration in the Azure portal 

1. Open the [Azure portal](https://portal.azure.com).
2. In the main navigation, select **Azure Active Directory**. The **Microsoft – Overview** page appears. 
3. In the left pane of Overview, under **Manage**, select **App registrations**. The **Microsoft - App registrations** page appears. You can return to this page at any time to view your app registrations. 
4. Select **New registration**. The **Register an application** page appears. 
5. In the **Name** field, enter any name (for example, **API service account**). In the **Supported account types** field group, leave the **Accounts in this organizational directory only (\<your tenant name\>)** option selected. The Redirect (Web) URI is optional. It can be any URL that starts with **https://**. 

## Create an Azure AD app registration in PowerShell 
If you prefer to use Microsoft Windows PowerShell to create an Azure AD app registration, see [New-AzureRmADApplication](/powershell/module/azurerm.resources/new-azurermadapplication?preserve-view=true&view=azurermps-6.13.0). 

## Grant your Azure AD app access to the Fraud Protection real-time APIs 
For more information about how to configure API access to your Fraud Protection endpoint via the Azure portal, see [How to: Use the portal to create an Azure AD application and service principal that can access resources](/azure/active-directory/develop/howto-create-service-principal-portal). 

To assign the appropriate Dynamics 365 API role to your Azure AD app using PowerShell, use the [New-AzureADServiceAppRoleAssignment Windows PowerShell script](/powershell/module/azuread/new-azureadserviceapproleassignment?preserve-view=true&view=azureadps-2.0), as shown in the following example. 

```console
$c_app_name = "<your Azure AD application display name here>"

# Pick a role to assign; use Risk_API for production or Sandbox_Risk_API for sandbox (test) access.
$c_app_role_name = "API role here"

################################################################
# -- There is no need to change the script below this line. –- 
################################################################
$app_name = "Dynamics 365 Fraud Protection"
$sp = Get-AzureADServicePrincipal -Filter "displayName eq '$app_name'"

#Assign AppRole
$c_appRole = $sp.AppRoles | Where-Object { $_.DisplayName -eq $c_app_role_name }
$c_sp = Get-AzureADServicePrincipal -Filter "displayName eq '$c_app_name'"
New-AzureADServiceAppRoleAssignment -ObjectId $c_sp.ObjectId -PrincipalId $c_sp.ObjectId -ResourceId $sp.ObjectId -Id $c_appRole.Id 
```


[!INCLUDE[footer-include](includes/footer-banner.md)]
