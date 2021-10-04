---
author: tajimha
description: This topic explains how to configure user access for PSP roles in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 10/04/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: PSP User Roles and Access

---


# Configuring Access using PSP Roles

Microsoft Dynamics 365 Fraud Protection allows you to grant users various levels of access to the tool based on logical or functional roles.

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

## PSP User Roles and Access 

Fraud Protection offers a defined set of user roles, each of which has access to specific features and functions. You can select these when assigning a user to the system. 

![User Access Key](/content/media/psp-images/user-access-key.png)

![User Access Table](/content/media/psp-images/user-access-table.png)

*To create an Azure AD Application, the user assigned a PSP Admin or Technical Developer role must also be an Application Administrator, Cloud Application Administrator, or Global Administrator in your Azure tenant.

### PSP Admin 
A PSP Admin has the highest level of authority and can manage Dynamics 365 Fraud Protection for a PSP and their merchant customers. It is a high-level administrative account with full access to all the PSP-centric features. 

### Fraud Manager 
A Fraud Manager is an internal role within a Payment Service Provider intended to manage Dynamics 365 Fraud Protection for a PSP's customer merchants.

### Fraud Supervisor 
A Fraud Supervisor is the highest level of authority within a PSP's customer merchant and can access merchant facing functions delegated to them by the PSP.

### Fraud Analyst 
A Fraud analyst is a role for a PSP's customer merchant used to run analysis and reports with read-only access to a customer merchant's data.

### Manual Review Agent 
A Manual Review Agent is responsible for reviewing individual transactions and approving or declining them.  
*A Manual Review Agent does not have direct access to view the Support Lists page but can modify the state of an entry in the Support List via the Transaction Search page. 

### Technical Developer
A Technical Developer is responsible for managing the technical configurations and integrations of a PSP's Dynamics 365 Fraud Protection instance. 

### Customer Service Support
Customer Service Support has visibility on the transaction details and is provided with information needed to handle  customer queries.

### Reporting
This PSP role only has access to Event Tracing to allow integrating into DFP events and data to for consumption into the PSP's internal reporting infrastructure. 

[!INCLUDE[footer-include](includes/footer-banner.md)]
