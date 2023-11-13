---
author: weiswang
description: This article provides information about the Configuration
ms.author: weiswang
ms.date: 11/10/2023
ms.topic: conceptual
search.audienceType:
  - admin
title: Configuration

---

# Configuration Overview

Configuration allows you have a greater flexibility and extensibility to modify UI elements or interfaces within Microsoft Dynamics 365 Fraud Protection to fit your business needs. Configuration currently supports the following feature areas:

- [Case management](configuration.md#case-management-configuration)

Under the **Admin Settings**, you can find the **Configuration** tab where you can choose the assessment and feature you want to apply configuration for. This setting is only accessible in the root environment and to users with role Product Admin and AllAreas Admin as defined in the article, [User roles and access](configure-user-access.md)

## Case management configuration

Case management configuration supports the following areas for configurability:

- **Decision action name and its corresponding action, label, button icon**: customize name of the decision button and its corresponding decision action, abililty to enable when to send fraud labels to Fraud protection and icon displayed next to the decision action name
- **Decision reasons**: customize reasons lists for each decision action

To update the configuration, use the JSON editor to update attribute values. When you are ready to apply the configuration, select **Save and Apply** to apply the configuration to selected assessment. To ensure configuration has been applied, please refresh your browser before reviewing cases with new configuration within Case Management.

> [!Note]
> Case management configurations can impact queue creation/editing details page, Search and Case management reports.

### Case management options schema
|Property|Type|Description|
| :--------: | :--------------------------------------: |---------------------|
|sortableBy|Array of strings|**Ready-only**; for Fraud Protection internal use.|
|queueDecisions|Array of CaseManagementDecisionAction|An array of CaseManagementQueueActions. <br /> <br /> Each of which will be displayed as a button for Case Management decisions.|
|defaultDecisionButtonName|String|Action on timeout for queues. <br /> <br />defaultDecisionButtonName can only be values from queueDecision "name".|

### Case management queue actions schema
|Property|Type|Description|
| :--------: | :--------------------------------------: |---------------------|
|name|String|Name of the decision action. <br /> <br /> Minimum of two distinct names are needed.|
|caseAction|Enum <br /> <br /> *Expected values:* <br /> Approve <br /> Reject <br /> None| Fraud Proection decision action. <br /> <br /> Minimum of two distinct caseActions are needed.|
|labelAction|Enum <br /> <br /> *Expected values:* <br /> Fraud <br /> NonFraud <br /> None | Enables you to ingest cases with fraud labels to Fraud Protection.|
|reasons|String| When making a certain decision in manul review cases, you can select specific reasons to be shown in the dropdown. <br /> <br /> Minimum of one reason per caseAction is needed.|
|buttonSentiment|Enum <br /> <br /> *Expected values:* <br /> Positive <br /> Negative <br /> Neutral <br /> Null|Button icon displayed with decision action name. <br /> <br /> Positive: Green checkmark icon <br /> Negative: Red X icon <br /> Neutral: Black circle witha white line icon <br /> Null: no icon|

### Default case management configuration
The following schema is the system default unless you have applied custom configuration:

```json
{
"caseManagementOptions": {
		"sortableBy": [
			"53f445d8-71dd-4a77-b31f-76c7c118ee1c/request/metadata/timestamp"
		],
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

