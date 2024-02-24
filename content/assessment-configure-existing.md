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
- Share the assessment, allowing it to be called by another assessment, using one of the following options:
  - **Private** – Only in the second assessment’s root environment (_default_)
  - **Shared** – Accessible in all environments in the tenant
  - Provide the sample response by manually adding it in the Add sample response pane in the Sharing settings tile on the Configuration page. Sample response must be provided in JSON format. The sample response fields provided here will be used to enable IntelliSense on these fields in the rule editor.  To learn more about how to call a Shared or Private assessment from another assessment, please visit [External assessments](external-assessments.md)
allowing it to be called by a second assessment from another environment using one of the following options:
- Delete the assessment:
  - An assessment can only be deleted in the root environment it was created in. An assessment can't be deleted if a velocity is referencing it, or if the assessment is being shared.
  - Deleting an assessment permanently removes the assessment and its transactional data from your environment and all its child environments. All cases associated with that assessment across all environments, including the root and children are dropped.
  - If an assessment and associated data like rules are deleted in the root environment, the velocities that reference this assessment in child environments show an error on the [Velocities](velocities.md) page. 


[!INCLUDE[footer-include](includes/footer-banner.md)]
