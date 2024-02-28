---
author: arj-malhotra
description: This article provides information about roles and user access to Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 02/28/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: User roles and access

---

# User roles and access

This article provides information about roles and user access to Microsoft Dynamics 365 Fraud Protection.

Microsoft Dynamics 365 Fraud Protection offers a defined set of user roles, each of which has access to specific features and functions. Users access Fraud Protection differently, depending on their user role in the organization's Azure tenant. When you add a new user to the system, you can select the roles to assign roles to the user. For information about how to set up user roles and access in Fraud Protection, see [Configure user access](configure-user-access.md).

All the roles in the following list are named as they are named in your production environment. To grant users access to these roles in your sandbox environment, select the version of the role that begins with "Sandbox_". For example, **Sandbox_AllAreas_Admin**.

> [!NOTE]
> If the selection of roles that's shown to you differs from the following list, you might be using the payment service provider version of Fraud Protection. In this case, see [Payment service provider user roles and access](psp-user-roles.md) for the list of roles.

## Roles

- **Product admin** – This top-level administrative account has full access to your Fraud Protection instance and all the environments in the hierarchy.
- **AllAreas_Admin** – This high-level administrative account has full access to an environment and its child environments Fraud Protection.
- **AllAreasEditor** – A user in this role is a power user who can view all areas and has permissions to use key Fraud Protection tools in an environment and its child environments. However, this role doesn't give access to make user role assignments.
- **AllAreasViewer** – A user in this role can view all areas of Fraud Protection and learn from the data, but can't do uploads or change settings in an environment and its child environments.
- **SupportAgent** – This role provides tailored access to Fraud Protection for support agents who work with your customers. A user in this role can view and work in the support tool, view the ontology, and assign customers to safe lists or block lists in an environment and its child environments.
- **FraudEngineer** – This role provides tailored access for fraud analysts and engineers in your organization who work with Fraud Protection. A user in this role has similar access to a user in the **AllAreasEditor** role. This user can access the data engineering information but doesn't have access to some configuration options in an environment and its child environments.
- **Risk_API** – This role provides access to the API for an environment and its child environments but not to the user-facing tool.
- ManualReviewAnalyst – A user in this role is responsible for reviewing individual transactions and approving or declining them. Manual review analysts have access to the Search tool and queues in Case management.
- **ManualReviewSeniorAnalyst** – In addition to reviewing individual transactions and approving or declining them, a user in this role can also set up routing rules. Manual review senior analysts have access to the Search tool, queues, and Routing rules in Case management.
- **ManualReviewFraudManager** – A user in this role is intended to manage manual review operations for the merchant. A user in this role can assign user access, configure assessment rules, create queues, define routing rules, and view performance reports. 


## Permissions

The following table shows the specific read/write permissions that users have on each page in the Fraud Protection portal, depending on their roles. Along with the sections listed in the table, **Product admin** also has Read/Write permission to the **Admin settings** page, including the **Configuration**, **Search**, **Billing**, and **Subscription** tabs.

<table>
<thead>
<tr>
<th>Section</th>
<th>Subpage (tab)</th>
<th>Product Admin</th>
<th>AllAreas_Admin</th>
<th>AllAreasEditor</th>
<th>AllAreasViewer</th>
<th>SupportAgent</th>
<th>FraudEngineer</th>
<th>Risk_API</th>
<th>ManualReviewFraudManager</th>
<th>ManualReviewSeniorAnalyst</th>
<th>ManualReviewAnalyst</th>
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
<td>Read/Write</td>
<td>No access</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
</tr>
<tr>
<td rowspan="2">Account creation</td>
<td>Monitoring</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>No access</td>
<td>Read only</td>
<td>No access</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Rules</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td rowspan="2">Account login</td>
<td>Monitoring</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>No access</td>
<td>Read only</td>
<td>No access</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Rules</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td rowspan="3">Purchase</td>
<td>Monitoring</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>No access</td>
<td>Read only</td>
<td>No access</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Rules</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Support</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>No access</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">Loss Prevention</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>No access</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">Assessments</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">Assessments monitoring</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>No access</td>
<td>Read only</td>
<td>No access</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">Custom assessments</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">Configuration</td>
<td>Read/Write</td>
<td>Read/Write</td>
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
<td colspan="2">Search</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>No access</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
</tr>
<tr>
<td colspan="2">Event Details</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only</td>
<td>Read/write</td>
<td>Read/write</td>
<td>No access</td>
<td>Read/write</td>
<td>Read/write</td>
<td>Read/write</td>
</tr>
<tr>
<td rowspan="3">Case management</td>
<td>Queues</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>Read/write</td>
<td>Read/write</td>
<td>Read/write</td>
</tr>
<tr>
<td>Assign Queues</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>Read/write</td>
<td>Read/write</td>
<td>Read/write</td>
</tr>
<tr>
<td>Report</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Routing rules</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>Read/write</td>
<td>Read/write</td>
<td>No access</td>
</tr>
<tr>
<td rowspan="4">Virtual fraud analyst</td>
<td>Summary</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>No access</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
</tr>
<tr>
<td>Rule analyst</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>No access</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
</tr>
<tr>
<td>Score analyst</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>No access</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
</tr>
<tr>
<td>Threat analyst</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>No access</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
</tr>
<tr>
<td colspan="2">Velocities</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>Read/write</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">External calls</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only</td>
<td>No access</td>
<td>Read/Write</td>
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
<td>Read only</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Support</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">Graph explorer</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>No access</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
</tr>
<tr>
<td colspan="2">Event tracing</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">Data upload</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td rowspan="3">API management</td>
<td>API requests</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Errors</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
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
<td>Read only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td rowspan="3">Integration</td>
<td>Dashboard</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Microsoft Entra Apps</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Device Fingerprinting</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td rowspan="2">Usage</td>
<td>Summary</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Details</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
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
<td>Read only</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td rowspan="2">Subject requests</td>
<td>Search</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Requests</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td rowspan="2">Transaction acceptance booster</td>
<td>Opt in</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read only</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Report</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
  </tr>
<tr>
<td colspan="2">Activity logs</td>
<td>Read only</td>
<td>No access</td>
<td>No access</td>
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

> [!NOTE]
> The **SupportAgent**, **ManualReviewAnalyst**, and **ManualReviewSeniorAnalyst** roles can add items to, or remove items from, **Support lists** (for example, Safe, Block, and Watch) by using the **Event Details** page. However, they can't read or edit the full Support lists page.
> 
> To create a Microsoft Entra application, the user must also be assigned the **Application Administrator**, **Cloud Application Administrator**, or **Global Administrator** role in your Azure tenant.
>
> The user who assigns roles must also be assigned the **Application Administrator**, **Cloud Application Administrator**, **Global Administrator**, **User Administrator**, or **Privileged Role Administrator** role in your Azure tenant.

## Member access

Members can access their [Fraud Protection account](https://dfp.microsoft.com/) and use a Microsoft account to sign in.

## Guest user access

Guest users can access Fraud Protection after they accept an email invitation and sign up or sign in.

To accept an invitation to Fraud Protection, follow these steps.

1. Check your email inbox for an email that has the subject line "\<Name> invited you to access applications within their organization."
2. Select **Accept invitation**.
3. If an existing Microsoft account or related account uses your email address, you are prompted to use that account to sign in. Otherwise, follow the steps to sign up for a new account. After you're signed in, you should have access to Fraud Protection.
4. Return to the invitation email, and write down or bookmark the exact link that appears after the text, "If you accept this invitation, you'll be sent to...." This link is in the format `https://dfp.microsoft.com/.../...`. 
Each time that you access Fraud Protection, you must use this exact link.


## Additional resources

[Configure user access](configure-user-access.md).

[Payment service provider user roles and access](psp-user-roles.md)

[Create a user account in Microsoft Entra ID](/azure/active-directory/manage-apps/add-application-portal-assign-users#create-a-user-account)

[Assign a user account to an enterprise application](/azure/active-directory/manage-apps/add-application-portal-assign-users#assign-a-user-account-to-an-enterprise-application)

[!INCLUDE[footer-include](includes/footer-banner.md)]
