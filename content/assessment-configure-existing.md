# Assessment configuration overview

You can configure an existing assessment by selecting the assessment in Fraud Protection’s left-hand navigation bar and then clicking its _Configuration_ tab.  This _Configuration_ tab only applies to assessments created using [templates](assessment-create-new.md#assessment-wizard-select-template) and is only visible to users with a minimum of "_Read_" permissions for _Assessments_ as defined in [User roles and access](user-roles-access.md).

If you have "_Read/Write_" permissions to Assessments, you can:

- Create a new label, if one doesn't already exist, and any other observation events that may be relevant to your specific fraud scenario. You can create many observation events from the same observation event template.
- Make edits to the following aspects of the assessment:
  - Assessment schema
  - Assessment friendly name
  - Assessment settings – Rule evaluation behavior, features, and data subject IDs
  - Any existing label and observation events associated with the assessment.
- Share the assessment, allowing a second assessment to call it from another environment using one of the following options:
  - **Private** – Only in the second assessment’s root environment (_default_)
  - **Shared** – Accessible in all environments in the tenant
- Delete the assessment.
  - An assessment can only be deleted in the root environment it was created in. An assessment can't be deleted if a velocity is referencing it, or if the assessment is being shared.
  - Deleting an assessment permanently removes the assessment and its transactional data from your environment and all its child environments. It also drops all cases associated with that assessment across all environments, including the root and children.
  - If an assessment and associated data like rules are deleted in the root environment, the velocities that reference this assessment in child environments show an error in the [Velocities](velocities.md) page. 
