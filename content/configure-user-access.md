---
author: josaw1
description: This topic explains how to configure user access to Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 10/07/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Configure user access

---

# Configure user access

Microsoft Dynamics 365 Fraud Protection lets you grant users various levels of access to the tool, based on logical or functional roles. Administrators can use the **User access** section to assign these roles.

## Assign roles
Users are managed through your assigned Azure Active Directory (Azure AD) tenant.

Roles can be assigned to either of the following types of users:
- Users inside of the organization's Azure tenant. 
- Users outside of the organization's Azure tenant, who will be invited to join the tenant as guest users.

> [!IMPORTANT]
> Users inside of the organization's Azure tenant that are member users can see a list of all other users in the tenant. In contrast, users outside of the tenant who join as guest users cannot see any other users aside from those within the same Fraud Protection environment they were given access to. Assign users member or guest roles accordingly based on your business privacy requirements.

For more information on how to directly add users to your Azure AD tenant as members or non-guest users, see [Create a user account in Azure Active Directory](/azure/active-directory/manage-apps/add-application-portal-assign-users#create-a-user-account).

### Assign roles to users in Fraud Protection

To assign roles to users in Fraud Protection, follow these steps.

1. Open the Fraud Protection portal page.
1. In the left navigation pane, select **Settings**, and then select **User access**.
1. Select **Assign role(s)**.
1. Enter the name or email address of the person or group that you want to assign a Fraud Protection role to.

    > [!NOTE] 
    >  In the Azure tenant, user suggestions will appear while you type. Select a user if it matches whom you intend to assign a user role to. Otherwise, a notice will inform you that an invitation email will be sent to the person or group you entered to allow them to join the Fraud Protection environment.

1. In the **Roles** field, select one or more defined roles that you want to assign to the user.
1. Select **Assign role(s)**.

### Edit assigned roles

To edit the role that is assigned to a user in Fraud Protection, select the user in the member list, and then select **Edit**.

In this part of the page, roles can be added to or deleted from a user. If you edit your own account (for example, if you delete your own administrative role), your edits might interfere with your ability to use some features of Fraud Protection. If you must restore permissions, you can reset them in the [Azure portal](https://portal.azure.com/#home).

To learn more about the available roles, see the [Fraud Protection roles](configure-user-access.md#roles) section of this topic.

### Revoke user access to environment

To revoke a user's access to the current environment, select the user in the member list, and then select **Revoke access**. 

> [!IMPORTANT]
> Revoking access for a user removes them from the current environment. They may still have access to other environments in the hierarchy. To fully remove a user from accessing Fraud Protection, [delete the user from your AAD tenant](/azure/active-directory/fundamentals/add-users-azure-active-directory#delete-a-user).

## User roles and access

Fraud Protection offers a defined set of user roles, each of which has access to specific features and functions. Users will access Fraud Protection differently depending on their user role within the organization's Azure tenant. You can select roles when you assign a new user to the system.

All the roles in the following list are named as they will be named in your production environment. To grant users access to these roles in your sandbox environment, select the version of the role that begins with "Sandbox_" (for example, **Sandbox_AllAreas_Admin**).

- **AllAreas_Admin** – This high-level administrative account has full access to Fraud Protection.
- **AllAreasEditor** – A user in this role is a power user who can view all areas and has permissions to use key Fraud Protection tools.

    - **Write** – **AllAreasEditor** user roles have write permissions to edit or perform data uploads, rules, virtual fraud analyst, lists, and subject requests.
    - **Read** – **AllAreasEditor** user roles have read permissions for diagnostic reports, support tool, scorecard, metrics, ontology, graph explorer, API configuration, metering, monitoring, permissions, and transaction acceptance booster.

- **AllAreasViewer** – A user in this role can view all areas of Fraud Protection and learn from the data, but can't do uploads or change settings.

    - **Write** – **AllAreasViewer** user roles have no write permissions.
    - **Read** – **AllAreasViewer** user roles have read permissions for all areas.

- **SupportAgent** – This role provides tailored access to Fraud Protection for support agents who work with your customers. A user in this role can view and work in the support tool, view the ontology, and assign customers to safe lists or block lists.

    - **Write** – **SupportAgent** user roles have write permissions for support lists.
    - **Read** – **SupportAgent** user roles have read permissions for lists, support tool, and ontology.
    - **No access** – **SupportAgent** user roles have no access to areas other than those specified for write and read permissions. Some pages might be accessible in the navigation but not fully usable.

- **FraudEngineer** – This role provides tailored access for fraud analysts and engineers in your organization who work with Fraud Protection. A user in this role has similar access to a user in the **AllAreasEditor** role. This user can access the data engineering information but doesn't have access to some configuration options.

    - **Write** – **AllAreasEditor** user roles have write permissions to edit or perform data uploads, rules, virtual fraud analyst, lists, and subject requests.
    - **Read** – **AllAreasEditor** user roles have read permissions for diagnostic reports, support tool, scorecard, metrics, ontology, and graph explorer.
    - **No access** – **AllAreasEditor** user roles have no access to API configuration, metering, monitoring, permissions, and transaction acceptance booster. Some pages might be accessible in the navigation but not fully usable.

- **Risk_API** – This role provides access to the API but not to the user-facing tool.

### Member access

Members can access Fraud Protection by visiting [https://dfp.microsoft.com/](https://dfp.microsoft.com/) and signing in with a Microsoft account.

### Guest user access

Guest users can access Fraud Protection after accepting an email invitation and signing up (or signing in).

To accept an invitation to Fraud Protection, follow these steps.

1. Check your email inbox for an email with the subject line "___ invited you to access applications within their organization".
1. Select **Accept invitation**.
1. If an existing Microsoft or related account exists with your email address, you will be prompted to sign in with that account. Otherwise, follow the setup process to sign up for a new account. Once fully signed in, you should have access to Fraud Protection.  
1. Go back to the invitation email and write down or bookmark the exact link after the text "If you accept this invitation, you will be sent to ...". This link will be in the format `https://dfp.microsoft.com/.../...`. Each time you access Fraud Protection you will need to use this specific link.

## Additional resources

[User roles and access (PSPs)](psp-user-roles.md)

[Create a user account in Azure Active Directory](/azure/active-directory/manage-apps/add-application-portal-assign-users#create-a-user-account)

[Assign a user account to an enterprise application](/azure/active-directory/manage-apps/add-application-portal-assign-users#assign-a-user-account-to-an-enterprise-application)

[!INCLUDE[footer-include](includes/footer-banner.md)]
