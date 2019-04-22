---
author: jackwi111
description: This topic explains how to configure user access to Microsoft Dynamics 365 Fraud Protection.
ms.author: v-jowigh
ms.service: crm-online
ms.date: 04/22/2019

ms.topic: conceptual
title: Configure user access to Dynamics 365 Fraud Protection
---


# Configure user access to Dynamics 365 Fraud Protection

After you sign up for Microsoft Dynamics 365 Fraud Protection, its services are configured in your Microsoft Azure tenant. When this process is completed, you can sign in to your tenant by using your Azure Active Directory (Azure AD) credentials and access Dynamics 365 Fraud Protection.

## Find your app

For information about how to grant access to users and add user roles to Dynamics 365 Fraud Protection via the Azure portal, see [Assign a user or group to an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/manage-apps/assign-user-or-group-access-portal).

For information about how to add users to Azure AD or delete users from Azure AD, see [Add or delete users using Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/add-users-azure-active-directory).

You must be a tenant admin to administer Azure AD. If you have that role, follow these steps to configure user access to Dynamics 365 Fraud Protection. If you don't have the required permissions, ask your tenant admin for help.

1. Open the [Azure portal](https://portal.azure.com/#home).
1. In the navigation pane, select **Azure Active Directory**. The **Microsoft – Overview** page appears.
1. In the left pane, under **Manage**, select **Enterprise Applications**. The **Enterprise applications – All applications** page appears.
1. In the **Application Type** field, select **Microsoft Applications**. Then select **Apply**. 
1. To find the **Dynamics 365 Fraud Protection** enterprise app, search for **Dynamics 365 Fraud Protection**.
1. In the list of results, select **Dynamics 356 Fraud Protection**. The **Dynamics 365 Fraud Protection – Overview** page appears.

## Configure users in Dynamics 365 Fraud Protection

> [!IMPORTANT]
> Microsoft Dynamics 365 Fraud Protection Public Preview supports comprehensive access rights for all users. Upcoming updates will let you manage users, groups, and role assignments.

To add users and groups from Azure AD, sign up for [Azure AD Premium edition](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-get-started-premium). For information about the rights that are associated with these roles, see the tables later in this topic.

You can configure users by assigning them to the **Sandbox_AllAreas_Admin** or **AllAreas_Admin** role, depending on your sandbox (test) or production (live) environment.

1. On the **Dynamics 365 Fraud Protection – Overview** page, in the left pane, select **Getting started**, and then select either **Assign a user for testing (required)** or **Deploy single sign-on to users and groups (recommended)**. The **Users and groups** page appears.
1. To add users, select **Add user**. The **Add Assignment** blade appears.
1. In the **Add Assignment** blade, select **Users**. The **Users** blade appears.
1. In the **Users** blade, select a member, or invite an external user to join, and then select **Select**.
1. Return to the **Add Assignment** blade, and select **Select Role**. The **Select Role** blade appears.
1. In the **Select Role** blade, select a role, and then select **Select**.
1. To apply the role to the member that you selected, in the **Add Assignment** blade, select **Assign**. In the **Users** blade, the user and its assigned role appear.

By using these steps, you can continue to add users and their assignment to the **Sandbox_AllAreas_Admin** or **AllAreas_Admin** role. You can also use these steps to delete users and their role assignments.

To access the Dynamics 365 Fraud Protection portal, add your account to the following portals:

- [Sandbox portal](https://dfp.microsoft-int.com/)
- [Production portal](https://dfp.microsoft.com/)

> [!NOTE]
> The Dynamics 365 Fraud Protection sandbox portal and accompanying roles are associated with your integration (test) environment. The Dynamics 365 production portal and accompanying roles are associated with your production (live) environment.

## Manage access to a sandbox environment by using roles

The Dynamics 365 Fraud Protection sandbox environment lets your teams do integration testing outside the production environment. This environment is available to users who have the appropriate access. The data in this environment isn't permanent. The code that runs in this environment is periodically updated and communicated to all participating merchants before updates occur.

Use the following role membership to manage user access to the Dynamics 365 Fraud Protection sandbox environment.


| App role | Description |
|---|---|
| Sandbox_AllAreas_Admin | This role grants access rights to all areas and functionality of the Dynamics 365 Fraud Protection portal. |

## Manage access to a production environment by using roles

Members of the Dynamics 365 Fraud Protection team and merchant teams use the Dynamics 365 Fraud Protection production environment to work in their production environment. This environment is available to users who have the appropriate access.

Use the following role membership to manage user access to the Dynamics 365 Fraud Protection production environment.

| App role | Description |
|---|---|
| AllAreas_Admin | This role grants access rights to all areas and functionality of the Dynamics 365 Fraud Protection portal. |
