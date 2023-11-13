---
author: weiswang
description: This article provides information about the Configuration.
ms.author: weiswang
ms.date: 11/10/2023
ms.topic: conceptual
search.audienceType:
  - admin
title: Configuration

---

# Configuration overview

Configuration allows you greater flexibility and extensibility to modify UI elements or interfaces within Microsoft Dynamics 365 Fraud Protection to fit your business needs. Configuration currently supports the following feature areas:

- [Case management](configuration.md#case-management-configuration)

Under **Admin Settings**, use the **Configuration** tab to select the assessment and feature for which you want to apply the configuration. This setting is only accessible in the root environment and to users assigned the roles Product Admin and AllAreas Admin as defined in the article, [User roles and access](configure-user-access.md)

## Case management configuration

Case management configuration supports the following areas for configurability:

- **Decision action name and its corresponding action, label, button icon**: Customize the name of the decision button and its corresponding decision action, the ability to enable when fraud labels should be sent to to Fraud protection, and the icon displayed next to the decision action name.
- **Decision reasons**: Customize reasons lists for each decision action.

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

