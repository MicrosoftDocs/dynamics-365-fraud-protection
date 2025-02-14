---
author: arj-malhotra
description: This article explains how to configure user access to Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 08/06/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Configure user access
---

# Configure user access

[!include[deprecation](includes/deprecation.md)]

In Microsoft Dynamics 365 Fraud Protection, you can grant users different levels of access to the service, based on logical or functional roles. Administrators can use the **User access** section to assign these roles. For more information about the available roles, see [User roles and access](user-roles-access.md).

If your Fraud Protection instance has multiple environments, user access for each environment can be found by using the environment switcher. If the environment has child environments, the user or groups that are granted with a user role automatically have the same level of access to all the child environments. If you revoke a user role from an environment, the user or groups automatically lose the same level of access to all the child environments, unless it's explicitly added for another environment. 

Users are managed through your assigned Microsoft Entra tenant.

Roles can be assigned to the following types of users:

- Users inside the organization's Azure tenant
- Users outside the organization's Azure tenant, who will be invited to join the tenant as guest users

Member users inside the organization's Azure tenant can view a list of all other users in the tenant. Users outside the organization's Azure tenant who join as guest users can view only users who are in the same Fraud Protection environment that they have access to. Assign member or guest roles to users according to your business privacy requirements.

You can invite colleagues to use Fraud Protection or change their role assignments if one or both of the following conditions are met for your account:

- You're a global administrator of the Microsoft Entra tenant where Fraud Protection is set up. 
- You have one of these Fraud Protection roles assigned to you: **Product Admin**, **AllAreas_Admin**, or **Manual Review Fraud Manager**. You can only assign roles to other colleagues that have the same or lesser permissions than the role you have.

Administrator roles are asked to attest to usage disclaimers and play a brief educational video during their first-run experience in Fraud Protection.

For more information about how to directly add users to your Microsoft Entra tenant as members or non-guest users, see [Create a user account in Microsoft Entra ID](/azure/active-directory/manage-apps/add-application-portal-assign-users#create-a-user-account).

### Assign roles to users in Fraud Protection

To assign roles to users in Fraud Protection, follow these steps.

1. Open the Fraud Protection portal page.
2. In the left navigation pane, select **Settings**, and then select **User access** > **Assign roles**.
3. Enter the name or email address of the person or group that you're assigning a Fraud Protection role to.

    > [!NOTE]
    > In the Azure tenant, suggestions for users will appear while you type. Select a suggestion if it matches the user that you want to assign a role to. Otherwise, you'll receive a message that an invitation email will be sent to the person or group that you entered. That person or group can then join the Fraud Protection environment.

4. In the **Roles** field, select one or more defined roles that you want to assign to the user.
5. Select **Assign role(s)**.

### Edit assigned roles

To edit the role that's assigned to a user in Fraud Protection, select the user in the **Member list**, and then select **Edit**. To edit a role for a specific environment, use the environment switcher to select the environment that you want to configure. 

In this part of the page, roles can be added to or deleted from a user. If you edit your own account (for example, if you delete your own administrative role), your edits might interfere with your ability to use some features of Fraud Protection. If you must restore permissions, you can reset them in the [Azure portal](https://portal.azure.com/#home).

To learn more about the available roles, see the article, [User roles and access](user-roles-access.md).

### Revoke user access to the environment

To revoke a user's access to a specific environment, use the environment switcher to select the environment that you want to configure. 

To revoke a user's access to the current environment, select the user in the **Member list**, and then select **Revoke access**.

> [!IMPORTANT]
> When you revoke access for a user, the user is removed from the current environment. However, they might still have access to other environments in the hierarchy. If you want to remove the user from Fraud Protection, you must delete the user from your Microsoft Entra tenant. In this way, you completely remove the user's access to your tenant, and to its associated applications or services.

[!INCLUDE[footer-include](includes/footer-banner.md)]
