---
author: josaw1
description: This article provides an overview of how to configure assessments in Fraud Protection.
ms.author: josaw
ms.date: 07/10/2023
ms.topic: conceptual
search.audienceType:
  - admin
title: Assessment configuration overview

---

# Assessment configuration overview

To configure an existing assessment, in the left navigation bar, select the assessment and then select the **Configuration** tab. The **Configuration** tab only applies to assessments created using [templates](assessment-create-new.md#template) and is only visible to users with a minimum of **Read** permissions for **Assessments** as defined in [User roles and access](user-roles-access.md).

If you have **Read/Write** permissions for Assessments, you can:

- Create a new label and any other observation events that may be relevant to your specific fraud scenario. You can create many observation events from the same observation event template.
- Make edits to the following aspects of the assessment:
  - Assessment schema
  - Assessment friendly name
  - Assessment settings including rule evaluation behavior, features, and data subject IDs
  - Any existing label and observation events associated with the assessment
- Share the assessment, allowing it to be called by a second assessment from another environment using one of the following options:
  - **Private** – Only in the second assessment’s root environment (_default_)
  - **Shared** – Accessible in all environments in the tenant
- Delete the assessment:
  - An assessment can only be deleted in the root environment it was created in. An assessment can't be deleted if a velocity is referencing it, or if the assessment is being shared.
  - Deleting an assessment permanently removes the assessment and its transactional data from your environment and all its child environments. All cases associated with that assessment across all environments, including the root and children are dropped.
  - If an assessment and associated data like rules are deleted in the root environment, the velocities that reference this assessment in child environments show an error on the [Velocities](velocities.md) page. 
- Reporting
  - You can setup data filters   to match your business needs, allowing you to analyze your data in various ways within the reports. A default set of data filters will be assigned automatically based on your assessment configuration.
  - You can setup data fields from observation events and labels to show distribution metrics as needed.  
  - By enabling or disabling the "Amount" option, you can choose to show the Amount metric in the reports. You can select specific data attributes to determine how amounts are aggregated for reporting. The “txnAmount” in monetary templates like Purchase, Money Transfer, and Card Payment is considered as the default amount attributes. These default amount attributes will be converted  to USD for aggregation, specifically to unify the currency representation.
  - A limit has been set on report configuration changes to 5 times every 90 days to ensure the highest quality of performance and a consistent user experience. This has been implemented to maintain the integrity and responsiveness of the reports. Please note that it may take up to 24 hours for reports to be generated following the initial transaction. Similarly, enabling or re-enabling a report can result in up to a 24-hour delay before the reports become visible.


[!INCLUDE[footer-include](includes/footer-banner.md)]
