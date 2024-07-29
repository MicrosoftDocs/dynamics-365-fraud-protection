---
author: arj-malhotra
description: This article provides information about roles and user access to Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 07/29/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: User roles and access

---

# User roles and access

This article provides information about roles and user access to Microsoft Dynamics 365 Fraud Protection.

Microsoft Dynamics 365 Fraud Protection offers a defined set of user roles, each of which has access to specific features and functions. Users access Fraud Protection differently, depending on their user role in the organization's Azure tenant. When you add a new user to the system, you can select the roles to assign roles to the user. For information about how to set up user roles and access in Fraud Protection, see [Configure user access](configure-user-access.md).

All the roles in the following list are named as they are named in your production environment. To grant users access to these roles in your sandbox environment, select the version of the role that begins with "Sandbox_". For example, **Sandbox_AllAreas_Admin**.

## Roles

- **Product admin** – This top-level administrative account has full access to your Fraud Protection instance and all the environments in the hierarchy.
- **AllAreas_Admin** – This high-level administrative account has full access to an environment and its child environments Fraud Protection.
- **AllAreasEditor** – A user in this role is a power user who can view all areas and has permissions to use key Fraud Protection tools in an environment and its child environments. However, this role doesn't give access to make user role assignments.
- **AllAreasViewer** – A user in this role can view all areas of Fraud Protection and learn from the data, but can't do uploads or change settings in an environment and its child environments.
- **SupportAgent** – This role provides tailored access to Fraud Protection for support agents who work with your customers. A user in this role can view and work in the support tool, view the ontology, and assign customers to safe lists or block lists in an environment and its child environments.
- **FraudEngineer** – This role provides tailored access for fraud analysts and engineers in your organization who work with Fraud Protection. A user in this role has similar access to a user in the **AllAreasEditor** role. This user can access the data engineering information but doesn't have access to some configuration options in an environment and its child environments.
- **ManualReviewAnalyst** – A user in this role is responsible for reviewing individual transactions and approving or declining them. Manual review analysts have access to the Search tool and queues in Case management.
- **ManualReviewSeniorAnalyst** – In addition to reviewing individual transactions and approving or declining them, a user in this role can also set up routing rules. Manual review senior analysts have access to the Search tool, queues, and Routing rules in Case management.
- **ManualReviewFraudManager** – A user in this role is intended to manage manual review operations for the merchant. A user in this role can assign user access, configure assessment rules, create queues, define routing rules, and view performance reports. 
- **Risk_API** – This role provides access to the API for an environment and its child environments but not to the user-facing tool.
> [!NOTE]
> If the selection of roles that's shown to you differs from the following list, you might be using the payment service provider version of Fraud Protection.In this case, see [Payment service provider user roles and access](psp-user-roles.md) for the list of roles.


## Permissions
Members can access their [Fraud Protection account](https://dfp.microsoft.com/) and use a Microsoft Entra account to sign in. Tables below describe permissions that different roles have on various functionalities within the Fraud Protection portal.


### Assessments
|Permission | Roles |
|-------------|-------------|
|Read/Write|Product Admin, All Areas Admin, All Areas Editor, Fraud Engineer|
|Read-only|All Areas Viewer, Manual Review Fraud Manager|
|No access|Support Agent, Manual Review Analyst, Manual Review Senior Analyst|


### Decision Rules, Post Decision Actions and Branches
| Permission | Roles |
|-------------|-------------|
|Read/Write|Product Admin, All Areas Admin, All Areas Editor, Fraud Engineer, Manual Review Fraud Manager|
|Read-only|All Areas Viewer|
|No access|Support Agent, Manual Review Analyst, Manual Review Senior Analyst|


### Monitoring Report (Assessments)
| Permission | Roles |
|-------------|-------------|
|Read-only|Product Admin, All Areas Admin, All Areas Editor, All Areas Viewer, Fraud Engineer, Manual Review Fraud Manager|
|No access|Support Agent, Manual Review Analyst, Manual Review Senior Analyst|


### Virtual Fraud Analyst
| Permission | Roles |
|-------------|-------------|
|Read/Write|Product Admin, All Areas Admin, All Areas Editor|
|Read-only|All Areas Viewer, Fraud Engineer, Manual Review Fraud Manager|
|No access|Support Agent, Manual Review Analyst, Manual Review Senior Analyst|


### Search, View Transaction Details & Export
| Permission | Roles |
|-------------|-------------|
|Read-only|Product Admin, All Areas Admin, All Areas Editor, All Areas Viewer, Support Agent, Fraud Engineer, Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|


The following table shows the specific read/write permissions that users will have on each page in the Fraud Protection portal, depending on their roles. Along with the sections listed in the table, **Product admin** also has Read/Write permission to the **Admin settings** page, including the **Configuration**, **Search**, **Billing**, and **Subscription** tabs.

<table>
<thead>
<tr>
<th>Section</th>
<th>Sub-page (tab)</th>
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
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Rules</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read-only</td>
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
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Rules</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read-only</td>
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
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Rules</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read-only</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Support</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">Loss Prevention</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
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
<td>Read-only</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">Assessments monitoring</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">Custom assessments</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read-only</td>
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
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
</tr>
<tr>
<td colspan="2">Event Details</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read-only</td>
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
<td>Read-only</td>
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
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>Read/write</td>
<td>Read/write</td>
<td>Read/write</td>
</tr>
<tr>
<td>Report</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Routing rules</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>Read/write</td>
<td>Read/write</td>
<td>No access</td>
</tr>
<tr>
<td rowspan="5">Reporting</td>
<td>Summary</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Rule reports</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Score reports</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Threat report</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Observation report(Assessment Only)</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">Velocities</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read-only</td>
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
<td>Read-only</td>
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
<td>Read-only</td>
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
<td>Read-only</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>No access</td>
<td>Read/Write</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td colspan="2">Graph explorer</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>No access</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
</tr>
<tr>
<td colspan="2">Event tracing</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read-only</td>
<td>Read-only</td>
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
<td>Read-only</td>
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
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Errors</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Ontology</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
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
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>AAD Apps</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read/Write</td>
<td>Read-only</td>
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
<td>Read-only</td>
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
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Details</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
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
<td>Read-only</td>
<td>Read-only</td>
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
<td>Read-only</td>
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
<td>Read-only</td>
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
<td>Read-only</td>
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
<tr>
<td>Report</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>Read-only</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
<td>No access</td>
</tr>
</tbody>
</table>


### Case Management - Queues
| Permission | Roles |
|-------------|-------------|
|Read/Write|Product Admin, All Areas Admin, All Areas Editor, Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|
|Read-only|All Areas Viewer|
|No access|Support Agent, Fraud Engineer|


### Case Management - Queues : Assign users
| Permission | Roles |
|-------------|-------------|
|Read/Write|Product Admin, All Areas Admin, All Areas Editor, Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|
|No access|All Areas Viewer, Support Agent, Fraud Engineer|


### Case Management - Reviewing Cases
| Permission | Roles |
|-------------|-------------|
|Read/Write|Product Admin, All Areas Admin, All Areas Editor, Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|
|Read-only|All Areas Viewer|
|No access|Support Agent, Fraud Engineer|


### Case Management - Report
| Permission | Roles |
|-------------|-------------|
|Read-only|Product Admin, All Areas Admin, All Areas Editor, All Areas Viewer, Manual Review Fraud Manager|
|No access|Support Agent, Fraud Engineer, Manual Review Analyst, Manual Review Senior Analyst|


### Routing rules, Functions, Velocities, External Calls, External Assessments, Custom Lists & Support Lists
| Permission | Roles |
|-------------|-------------|
|Read/Write|Product Admin, All Areas Admin, All Areas Editor, Fraud Engineer, Manual Review Fraud Manager|
|Read-only|All Areas Viewer|
|No access|Support Agent, Manual Review Analyst, Manual Review Senior Analyst|
> [!NOTE]
> The Support Agent role can't access the **Support list** page, but can modify the list from **Transaction detail** page, on the **Support** tab under **Purchase assessment**.


### Event Tracing
| Permission | Roles |
|-------------|-------------|
|Read/Write|Product Admin, All Areas Admin|
|Read-only|All Areas Editor, All Areas Viewer|
|No access|Support Agent, Fraud Engineer, Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|


### Data Upload
| Permission | Roles |
|-------------|-------------|
|Read/Write|Product Admin, All Areas Admin, All Areas Editor, All Areas Viewer, Fraud Engineer|
|No access|Support Agent, Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|


### API Management
| Permission | Roles |
|-------------|-------------|
|Read-only|Product Admin, All Areas Admin, All Areas Editor, All Areas Viewer, Fraud Engineer|
|No access|Support Agent, Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|


### Templates
|Template Type| Permission | Roles |
|-------------|-------------|-------------|
|Rule|Read/Write/Export|Product Admin, All Areas Admin, All Areas Editor, Fraud Engineer, Manual Review Fraud Manager|
|Rule|Read-only|All Areas Viewer|
|Rule|No access|Support Agent, Manual Review Analyst, Manual Review Senior Analyst|
|Assessment|Read/Write/Export|Product Admin, All Areas Admin, All Areas Editor|
|Assessment|Read-only|All Areas Viewer, Manual Review Fraud Manager|
|Assessment|No access|Support Agent, Fraud Engineer, Manual Review Analyst, Manual Review Senior Analyst|
|Environment|Read/Write/Export|Product Admin, All Areas Admin, All Areas Editor|
|Environment|Read-only|All Areas Viewer|
|Environment|No access|Support Agent, Fraud Engineer, Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|
  > [!NOTE]
  > - To create a template from a resource, user must have read permission on the resource as well as write permission on the template.
  > - To create a resource using a template,  user musthave write permission on the resource as well as read permission on the template. 

### Graph Explorer
| Permission | Roles |
|-------------|-------------|
|Read-only|Product Admin, All Areas Admin, All Areas Editor, All Areas Viewer, Support Agent, Fraud Engineer|
|No access|Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|


### Integration-Dashboard
| Permission | Roles |
|-------------|-------------|
|Read-only|Product Admin, All Areas Admin, All Areas Editor, All Areas Viewer, Fraud Engineer|
|No access|Support Agent, Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|


### Integration- Entra Applications and SSL Certificate
| Permission | Roles |
|-------------|-------------|
|Read/Write|Product Admin, All Areas Admin, All Areas Editor, Fraud Engineer|
|Read-only|All Areas Viewer|
|No access|Support Agent, Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|
> [!NOTE]
> To create a Microsoft Entra application, the user must also be assigned the Application Administrator, Cloud Application Administrator, or Global Administrator role in your Azure tenant.


### Settings - Usage
| Permission | Roles |
|-------------|-------------|
|Read-only|Product Admin, All Areas Admin, All Areas Editor, All Areas Viewer|
|No access|Support Agent, Fraud Engineer, Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|


### Settings - Activity Logs
| Permission | Roles |
|-------------|-------------|
|Read-only|Product Admin, All Areas Admin|
|No access|All Areas Editor, All Areas Viewer, Support Agent, Fraud Engineer, Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|


### Settings - Access Management (Users & Microsoft Entra Groups)
| Permission | Roles |
|-------------|-------------|
|Read/Write|Product Admin, All Areas Admin, Manual Review Fraud Manager|
|Read-only|All Areas Editor, All Areas Viewer|
|No access|Support Agent, Fraud Engineer, Manual Review Analyst, Manual Review Senior Analyst|
> [!NOTE]
> All Areas Admin can assign all roles except Product Admin.
> Manual Review Fraud Manager can only assign these roles: ManualReviewFraudManager, ManualReviewAnalyst, ManualReviewSeniorAnalyst.


### Settings - Subject Requests: Submit new requests
| Permission | Roles |
|-------------|-------------|
|Read/Write|Product Admin, All Areas Admin, All Areas Editor, Fraud Engineer|
|No access|All Areas Viewer, Support Agent, Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|


### Settings - Subject Requests:  View previous requests
| Permission | Roles |
|-------------|-------------|
|Read-only|Product Admin, All Areas Admin, All Areas Editor, All Areas Viewer, Fraud Engineer|
|No access|Support Agent, Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|


### Settings - Transaction acceptance booster
| Permission | Roles |
|-------------|-------------|
|Read/Write|Product Admin, All Areas Admin|
|Read-only|All Areas Editor, All Areas Viewer|
|No access|Support Agent, Fraud Engineer, Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|


### Notifications
| Notification Type | Roles that have access to view & dismiss  |
|-------------|-------------|
|Environment Management, Event tracing & Subscription Expiry|Product Admin, All Areas Admin|
|Subject requests, SSL certificate & External call|Product Admin, All Areas Admin, All Areas Editor, Fraud Engineer|
|Actions|Product Admin, All Areas Admin, All Areas Editor, Fraud Engineer|
|Search|Product Admin, All Areas Admin, All Areas Editor, All Areas Viewer, Support Agent, Fraud Engineer, Manual Review Analyst, Manual Review Fraud Manager, Manual Review Senior Analyst, |
|Notes|Product Admin, PSP Admin, Fraud Manager, Fraud Supervisor, Fraud Analyst, Manual Review Agent, Customer Service Support|


### Manage Environments - Create and Delete Environments
| Permission | Roles |
|-------------|-------------|
|Read/Write|Product Admin, All Areas Admin|
|No access|All Areas Editor, All Areas Viewer, Support Agent, Fraud Engineer, Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|
> [!NOTE]
> All Areas Admin can't create root (top-level) environments. They can only create children environments.


### Manage Environments - Update Environments
| Permission | Roles |
|-------------|-------------|
|Read-only|Product Admin, All Areas Admin, All Areas Editor|
|No access|All Areas Viewer, Support Agent, Fraud Engineer, Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|
> [!NOTE]
> Updates include updating name and tags, and assigning APIs.


### Admin Settings - Subscription & Billing
| Permission | Roles |
|-------------|-------------|
|Read-only|Product Admin|
|No access|All Areas Admin, All Areas Editor, All Areas Viewer, Support Agent, Fraud Engineer, Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|


### Admin Settings - Configuration
| Permission | Roles |
|-------------|-------------|
|Read-only|Product Admin, All Areas Admin|
|No access|All Areas Editor, All Areas Viewer, Support Agent, Fraud Engineer, Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|


### Loss Prevention
| Permission | Roles |
|-------------|-------------|
|Read-only|Product Admin, All Areas Admin, All Areas Editor, All Areas Viewer, Fraud Engineer|
|No access|Support Agent, Manual Review Analyst, Manual Review Senior Analyst, Manual Review Fraud Manager|


## Guest user access
Guest users can access Fraud Protection after they accept an email invitation and sign up or sign in. To accept an invitation to Fraud Protection, follow these steps.

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
