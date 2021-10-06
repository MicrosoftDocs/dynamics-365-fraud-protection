---
author: josaw1
description: This topic explains how to configure user access to Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 10/05/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Configure user access

---


# Configure user access

Microsoft Dynamics 365 Fraud Protection enables you to grant users various levels of access to the tool based on logical or functional roles. Administrators can use the **User access** section to assign these roles.

## Assign roles 

The administrator who is defined in your Azure tenant sets up the initial user and role configuration. For information about how to add users to Azure Active Directory, see [Create a user account in Azure Active Directory](/azure/active-directory/manage-apps/add-application-portal-assign-users#create-a-user-account).

### Assign roles to existing users or groups of your tenant in Fraud Protection
1. In the left navigation pane, select **Settings**, and then select **User access**. 
1. Select **Assign role**. 
1. Enter the name or company email address of the person or group that you want to edit. 

    If the name is recognized as a member of your Azure tenant, the name will resolve, and the full name will be shown. 

1. Select the name to continue. 
1. In the **Roles** field, select one or more of the defined roles. 
1. Select **Assign role** to create the user. 

### Edit or delete existing users
1. To edit or delete a user, select the user name in the **Member** list, and then select **Edit** or **Remove**. 

   On this part of the page, roles can be added to or deleted from a member. If you edit your own account (for example, if you delete your own administrative role), your edits may interfere with your ability to use some features of Fraud Protection. If you must restore permissions, you can reset them in the [Azure portal](https://portal.azure.com/#home). 

To learn more about the available roles, see the [Fraud Protection roles](configure-user-access.md#Roles) section of this topic. 

### User management in your Azure tenant 

Users and roles can also be managed through the Azure portal. For information about how to grant access to users through the Azure portal, see [Assign a user account to an enterprise application](/azure/active-directory/manage-apps/add-application-portal-assign-users#assign-a-user-account-to-an-enterprise-application). 

## Roles

Fraud Protection offers a defined set of user roles, each of which has access to specific features and functions. You can select roles when you assign a user to the system. 

All roles listed below are named as they will be in your production environment. To grant users access to these roles in your sandbox environment, choose the version of the role that begins with "Sandbox_" (for example, "Sandbox_AllAreas_Admin"). 

- **AllAreas_Admin** - This is a high-level administrative account that has full access to Fraud Protection. 

- **AllAreasEditor** - This is a power user who can view all areas and has permissions to use key Fraud Protection tools. 
  - **Write**: Data upload, rules, virtual fraud analyst, lists, subject requests. 
  - **Read**: Diagnostic reports, support tool, scorecard, metrics, ontology, graph explorer, API configuration, metering, monitoring, permissions, transaction acceptance booster.

- **AllAreasViewer** - This role can view all areas of Fraud Protection and learn from the data. The user with this role will not be able to make uploads or change settings. 
  - **Write**: None.
  - **Read**: All areas. 

- **SupportAgent** - This role provides tailored access to Fraud Protection for support agents working with your customers. The user with this role can view and work within the support tool, see the ontology, and assign customers to safe or block lists. 
  - **Write**: Support lists.
  - **Read**: Lists, support tool, ontology 
  - **No access**: All other areas. Pages may be accessible in the navigation but can't be used in full. 

- **FraudEngineer** - This role provides tailored access for fraud analysts and engineers in your organization working with Fraud Protection. The user with this role has similar access to the **AllAreasEditor** and can access the data engineering information, but does not have access to certain configuration options. 
  - **Write**: Data upload, rules, virtual fraud analyst, lists, subject requests.
  - **Read**: Diagnostic reports, support tool, scorecard, metrics, ontology, graph explorer. 
  - **No access**: API configuration, metering, monitoring, permissions, transaction acceptance booster. Pages may be accessible in the navigation but can't be used in full. 

- **Risk_API** - This role grants access to the API, but does not provide access to the user-facing tool. 

## Additional resources

[User roles and access (PSPs)](psp-user-roles.md)

[!INCLUDE[footer-include](includes/footer-banner.md)]
