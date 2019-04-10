---
author: jackwi111
description: Configure user access to Dynamics 365 Fraud Protection
ms.author: v-jowigh
ms.date: 03/01/2019
ms.service:
- crm-online
ms.topic: conceptual
title: Configure user access to Dynamics 365 Fraud Protection
---


# Configure user access to Dynamics 365 Fraud Protection

After signing up for Dynamics 365 Fraud Protection, the product’s services are configured within your Azure tenant. When this process completes, you can log in to your tenant with your Azure Active Directory (Azure AD) credentials to access the Dynamics 365 Fraud Protection portal.

The Dynamics 365 Fraud Protection portal provides three experiences:

- [Diagnose](diagnose-experience.md)
- [Evaluate](evaluate-experience.md)
- [Protect](protect-experience.md)

Set up your company’s user access to Dynamics 365 Fraud Protection portal, using the following roles and permissions.

## To configure user access via the Azure portal

You can configure users by assigning them to specific roles provided within Dynamics 365 Fraud Protection.

To grant users access and add user roles to Dynamics 365 Fraud Protection via the Azure portal, see [Assign a user or group to an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/manage-apps/assign-user-or-group-access-portal).

You must be a tenant admin to administer the Azure Active Directory. If you have that role, follow these instructions to configure user access to Dynamics 365 Fraud Protection. If you do not have the required permissions, ask your tenant admin for assistance.

1.	Open the **Azure Active Directory** in the [Microsoft Azure portal](https://portal.azure.com/#home).
1.	Click **Manage**, then **Enterprise Applications** within the **Azure Active Directory Overview** page.
1.	Search for the **Dynamics 365 Fraud Protection** enterprise app in your Azure AD by entering the DFP App GUID ‘bf04bdab-e06f-44f3-9821-d3af64fc93a9’.
1.	Within the Enterprise app, select **Getting Started**, and then select either **Assign a user for testing (required)** or **Deploy single sign-on to users and groups (recommended)**.
1.	Add any Users or Groups from your Azure AD, and assign them to appropriate Dynamics 365 Fraud Protection BETA roles. For rights associated with these roles, see the following tables.

> [!TIP]
> To access the Dynamics 365 Fraud Protection portal, add your account to the following:

- [Sandbox portal](https://dfp.microsoft-int.com/)
- [Production portal](https://dfp.microsoft.com/)

> [!NOTE]
> The Sandbox portal and roles are associated with your integration (test) environment. The Production portal and roles are associated with your production (live) environment.

## Manage access to sandbox environment through roles

The Dynamics 365 Fraud Protection sandbox environment enables your teams to perform integration testing outside the production environment. This environment is available to those with appropriate access. The data here is not permanent. The code running in this environment is updated periodically and communicated to all participating merchants before updates.

Use the following role membership to manage user access to the Dynamics 365 Fraud Protection sandbox environment.

> [!div class="mx-tableFixed"]
> |App role   |Description   |Rights   |
> |---|---|---|
> |Sandbox_AllAreas_Admin   |Within all areas of the Dynamics 365 Fraud Protection portal, grants access rights to All Areas Edit and All Areas Viewer as well as enabling View, Create, Edit, and Delete access to content and APIs within all areas.   |- VIEW<br/>- CREATE<br/>- EDIT<br/>- DELETE<br/>- ADMIN |
> |Sandbox_AllAreas_Edit   |Within all areas of the Dynamics 365 Fraud Protection portal, grants View, Create, Edit, and Delete access to all areas.   |- VIEW<br/>- CREATE<br/>- EDIT<br/>- DELETE   |
> |Sandbox_AllAreas_Viewer   |Within all areas of the Dynamics 365 Fraud Protection portal, grants View access to all areas.   |- VIEW   |
> |Sandbox_Data_Admin   |Within the **Data engineering** area of the Dynamics 365 Fraud Protection portal, grants access rights to Data Edit and Data Viewer as well as enabling View, Create, Edit, and Delete access to content and APIs within the Data Management area.   |- VIEW<br/>- CREATE<br/>- EDIT<br/>- DELETE<br/>- ADMIN   |
> |Sandbox_Data_Edit   |Within the **Data engineering** area of the Dynamics 365 Fraud Protection portal, grants View, Create, Edit, and Delete access to content and APIs within the Data Management area.   |- VIEW<br/>- CREATE<br/>- EDIT<br/>- DELETE  |
> |Sandbox_Data_Viewer   |Within the **Data engineering** area of the Dynamics 365 Fraud Protection portal, grants View access to the Data Management area and APIs.   |- VIEW  |
> |Sandbox_Risk_Admin   |Within the **Risk decisioning** and **Data engineering** (except subject requests) areas of the Dynamics 365 Fraud Protection portal, grants access rights to Risk Edit and Risk Viewer as well as enabling View, Create, Edit, and Delete access to content and APIs within the <Risk> area.   |- VIEW<br/>- CREATE<br/>- EDIT<br/>- DELETE<br/>- ADMIN   |
> |Sandbox_Risk_Edit   |Within the **Risk decisioning** and **Data engineering** (except subject requests) areas of the Dynamics 365 Fraud Protection portal, grants View, Create, Edit, and Delete access to content and APIs within the Risk Management area.   |- VIEW<br/>- CREATE<br/>- EDIT<br/>- DELETE   |
> |Sandbox_Risk_Viewer   |Within the **Risk decisioning** and **Data engineering** (except subject requests) areas of the Dynamics 365 Fraud Protection portal, grants View access to the Risk Management area.   |- VIEW  |

## Manage access to production environment through roles

The Dynamics 365 Fraud Protection production environment is used for Dynamics 365 Fraud Protection team members and merchant teams to work in their production environment. This environment is available to those with appropriate access controls.

Use the following role membership to manage user access to the Dynamics 365 Fraud Protection production environment.

> [!div class="mx-tableFixed"]
> |App role   |Description   |Rights   |
> |---|---|---|
> |AllAreas_Admin   |Within all areas of the Dynamics 365 Fraud Protection portal, grants access rights to All Areas Edit and All Areas Viewer as well as enabling View, Create, Edit, and Delete access to content and APIs within all areas.   |- VIEW<br/>- CREATE<br/>- EDIT<br/>- DELETE<br/>- ADMIN  |
> |AllAreas_Edit   |Within all areas of the Dynamics 365 Fraud Protection portal, grants View, Create, Edit, and Delete access to all areas.   |- VIEW<br/>- CREATE<br/>- EDIT<br/>- DELETE   |
> |AllAreas_Viewer   |Within all areas of the Dynamics 365 Fraud Protection portal, grants View access to all areas.   |- VIEW  |
> | Data_Admin   |Within the **Data engineering** area of the Dynamics 365 Fraud Protection portal, grants access rights to Data Edit and Data Viewer as well as enabling View, Create, Edit, and Delete access to content and APIs within the Data Management area.   |- VIEW<br/>- CREATE<br/>- EDIT<br/>- DELETE<br/>- ADMIN   |
> | Data_Edit   |Within the **Data engineering** area of the Dynamics 365 Fraud Protection portal, grants View, Create, Edit, and Delete access to content and APIs within the Data Management area.   |- VIEW<br/>- CREATE<br/>- EDIT<br/>- DELETE   |
> |Data_Viewer   |Within the **Data engineering** area of the Dynamics 365 Fraud Protection portal, grants View access to the Data Management area and APIs.   |- VIEW  |
> |Risk_Admin   |Within the **Risk decisioning** and **Data engineering** (except subject requests) areas of the Dynamics 365 Fraud Protection portal, grants access rights to Risk Edit and Risk Viewer as well as enabling View, Create, Edit, and Delete access to content and APIs within the <Risk> area.   |- VIEW<br/>- CREATE<br/>- EDIT<br/>- DELETE<br/>- ADMIN   |
> |Risk_Edit   |Within the **Risk decisioning** and **Data engineering** (except subject requests) areas of the Dynamics 365 Fraud Protection portal, grants View, Create, Edit, and Delete access to content and APIs within the Risk Management area.   |- VIEW<br/>- CREATE<br/>- EDIT<br/>- DELETE   |
> |Risk_Viewer   |Within the **Risk decisioning** and **Data engineering** (except subject requests) areas of the Dynamics 365 Fraud Protection portal, grants View access to the Risk Management area.   |- VIEW  |
