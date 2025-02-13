---
author: weiswang
description: This article provides information about the Configuration.
ms.author: weiswang
ms.date: 01/22/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Configuration
---

# Configuration overview

[!include[deprecation](includes/deprecation.md)]

Configuration allows you greater flexibility and extensibility to modify UI elements or interfaces within Microsoft Dynamics 365 Fraud Protection to fit your business needs. Configuration currently supports the following feature areas:

- [Case management](configuration.md#case-management-configuration)
- [Actions](configuration.md#action-configuration)

Under **Admin Settings**, use the **Configuration** tab to select the assessment and feature to which you want to apply the configuration. This setting is only accessible in the root environment and to users assigned the roles Product Admin and AllAreas Admin as defined in the article, [User roles and access](configure-user-access.md)

## Case management configuration

Case management configuration supports the following areas for configurability:

- **Decision action name and its corresponding action, label, button icon**: Customize the name of the decision button and its corresponding decision action, the ability to enable when fraud labels should be sent to Fraud protection, and the icon displayed next to the decision action name.
- **Decision reasons**: Customize reasons lists for each decision action.
- **FQL action**: Trigger an External Call when you click a decision button in Case Management.

To update the configuration, use the JSON editor to update attribute values. When you're ready to apply the configuration, select **Save and Apply** to apply the configuration to the selected assessment. To ensure the configuration is applied, refresh your browser before reviewing cases with new configurations in Case management.

> [!NOTE]
> Case management configurations can impact queue creation/editing details page, Search and Case management reports.

### Case management options schema
|Property|Type|Description|
| :--------: | :--------------------------------------: |---------------------|
|sortableBy|Array of strings|**Ready-only**; for Fraud Protection internal use.|
|queueDecisions|Array of CaseManagementDecisionAction|An array of CaseManagementQueueActions. <br /> <br /> Each of which are displayed as a button for Case Management decisions.|
|defaultDecisionButtonName|String|Action on timeout for queues. <br /> <br />defaultDecisionButtonName can only be values from queueDecision "name".|

### Case management queue actions schema
|Property|Type|Description|
| :--------: | :--------------------------------------: |---------------------|
|name|String|Name of the decision action. <br /> <br /> Minimum of two distinct names are needed.|
|caseAction|Enum <br /> <br /> *Expected values:* <br /> Approve <br /> Reject <br /> None| Fraud Protection decision action. <br /> <br /> Minimum of two distinct caseActions are needed.|
|labelAction|Enum <br /> <br /> *Expected values:* <br /> Fraud <br /> NonFraud <br /> None | Enables you to ingest cases with fraud labels to Fraud Protection.|
|reasons|String| When making a certain decision in manual review cases, you can select specific reasons to be shown in the dropdown. <br /> <br /> Minimum of one reason per caseAction is needed.|
|buttonSentiment|Enum <br /> <br /> *Expected values:* <br /> Positive <br /> Negative <br /> Neutral <br /> Null|Button icon displayed with decision action name. <br /> <br /> Positive: Green checkmark icon <br /> Negative: Red X icon <br /> Neutral: Black circle with a white line icon <br /> Null: no icon|
|fqlAction|String <br /> <br /> *Entry Exemple:* <br /> "fqlAction" : "fqlAction" : "DO External.CallWebService() when true"| Example value for fqlAction that would result in the External Call "CallWebService" being called every time corresponding CM Decision button is selected.|

### Default case management configuration
The following schema is the system default unless you apply a custom configuration:
```json
{
"caseManagementOptions": {
		"queueDecisions": [
			{
				"name": "Approve",
				"caseAction": "Approve",
				"labelAction": "None",
				"reasons": [
					"Wrong decision",
					"Account rehabilitated",
					"Business policy",
					"Verified customer",
					"Test account",
					"Other",
					"Low risk",
					"Not enough info to claim fraud"
				],
				"buttonSentiment": "Positive",
				"fqlAction": null
			},
			{
				"name": "Reject",
				"caseAction": "Reject",
				"labelAction": "None",
				"reasons": [
					"Stolen card",
					"Compromised account",
					"Collusion",
					"Fraud business",
					"Business policy violation",
					"Unauthorized activity",
					"Friendly fraud",
					"Abuse",
					"Suspected fraud",
					"Other"
				],
				"buttonSentiment": "Negative",
				"fqlAction": null
			}
		],
		"defaultDecisionName": "Approve"
	}
}  
```

## Action configuration

Fraud Protection enables you to configure custom actions that execute FQL within a given context. Action configuration supports the following contexts:

- **AssessmentEvent**: Actions appear every time an Assessment Event is shown (for example, Search results page, Search individual transaction page). Actions can be applied to one or many transactions.


To create an action, go to **Actions** on the **Configuration** page, then select **...** -> **Create an action**. Use the JSON editor to update the template to configure your action. When you're ready to create the action, select **Save and Apply**. To ensure the action is configured, refresh your browser before applying an action for the first time. Actions can only be configured at a root environment level by an admin. Once an action is configured, it is visible to all environments underneath the root environment.

### Actions configuration schema
|Property|Type|Description|
| :--------: | :--------------------------------------: |---------------------|
|name|String|Name of the action. Action names must be unique.|
|context -> type|Enum <br /> <br /> *Expected values:* <br /> "AssessmentEvent"|The context in which this action is displayed.|
|context -> ids|Array of strings|The specific ids for which the action is displayed. For AssessmentEvent, the ids are the Assessment API names.|
|fql|String <br /> <br /> *Entry Example:* <br /> "fql" : "DO Assessment.SendLabel(@eventId, \"Fraud\", \"Some Reason\")"|The FQL that the action executes when invoked.|

### Actions functions schema
|Function|Description|Parameters|
| :--------: | :--------------------------------------: | :--------------------: |
|DO Assessment.SendLabel(@eventId, Enum *label*, string *reason*)|Send a label for a transaction.|label: <br /> *Expected values:* <br /> "Fraud" <br /> "NonFraud" <br /> "None" <br /> <br /> reason: reason for applying label.|

### Default actions template
The following schema is the default Actions template when you create an action:
```json
{
	"name": "Put some name here....",
	"context": {
		"type": "AssessmentEvent",
		"ids": [
			"Assessment apiName (purchase, for example)",
			"add more apiNames here"
		]
	},
	"fql": "DO Assessment.SendLabel(@eventId, \"Fraud\", \"Some Reason\")"
}
```

