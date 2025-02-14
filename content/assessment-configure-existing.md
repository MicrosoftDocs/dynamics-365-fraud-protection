---
author: josaw1
description: This article provides an overview of how to configure assessments in Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 07/24/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Assessment configuration overview

---

# Assessment configuration overview

[!include[deprecation](includes/deprecation.md)]

To configure an existing assessment, in the left navigation bar, select the assessment and then select the **Configuration** tab. The **Configuration** tab only applies to assessments created using [templates](assessment-create-new.md#template) and is only visible to users with a minimum of **Read** permissions for **Assessments** as defined in [User roles and access](user-roles-access.md).

If you have **Read/Write** permissions for Assessments, you can:

- Create a new label and any other observation events that may be relevant to your specific fraud scenario. You can create many observation events from the same observation event template.
- Make edits to the following aspects of the assessment:
  - Assessment schema
  - Assessment friendly name
  - Assessment settings including rule evaluation behavior, features, and data subject IDs
  - Any existing label and observation events associated with the assessment
- Share the assessment, allowing it to be called by another assessment, using one of the following options:
  - **Private** – Can be called only from the same root environment (_default_)
  - **Shared** – Accessible in all environments in the tenant
  - Provide the sample response in the **Add sample response** pane, in the *Sharing* setting. The sample response must be provided in JSON format. The sample response fields you provide are used to enable descriptions (tooltips) and suggestions for autocomplete when they are referenced in a rule. For more information about how to call a shared or private assessment from another assessment, see [External assessments](external-assessments.md).
- Delete the assessment:
  - An assessment can only be deleted in the root environment it was created in. An assessment can't be deleted if a velocity is referencing it, or if the assessment is being shared.
  - Deleting an assessment permanently removes the assessment and its transactional data from your environment and all its child environments. All cases associated with that assessment across all environments, including the root and children are dropped.
  - If an assessment and associated data like rules are deleted in the root environment, the velocities that reference this assessment in child environments show an error on the [Velocities](velocities.md) page. 
- Create reports:
  - You can set up data filters to match your business needs. Data filters enable you to analyze your data in various ways within reports. Default data filters are automatically assigned based on your assessment configuration.
  - You can set up data fields from observation events and labels to display distribution metrics as needed.  
  - By enabling or disabling the **Amount** option, you can display the Amount metric in your reports. You can select specific data attributes to determine how amounts are aggregated for reporting. The **txnAmount** in monetary templates like Purchase, Money Transfer, and Card Payment is considered to be default Amount attributes.
  - Report configuration changes are limited to five times every 90 days to ensure the highest quality of performance and a consistent user experience. This limit maintains the integrity and responsiveness of the reports. It may take up to 24 hours to generate reports after the initial transaction. Similarly, if you enable or re-enable a report, a 24-hour delay may result in when the reports are visible.


[!INCLUDE[footer-include](includes/footer-banner.md)]
