---
author: v-davido
description: This topic explains how to configure user access to Microsoft Dynamics 365 Fraud Protection.
ms.author: v-davido
ms.service: fraud-protection
ms.date: 01/14/2020
ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Configure user access to Dynamics 365 Fraud Protection

---


# Configure user access to Dynamics 365 Fraud Protection

Microsoft Dynamics 365 Fraud Protection allows you to grant users various levels of access to the tool based on logical or functional roles. Administrators can use the User access section to assign these roles.

## Assign roles 

Initial user and role configuration should be done by your administrator as defined in your Azure tenant. Go to **Configuration** in the left-hand navigation and select **User access** to assign roles to existing users or groups of your tenant. 

Select **Assign role** to grant access a to user or group in this environment. Type the name or the company email address of the person or group you want to edit. If it is recognized as a member of your Azure tenant, it will resolve and display their complete name. Select it to continue. 

To assign a specific role to the user, use the **Roles** dropdown and select one or more of the defined roles. Then select **Assign role** to create the user. 

To edit or delete existing users, select them by name in the **Member** list and then select **Edit** or **Remove**. Roles can be added or deleted from a member in this section. Note that editing your own account, for instance deleting your own administrative role, may interfere with your ability to use certain features of Fraud Protection. If you need to restore permissions, you can reset this in the [Azure portal](https://portal.azure.com/#home). 

To learn more about the available roles, see the “Dynamics 365 Fraud Protection roles” section of this document. 

### User management in your Azure tenant 

Users and roles can also be managed through the Azure portal. For information about how to grant access to users via the Azure portal, see [Assign a user or group to an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/manage-apps/assign-user-or-group-access-portal). For information about how to add users to Azure AD or delete users from Azure AD, see [Add or delete users using Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/add-users-azure-active-directory). 

## Dynamics 365 Fraud Protection roles 

Fraud Protection offers a defined set of user roles, each of which has access to specific features and functions. You can select these when assigning a user to the system. 

All roles listed here are named as they would be in your production environment. To grant users access to these roles in your sandbox environment, choose the version of the role that begins with “Sandbox_” (for example, “Sandbox_AllAreas_Admin”). 

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
