---
author: yvonnedeq
description: This topic explains how to configure user access to Microsoft Dynamics 365 Fraud Protection.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 04/02/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Configure user access to Dynamics 365 Fraud Protection

---


# Configure user access to Dynamics 365 Fraud Protection

Microsoft Dynamics 365 Fraud Protection (Fraud Protection) allows you to grant users various levels of access to the tool based on logical or functional roles. Administrators can use the User access section to assign these roles.

## Assign roles 

The administrator who is defined in your Azure tenant sets up the initial user and role configuration. 

### Assign roles to existing users or groups of your tenant
- In the left navigation, select **Settings**, and then select **User access**. 

### Grant access to a user or group in this environment
1. Select **Assign role**. 
1. Enter the name or company email address of the person or group that you want to edit. 

    If the name is recognized as a member of your Azure tenant, it will be resolved, and the full name will be shown. 

1. Select the name to continue. 

### Assign a specific role to the user
1. In the **Roles** field, select one or more of the defined roles. 
1. Select **Assign role** to create the user. 

### Edit or delete existing users
- Select the user name in the **Member** list, and then select **Edit** or **Remove**. 

In this section, roles can be added to or deleted from a member. Note that, if you edit your own account (for example, if you delete your own administrative role), those edits might interfere with your ability to use some features of Fraud Protection. If you must restore permissions, you can reset them in the [Azure portal](https://portal.azure.com/#home). 

To learn more about the available roles, see the "Dynamics 365 Fraud Protection roles" section of this document. 

### User management in your Azure tenant 

Users and roles can also be managed through the Azure portal. For information about how to grant access to users via the Azure portal, see [Assign a user or group to an enterprise app in Azure Active Directory](/azure/active-directory/manage-apps/assign-user-or-group-access-portal). For information about how to add users to Azure AD or delete users from Azure AD, see [Add or delete users using Azure Active Directory](/azure/active-directory/fundamentals/add-users-azure-active-directory). 

## Dynamics 365 Fraud Protection roles 

Fraud Protection offers a defined set of user roles, each of which has access to specific features and functions. You can select these when assigning a user to the system. 

All roles listed here are named as they would be in your production environment. To grant users access to these roles in your sandbox environment, choose the version of the role that begins with "Sandbox_" (for example, "Sandbox_AllAreas_Admin"). 

### AllAreas_Admin 
High-level administrative account. Full access to Dynamics 365 Fraud Protection. 

### AllAreasEditor 
Power user. Can see all areas and has permissions to use key Dynamics 365 Fraud Protection tools. 
- **Write**: Data upload, Rules, Virtual fraud analyst, Lists, Subject requests 
- **Read**: Diagnostic reports, Support tool, Scorecard, Metrics, Ontology, Graph explorer, API configuration, Metering, Monitoring, Permissions, Transaction acceptance booster 

### AllAreasViewer 
Can view all areas of Dynamics 365 Fraud Protection and learn from the data. Will not be able to make uploads or change settings. 
- **Write**: None 
- **Read**: All areas 

### SupportAgent 
Tailored access to Dynamics 365 Fraud Protection for support agents working with your customers. Can view and work within the support tool, see the ontology, and assign customers to safe or block lists. 
- **Write**: Support lists 
- **Read**: Lists, Support tool, Ontology 
- **No access**: All other areas. Pages may be accessible in the navigation but cannot be used in full. 

### FraudEngineer 
Tailored access for fraud analysts and engineers in your organization working with Dynamics 365 Fraud Protection. Has similar access to the AllAreasEditor and provides access to the data engineering information, but does not have access to certain configuration options. 
- **Write**: Data upload, Rules, Virtual fraud analyst, Lists, Subject requests 
- **Read**: Diagnostic reports, Support tool, Scorecard, Metrics, Ontology, Graph explorer 
- **No access**: API configuration, Metering, Monitoring, Permissions, Transaction acceptance booster. Pages may be accessible in the navigation but cannot be used in full. 

### Risk_API
Grants API access. Provides no access to the user-facing tool. 


[!INCLUDE[footer-include](includes/footer-banner.md)]
