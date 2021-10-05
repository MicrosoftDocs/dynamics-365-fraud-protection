---
author: tajimha
description: This topic explains how to configure user access for payment service provider (PSP) roles in Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 10/04/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: User roles and access (PSPs)

---


# User roles and access (PSPs)
[!include [preview banner](includes/preview-banner.md)]

Payment service providers (PSPs) can grant users of Dynamics 365 Fraud Protection various levels of access based on logical or functional roles.

## Assign roles 

The initial user and role configuration must be set up by the administrator, as defined in your Azure tenant. 

### Existing users or groups of your tenant

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

Alternatively, users and roles can be managed through the Azure portal. For information about how to grant access to users through the Azure portal, see [Assign a user or group to an enterprise app in Azure Active Directory](/azure/active-directory/manage-apps/assign-user-or-group-access-portal). For information about how to add users to Azure AD or delete users from Azure AD, see [Add or delete users using Azure Active Directory](/azure/active-directory/fundamentals/add-users-azure-active-directory). 

## PSP user roles and access 

Fraud Protection offers a defined set of user roles, each of which has access to specific features and functions. You can select the features and funcitons when you assign a user to the system. 

![User Access Key](media/psp/user-access-key.png)

![User Access Table](media/psp/user-access-table.png)

>[!NOTE]
>To create an Azure AD application, the user assigned "PSP Admin" or "Technical Developer" role must also be assigned "Application Administrator", "Cloud Application Administrator", or "Global Administrator" in your Azure tenant.

The following roles are available for PSP users.

- **PSP Admin** - This role has the highest level of authority and can manage Fraud Protection for a PSP and their merchant customers. It is a high-level administrative account with full access to all of the PSP related features. 

- **Fraud Manager** - This is an internal role within the PSP. The user in this role is intended to manage Fraud Protection for a PSP's customer merchants.

- **Fraud Supervisor** - This role is the highest level of authority within a PSP's customer merchant and can access merchant-facing functions delegated to them by the PSP.

- **Fraud Analyst** - This role is intended for a PSP's customer merchant who will run analysis and reports with read-only access to a customer merchant's data.

- **Manual Review Agent** - This user is responsible for reviewing individual transactions and approving or declining them. A Manual Review Agent does not have direct access to the **Support Lists** page, but can modify the status of an entry in the support list through the **Transaction Search** page. 

- **Technical Developer** - This role is responsible for managing the technical configurations and integrations of a Fraud Protection instance for the PSP. 

- **Customer Service Support** - This user can view the transaction details and is provided with information needed to handle customer queries.

- **Reporting** - This role only has access to event tracing to allow Fraud Protection events and data to be consumed into the PSP's internal reporting infrastructure. 

[!INCLUDE[footer-include](includes/footer-banner.md)]
