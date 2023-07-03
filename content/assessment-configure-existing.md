# Assessment configuration overview

You can configure an existing assessment by selecting the assessment in Fraud Protection’s left-hand navigation bar and then clicking its _Configuration_ tab.  This _Configuration_ tab only applies to assessments created using [templates](assessment-create-new.md#assessment-wizard-select-template) and is only visible to users with a minimum of "_Read_" permissions for _Assessments_ as defined in [User roles and access](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/configure-user-access).

If you have "_Read/Write_" permissions to Assessments, you will also be able to:

- Create a new label (if one does not already exist) and any additional observation events that may be relevant to your specific fraud scenario. Please note you can create many observation events from the same observation event template.
- Make edits to the following aspects of the assessment:
  - Assessment schema
  - Assessment friendly name
  - Assessment settings – rule evaluation behavior, features, data subject IDs
  - Any existing label and observation events associated with the assessment.
- Share the assessment, allowing a second assessment to call it from another environment using one of the following options:
  - **Private** – only in the second assessment’s root environment (_default_)
  - **Shared** – accessible in all environments in the tenant
- Delete the assessment.
  - Deleting an assessment will permanently remove the assessment and its transactional data from your environment and all its child environments.
  - For more details on deleting an assessment in a multi-hierarchy environment, see [Manage environments](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/manage-psp-environments).
  - An assessment cannot be deleted if a velocity is referencing it or if it is being shared.
