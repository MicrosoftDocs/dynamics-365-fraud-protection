---
author: josaw1
description: This topic explains how to configure user access for payment service provider (PSP) roles in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 10/07/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: User roles and access (PSPs)

---

# User roles and access (PSPs)

[!include [preview banner](includes/preview-banner.md)]

Payment service providers (PSPs) can grant users of Microsoft Dynamics 365 Fraud Protection various levels of access, based on logical or functional roles.

## Assign PSP roles

The administrator who is defined in the Azure tenant initially creates users in the tenant. They can then assign Fraud Protection roles from the Fraud Protection portal. For information about how to add users to Azure Active Directory (Azure AD), see [Create a user account in Azure Active Directory](/azure/active-directory/manage-apps/add-application-portal-assign-users#create-a-user-account).

### Assign PSP roles to users in Fraud Protection

After a user has been added to the PSP's Azure AD, you can assign a PSP role to them in Fraud Protection.

1. Open the Fraud Protection portal page.
1. In the left navigation pane, select **Settings**, and then select **User access**.
1. Select **Assign role(s)**.
1. Enter the name or company email address of the person or group that you want to assign a Fraud Protection PSP role to.

    If the name is recognized as a member of the Azure tenant, it's resolved to the full name.

1. Select the name.
1. In the **Roles** field, select one or more defined roles that you want to assign to the user.
1. Under each role that you selected, select **Assign role**. The user is added to the Fraud Protection environment that you're using.

### Edit assigned roles or delete users

To edit the role that is assigned to a user in Fraud Protection, or to delete a user, select the user name in the **Member** list, and then select either **Edit** or **Remove**.

In this part of the page, roles can be added to or deleted from a user. If you edit your own account (for example, if you delete your own administrative role), your edits might interfere with your ability to use some features of Fraud Protection. If you must restore permissions, you can reset them in the [Azure portal](https://portal.azure.com/#home).

To learn more about the available PSP roles, see the [PSP user roles and access](psp-user-roles.md#psp-user-roles-and-access) section of this topic.

### User management in your Azure tenant

Users and roles can also be managed through the Azure portal. For information about how to grant access to users through the Azure portal, see [Assign a user account to an enterprise application](/azure/active-directory/manage-apps/add-application-portal-assign-users#assign-a-user-account-to-an-enterprise-application).

## PSP user roles and access

Fraud Protection offers a defined set of user roles, each of which has access to specific features and functions. You can select the features and functions when you assign a user to the system.

![Key to the user access table.](media/psp/user-access-key.png)

![User access table.](media/psp/user-access-table.png)

> [!NOTE]
> To create an Azure AD application, the user who is assigned the **PSP Admin** or **Technical Developer** role must also be assigned the **Application Administrator**, **Cloud Application Administrator**, or **Global Administrator** role in your Azure tenant.

The following roles are available for PSP users:

- **PSP Admin** – This role provides the highest level of authority. A user in this role can manage Fraud Protection for a PSP and its merchant customers. It's a high-level administrative account that has full access to all PSP-related features.
- **Fraud Manager** – This role is an internal role in a PSP. A user in this role is intended to manage Fraud Protection for the PSP's customer merchants.
- **Fraud Supervisor** – This role provides the highest level of authority in a PSP's customer merchant. A user in this role can access merchant-facing functions that the PSP delegates to them.
- **Fraud Analyst** – This role is intended for a PSP's customer merchant who will run analysis and reports. A user in this role has read-only access to the customer merchant's data.
- **Manual Review Agent** – A user in this role is responsible for reviewing individual transactions and approving or declining them. Although manual review agents don't have direct access to the **Support Lists** page, they can modify the status of an entry in the support list through the **Transaction Search** page.
- **Technical Developer** – A user in this role is responsible for managing the technical configurations and integrations of a Fraud Protection instance for a PSP.
- **Customer Service Support** – A user in this role can view the transaction details and is provided with information that is required to handle customer queries.
- **Reporting** – This role provides access to event tracing only, to enable Fraud Protection events and data to be consumed into the PSP's internal reporting infrastructure. 

## Additional resources

[Configure user access](configure-user-access.md)

[Create a user account in Azure Active Directory](/azure/active-directory/manage-apps/add-application-portal-assign-users#create-a-user-account)

[Assign a user account to an enterprise application](/azure/active-directory/manage-apps/add-application-portal-assign-users#assign-a-user-account-to-an-enterprise-application)

[!INCLUDE[footer-include](includes/footer-banner.md)]
