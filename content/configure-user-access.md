---
author: kha-microsoft
description: This article explains how to configure user access to Microsoft Dynamics 365 Fraud Protection.
ms.author: khanguyen
ms.date: 08/03/2022
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Configure user access

---

# Configure user access

Dynamics 365 Fraud Protection lets you grant users various levels of access to the service, based on logical or functional roles. Administrators can use the **User access** section to assign these roles.

> [!IMPORTANT]
> Information in this article is subject to change at any time.

## Assign roles

Users are managed through your assigned Azure Active Directory (Azure AD) tenant.

Roles can be assigned to either of the following types of users:

- Users inside the organization's Azure tenant
- Users outside the organization's Azure tenant, who will be invited to join the tenant as guest users

Users inside the organization's Azure tenant who are member users can view a list of all other users in the tenant. Users outside the organization's Azure tenant who join as guest users can view only users who are in the same Fraud Protection environment that they have access to. Assign member or guest roles to users according to your business privacy requirements.

You can invite colleagues to use Fraud Protection or change their role assignments if one or both of the following conditions are true for your account:

- You're a global administrator of the Azure AD tenant where Fraud Protection is set up. 
- You have "AllAreas_Admin" or "AllAreas_Editor" permissions for Fraud Protection, and have one of the following permissions in the Azure AD tenant where Fraud Protection is set up: Application administrator, Cloud application administrator, User administrator, or Privileged role administrator.

For more information about how to directly add users to your Azure AD tenant as members or non-guest users, see [Create a user account in Azure Active Directory](/azure/active-directory/manage-apps/add-application-portal-assign-users#create-a-user-account).

### Assign roles to users in Fraud Protection

To assign roles to users in Fraud Protection, follow these steps.

1. Open the Fraud Protection portal page.
1. In the left navigation pane, select **Settings**, and then select **User access**.
1. Select **Assign role(s)**.
1. Enter the name or email address of the person or group that you want to assign a Fraud Protection role to.

    > [!NOTE]
    > In the Azure tenant, suggestions for users will appear while you type. Select a suggestion if it matches the user that you want to assign a user role to. Otherwise, a message informs you that an invitation email will be sent to the person or group that you entered, so that the person or group can join the Fraud Protection environment.

1. In the **Roles** field, select one or more defined roles that you want to assign to the user.
1. Select **Assign role(s)**.

### Edit assigned roles

To edit the role that is assigned to a user in Fraud Protection, select the user in the **Member list**, and then select **Edit**.

In this part of the page, roles can be added to or deleted from a user. If you edit your own account (for example, if you delete your own administrative role), your edits might interfere with your ability to use some features of Fraud Protection. If you must restore permissions, you can reset them in the [Azure portal](https://portal.azure.com/#home).

To learn more about the available roles, see the [User roles and access](configure-user-access.md#user-roles-and-access) section of this article.

### Revoke user access to the environment

To revoke a user's access to the current environment, select the user in the **Member list**, and then select **Revoke access**.

> [!IMPORTANT]
> When you revoke access for a user, the user is removed from the current environment. However, they might still have access to other environments in the hierarchy. To fully remove a user's access to Fraud Protection, [delete the user from your Azure AD tenant](/azure/active-directory/fundamentals/add-users-azure-active-directory#delete-a-user). In this way, you completely remove the user's access to your tenant and its associated applications or services.

## User roles and access

Fraud Protection offers a defined set of user roles, each of which has access to specific features and functions. Users will access Fraud Protection differently, depending on their user role in the organization's Azure tenant. You can select roles when you assign a new user to the system.

All the roles in the following list are named as they will be named in your production environment. To grant users access to these roles in your sandbox environment, select the version of the role that begins with "Sandbox_" (for example, **Sandbox_AllAreas_Admin**).


> [!NOTE]
> If you are shown a different selection of roles than those detailed below, you may be using the payment service provider version of Fraud Protection. Go to [User roles and access (payment service providers)](psp-user-roles.md) instead.


### Roles

- **AllAreas_Admin** – This high-level administrative account has full access to Fraud Protection.
- **AllAreasEditor** – A user in this role is a power user who can view all areas and has permissions to use key Fraud Protection tools.
- **AllAreasViewer** – A user in this role can view all areas of Fraud Protection and learn from the data, but can't do uploads or change settings.
- **SupportAgent** – This role provides tailored access to Fraud Protection for support agents who work with your customers. A user in this role can view and work in the support tool, view the ontology, and assign customers to safe lists or block lists.
- **FraudEngineer** – This role provides tailored access for fraud analysts and engineers in your organization who work with Fraud Protection. A user in this role has similar access to a user in the **AllAreasEditor** role. This user can access the data engineering information but doesn't have access to some configuration options.
- **Risk_API** – This role provides access to the API but not to the user-facing tool.
- **ManualReviewFraudManager**, **ManualReviewSeniorAnalyst**, **ManualReviewAnalyst** – These roles are used only internally and don't grant any user permissions in the Fraud Protection portal.

### Permissions

The following table shows the specific read/write permissions that users will have on each page in the Fraud Protection portal, depending on their roles.

<table>
    <thead>
        <tr>
            <th>Section</th>
            <th>Sub-page (tab)</th>
            <th>AllAreas_Admin</th>
            <th>AllAreasEditor</th>
            <th>AllAreasViewer</th>
            <th>SupportAgent</th>
            <th>FraudEngineer</th>
            <th>Risk_API</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan="2">Dashboard</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>No access</td>
        </tr>
        <tr>
            <td rowspan="2">Account creation</td>
            <td>Scorecard</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
            <td>Read only</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>Rules</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>No access</td>
            <td>Read/Write</td>
            <td>No access</td>
        </tr>
        <tr>
            <td rowspan="2">Account login</td>
            <td>Scorecard</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
            <td>Read only</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>Rules</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>No access</td>
            <td>Read/Write</td>
            <td>No access</td>
        </tr>
        <tr>
            <td rowspan="5">Account protection reports</td>
            <td>Summary</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
            <td>Read only</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>Score and reason code</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
            <td>Read only</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>Status and label</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
            <td>Read only</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>Device high level</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
            <td>Read only</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>IP and Device ID</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
            <td>Read only</td>
            <td>No access</td>
        </tr>
        <tr>
            <td rowspan="6">Purchase</td>
            <td>Summary</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
            <td>Read only</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>Rules</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read/Write</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>Rules performance</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
            <td>Read only</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>Virtual fraud analyst</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read/Write</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>Fraud analysis</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
            <td>Read only</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>Support</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
        </tr>
        <tr>
            <td colspan="2">Loss Prevention</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
            <td>Read/Write</td>
        </tr>
        <tr>
            <td colspan="2">Custom assessments</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>No access</td>
            <td>Read/Write</td>
            <td>No access</td>
        </tr>
        <tr>
            <td colspan="2">Search</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
        </tr>
        <tr>
            <td colspan="2">Event Details</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>Read/write</td>
            <td>Read/write</td>
            <td>No access</td>
        </tr>
        <tr>
            <td rowspan="3">Case management</td>
            <td>Queues</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>No access</td>
            <td>No access</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>Report</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
            <td>No access</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>Routing rules</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>No access</td>
            <td>No access</td>
            <td>No access</td>
        </tr>
        <tr>
            <td colspan="2">Velocities</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>No access</td>
            <td>Read/Write</td>
            <td>No access</td>
        </tr>
        <tr>
            <td colspan="2">External calls</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>No access</td>
            <td>Read/Write</td>
            <td>No access</td>
        </tr>
        <tr>
            <td rowspan="2">Lists</td>
            <td>Custom</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>No access</td>
            <td>Read/Write</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>Support</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>Read/Write<sup>1</sup></td>
            <td>Read/Write</td>
            <td>No access</td>
        </tr>
        <tr>
            <td colspan="2">Graph explorer</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
        </tr>
        <tr>
            <td colspan="2">Event tracing</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
            <td>No access</td>
            <td>No access</td>
        </tr>
        <tr>
            <td colspan="2">Data upload</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>No access</td>
            <td>Read/Write</td>
            <td>No access</td>
        </tr>
        <tr>
            <td rowspan="3">API management</td>
            <td>API requests</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
            <td>No access</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>Errors</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
            <td>No access</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>Ontology</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
        </tr>
        <tr>
            <td rowspan="3">Integration</td>
            <td>Dashboard</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>No access</td>
            <td>No access</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>AAD Apps<sup>2</sup></td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>No access</td>
            <td>No access</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>Device Fingerprinting</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>No access</td>
            <td>No access</td>
            <td>No access</td>
        </tr>
        <tr>
            <td rowspan="3">Subscription</td>
            <td>Summary</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
            <td>No access</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>Details</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
            <td>No access</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>Billing</td>
            <td>Read/Write</td>
            <td>No access</td>
            <td>No access</td>
            <td>No access</td>
            <td>No access</td>
            <td>No access</td>
        </tr>
        <tr>
            <td colspan="2">User access</td>
            <td>Read/Write<sup>3</sup></td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
            <td>No access</td>
            <td>No access</td>
        </tr>
        <tr>
            <td rowspan="2">Subject requests</td>
            <td>Search</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>No access</td>
            <td>Read/Write</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>Requests</td>
            <td>Read/Write</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>No access</td>
            <td>Read/Write</td>
            <td>No access</td>
        </tr>
        <tr>
            <td rowspan="2">Transaction acceptance booster</td>
            <td>Opt in</td>
            <td>Read/Write</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
            <td>No access</td>
            <td>No access</td>
        </tr>
        <tr>
            <td>Report</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>Read only</td>
            <td>No access</td>
            <td>No access</td>
            <td>No access</td>
        </tr>
    </tbody>
</table>

1. SupportAgent can remove items from **Support lists** (for example, Safe, Block, and Watch) via the **Event Details** page, or add items to those lists. However, it can't read or edit the full **Support lists** page.
2. To create an Azure AD application, the user must also be assigned the Application Administrator, Cloud Application Administrator, or Global Administrator role in your Azure tenant.
3. The user who assigns roles must also be assigned the Application Administrator, Cloud Application Administrator, Global Administrator, User Administrator, or Privileged Role Administrator role in your Azure tenant.

### Member access

Members can access Fraud Protection by visiting [https://dfp.microsoft.com/](https://dfp.microsoft.com/) and using a Microsoft account to sign in.

### Guest user access

Guest users can access Fraud Protection after they accept an email invitation and sign up (or sign in).

To accept an invitation to Fraud Protection, follow these steps.

1. Check your email inbox for an email that has the subject line "\<Name\> invited you to access applications within their organization."
1. Select **Accept invitation**.
1. If an existing Microsoft account or related account uses your email address, you're prompted to use that account to sign in. Otherwise, follow the setup process to sign up for a new account. After you're fully signed in, you should have access to Fraud Protection.
1. Return to the invitation email, and write down or bookmark the exact link that appears after the text "If you accept this invitation, you will be sent to...." This link will be in the format `https://dfp.microsoft.com/.../...`. Each time that you access Fraud Protection, you must use this exact link.

## Additional resources

[User roles and access (PSPs)](psp-user-roles.md)

[Create a user account in Azure Active Directory](/azure/active-directory/manage-apps/add-application-portal-assign-users#create-a-user-account)

[Assign a user account to an enterprise application](/azure/active-directory/manage-apps/add-application-portal-assign-users#assign-a-user-account-to-an-enterprise-application)

[!INCLUDE[footer-include](includes/footer-banner.md)]
