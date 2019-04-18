---
author: jackwi111
description: Configure user access to Dynamics 365 Fraud Protection
ms.author: v-jowigh
ms.service: crm-online
ms.date: 03/01/2019

ms.topic: conceptual
title: Configure user access to Dynamics 365 Fraud Protection
---


# Configure user access to Dynamics 365 Fraud Protection

After signing up for Dynamics 365 Fraud Protection, its services are configured within your Azure tenant. When this process completes, you can log in to your tenant with your Azure Active Directory (Azure AD) credentials to access Dynamics 365 Fraud Protection.

## Find your app

To grant users access and add user roles to Dynamics 365 Fraud Protection via the Azure portal, see [Assign a user or group to an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/manage-apps/assign-user-or-group-access-portal).

To add or delete users to Azure AD, see [Add or delete users using Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/add-users-azure-active-directory).

You must be a tenant admin to administer the Azure Active Directory. If you have that role, follow these instructions to configure user access to Dynamics 365 Fraud Protection. If you do not have the required permissions, ask your tenant admin for assistance.

1. Go to the [Microsoft Azure portal](https://portal.azure.com/#home).
1. In the navigation bar, select **Azure Active Directory**. The **Microsoft – Overview** page appears.
1. In the **Manage** menu, select **Enterprise Applications**.
1. In the **Application Type** dropdown, select **Microsoft Applications**>**Apply**. The **Enterprise applications – All applications** page appears.
1. To find the **Dynamics 365 Fraud Protection** enterprise app, search for **Dynamics 365 Fraud Protection**.
1. From the results pane, select **Dynamics 356 Fraud Protection**. The **Dynamics 365 Fraud Protection – Overview** page appears.

## Configure users in Dynamics 365 Fraud Protection

>[!IMPORTANT]
>For Dynamics 365 Fraud Protection Public Preview, the product supports comprehensive access rights for all users. Updates to managing users, groups, and role assignments is forthcoming.

To add Users and Groups from your Azure AD, sign up for [Azure AD Premium edition]( https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/active-directory-get-started-premium). For rights associated with these roles, see the following tables.

You can configure users by assigning them to the (Sandbox) AllAreas_Admin role, depending on your sandbox (test) or production (live) environment.

1.	Select **Getting Started**, and then choose either **Assign a user for testing (required)** or **Deploy single sign-on to users and groups (recommended)**.
1. To add users, select **Add user**. The **Add Assignment** page appears.
1. In the **Add Assignment** frame, select **Users**. The **Users** page appears.
1. In the **Users** frame, select a member or invite an external user to join, and then click **Select**.
1. After selecting a member, return to the **Add Assignment** frame, and click **Select Role**. The **Select Role** page appears.
1. In the **Select Role** frame, select a role, and then click **Select**.
1. To apply that role to the member you selected, in the **Add Assignment** frame, select **Assign**. In the **Users** page, the user and their assigned role appear. Using these steps, you can continue to add and delete users and their Sandbox_AllAreas_Admin or AllAreas_Admin role assignment.

To access the Dynamics 365 Fraud Protection portal, add your account to the following:

- [Sandbox portal](https://dfp.microsoft-int.com/)
- [Production portal](https://dfp.microsoft.com/)

> [!NOTE]
> The Dynamics 365 Fraud Protection sandbox portal and accompnaying roles are associated with your integration (test) environment. The Dynamics 365 production portal and accompanying roles are associated with your production (live) environment.

## Manage access to sandbox environment with roles

The Dynamics 365 Fraud Protection sandbox environment enables your teams to perform integration testing outside the production environment. This environment is available to those with appropriate access. The data here is not permanent. The code running in this environment is updated periodically and communicated to all participating merchants before updates.

Use the following role membership to manage user access to the Dynamics 365 Fraud Protection sandbox environment.

> [!div class="mx-tableFixed"]
> |App role   |Description  | 
> |---|---|
> |Sandbox_AllAreas_Admin   |Grants access rights to all areas and functionality of the Dynamics 365 Fraud Protection portal.   |

## Manage access to production environment with roles

The Dynamics 365 Fraud Protection production environment is used for Dynamics 365 Fraud Protection team members and merchant teams to work in their production environment. This environment is available to those with appropriate access.

Use the following role membership to manage user access to the Dynamics 365 Fraud Protection production environment.

> [!div class="mx-tableFixed"]
> |App role   |Description   |
> |---|---|---|
> |AllAreas_Admin   |Grants access rights to all areas and functionality of the Dynamics 365 Fraud Protection portal.   |

