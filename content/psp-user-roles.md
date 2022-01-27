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
Users are managed through your assigned Azure Active Directory (Azure AD) tenant.

Roles can be assigned to either of the following types of users:
- Users inside of the organization's Azure tenant 
- Users outside of the organization's Azure tenant, who will be invited to join the tenant as **Guest** users

> [!IMPORTANT]
> Users inside of the organization's Azure tenant that are **Member** users will have the ability to see a list of all other users in the tenant. In contrast, users outside of the tenant who join as **Guest** users *cannot* see any other users aside from those within the same Fraud Protection environment they were given access to. Decide accordingly based on your business privacy requirements.


For more information on how to directly add users to your Azure Active Directory (Azure AD) tenant as **Member**, non-guest users, see [Create a user account in Azure Active Directory](/azure/active-directory/manage-apps/add-application-portal-assign-users#create-a-user-account).

### Assign PSP roles to users in Fraud Protection

1. Open the Fraud Protection portal page.
1. In the left navigation pane, select **Settings**, and then select **User access**.
1. Select **Assign role(s)**.
1. Enter the name or email address of the person or group that you want to assign a Fraud Protection PSP role to.

    Suggestions of users in the Azure tenant will appear while you type. Select a user if it matches who you intend to assign roles to.
    
    Otherwise, a notice will inform you that an invitation email will be sent to allow the person or group to join the Fraud Protection environment.

1. In the **Roles** field, select one or more defined roles that you want to assign to the user.
1. Select **Assign role(s)**.

> [!NOTE]
> Users outside of the Azure tenant will join the tenant as a **Guest** user and appear in the table of users in **User access** after they have accepted the invitation emailed to them and completed the sign-in/sign-up process.


### Edit assigned roles

To edit the role that is assigned to a user in Fraud Protection, select the user in the member list, and then select **Edit**.

In this part of the page, roles can be added to or deleted from a user. If you edit your own account (for example, if you delete your own administrative role), your edits might interfere with your ability to use some features of Fraud Protection. If you must restore permissions, you can reset them in the [Azure portal](https://portal.azure.com/#home).

To learn more about the available PSP roles, see the [PSP user roles and access](psp-user-roles.md#psp-user-roles-and-access) section of this topic.

### Revoke user access to environment

To revoke a user's access to the current environment, select the user in the member list, and then select **Revoke access**. 

> [!IMPORTANT]
> Revoking access for a user removes them from the current environment. They may still have access to other environments in the hierarchy. To fully remove a user from accessing Fraud Protection, [delete the user from your AAD tenant](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/add-users-azure-active-directory#delete-a-user).

## PSP user roles and access

Fraud Protection offers a defined set of user roles, each of which has access to specific features and functions. You can select the features and functions when you assign a user to the system.

<table>
<thead>
<tr>
<th>Section</th>
<th>Sub-page (tab)</th>
<th>PSP Admin</th>
<th>Fraud Manager</th>
<th>Fraud Supervisor</th>
<th>Fraud Analyst</th>
<th>Manual Review Agent</th>
<th>Technical Developer</th>
<th>Customer Service Support</th>
<th>Reporting</th>
</tr>
</thead>
<tbody>
<td rowspan="2">Purchase</td>
<td>Summary</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Transaction Search</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only/View only</td>
<td>Read/Write</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">Rules</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only/View only</td>
<td>Read only/View only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">Velocities</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only/View only</td>
<td>Read only/View only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td rowspan="2">Lists</td>
<td>Custom</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only/View only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Support</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only/View only</td>
<td>*Write only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">External calls</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">Manual review</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">Graph explorer</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">Event tracing</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>Read/Write</td>
</tr>
<tr>
<td colspan="2">Data upload</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td rowspan="2">API Management</td>
<td>API requests</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Errors</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td rowspan="3">Integration</td>
<td>Dashboard</td>
<td>Read only/View only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>Read only/View only</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>AAD Apps*</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Device Fingerprinting</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">Subscription</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">User access</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">Subject requests</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">Transaction Acceptance Booster</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
</tbody>
</table>

\* To create an Azure AD application, the user who is assigned the **PSP Admin** or **Technical Developer** role must also be assigned the **Application Administrator**, **Cloud Application Administrator**, or **Global Administrator** role in your Azure tenant.

The following roles are available for PSP users:

- **PSP Admin** – This role provides the highest level of authority. A user in this role can manage Fraud Protection for a PSP and its merchant customers. It's a high-level administrative account that has full access to all PSP-related features.
- **Fraud Manager** – This role is an internal role in a PSP. A user in this role is intended to manage Fraud Protection for the PSP's merchant customers.
- **Fraud Supervisor** – This role provides the highest level of authority in a PSP's merchant customer. A user in this role can access merchant-facing functions that the PSP delegates to them.
- **Fraud Analyst** – This role is intended for a PSP's merchant customer who will run analysis and reports. A user in this role has read-only access to the merchant customer's data.
- **Manual Review Agent** – A user in this role is responsible for reviewing individual transactions and approving or declining them. Although manual review agents don't have direct access to the **Support Lists** page, they can modify the status of an entry in the support list through the **Transaction Search** page.
- **Technical Developer** – A user in this role is responsible for managing the technical configurations and integrations of a Fraud Protection instance for a PSP.
- **Customer Service Support** – A user in this role can view the transaction details and is provided with information that is required to handle customer queries.
- **Reporting** – This role provides access to event tracing only, to enable Fraud Protection events and data to be consumed into the PSP's internal reporting infrastructure. 

## Access Fraud Protection 
Users will access Fraud Protection differently depending on their user type within the organization's Azure tenant.


### Members
You can access Fraud Protection by simply visiting [https://dfp.microsoft.com/](https://dfp.microsoft.com/) and signing in with your Microsoft account.

### Guest users
Check your email inbox for an email with the subject line  "___ invited you to access applications within their organization" and follow the following steps:
1. Select the **Accept invitation** button.
1. If an existing Microsoft or related account exists with your email address, you will be prompted to sign in with that account.
  
    Otherwise, follow the setup process to sign up a new account.
1. Once fully signed in, you should have access to  Fraud Protection.  
1. Go back to your email inbox with the invitation email. 

    Note down or bookmark the exact link after the text "If you accept this invitation, you will be sent to ..." 
    
    This link will be in the format of `https://dfp.microsoft.com/.../...`

    Every time you wish to access Fraud Protection, you must visit this exact, specialized link.


## Additional resources

[Configure user access](configure-user-access.md)

[Create a user account in Azure Active Directory](/azure/active-directory/manage-apps/add-application-portal-assign-users#create-a-user-account)

[Assign a user account to an enterprise application](/azure/active-directory/manage-apps/add-application-portal-assign-users#assign-a-user-account-to-an-enterprise-application)


[!INCLUDE[footer-include](includes/footer-banner.md)]
