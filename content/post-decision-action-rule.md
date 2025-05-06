---
author: swasif23
description: This article provides an overview of the Post-decision action rules feature in Microsoft Dynamics 365 Fraud Protection.
ms.author: swasif
ms.date: 04/10/2024
ms.topic: article
search.audienceType:
  - admin
title: Post-decision Rules
---

# Post-decision Action Rules

[!include[deprecation](includes/deprecation.md)]

In addition to Decision rules [Manage rules](rules.md), Fraud Protection also allows you to configure Post-decision action rules for an assessment. Post-decision action rules are evaluated after Decision rules, but before the API response has been returned. These rules can be used to perform actions that you want to take **each time an assessment is evaluated**. You can use the decision of the assessment call in an action rule also. For example, if you always send additional information as part of your API response anytime a particular decision is taken, or if you always send or receive data from an External Call every time assessment is evaluated. 

> [!NOTE]
> Action rules are available for Assessments only.

## Defining an action rule

Action rules consist of clauses, and are defined by the **DO** and **WHEN** keywords. They have the following basic structure.

```FraudProtectionLanguage
DO <action>
WHEN <condition>
```

DO is a keyword unique to action rules. You can't use this keyword in Decision rules.
Only Action functions can be used following the DO keyword. For more information on available Action functions, see [Language reference guide](fpl-lang-ref.md#model-functions)

### Example

```FraudProtectionLanguage
DO SetResponse(test=true) 
WHEN Response.Decision() == "approve"
```
If the assessment call decision is Approve, the API response will show following fields:

```FraudProtectionLanguage
"customProperties": {
        "test": true
    },
``` 
•	Response.Decision() allows you to access the decision that was made on the assessment call.
•	SetResponse() method can only be use after DO keyword. It adds key value pairs to API response.  

> [!NOTE]
> DO keyword and SetResponse method are available in action rules only.

#### SetResponse Syntax
|Function call|API response in Assessments|
|-------------------------|-------------------|
|SetResponse(a="b", x="y")| "CustomProperties": {<br> &nbsp;&nbsp;&nbsp;&nbsp;"a" : "b",<br>&nbsp;&nbsp;&nbsp;&nbsp;"x" : "y"<br>}</br>|
|SetResponse("newSection", a="b", x="y")|"CustomProperties": {<br> &nbsp;&nbsp;&nbsp;&nbsp; "newSection":{<br> &nbsp;&nbsp;&nbsp;&nbsp; "a" : "b",<br> &nbsp;&nbsp;&nbsp;&nbsp; "x" : "y"<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>}</br>|

## Create and Manage Post-decision Action Rules

To create or manage action rules, go to **Rules** tab. 
To create a new Post-Decision Action rule, select **+ New rule**, and then select **Post-decision action**.

 - No rule evaluation is available in debugging experience.
 - No visual view is available for action rules. 

The **Rules** tab shows a list of the rules that have been configured for an assessment type. These rules are divided into three sections: **Post-decision actions**, **Published Rules** and **Drafts**.

You can view the following information for each rule or draft:
- The name
- The rule type (Decision rule -or- Post-decision action)
- The condition that you created
- The status: Active or Inactive

You can also select the tile for each rule to expand it and show additional information. Here are some examples:
-	The description
-	The number of clauses in the rule
-	Who last updated the rule
-	When the rule was last updated

> [!NOTE]
> On the **Rules** tab, published rules are listed in the order that they are run in.

## Rule evaluation behavior 

In a multi-hierarchy environment, rules are executed in the following order:
1.	Evaluate all active parent Decision rules.
2.	Evaluate all active child Decision rules.
3.	Evaluate all active parent Post-decision Action rules.
4.	Evaluate all active child Post-decision Action rules.

## Post-decision Action Rules Examples
### Calling an external call 
```FraudProtectionLanguage
DO SetResponse(visibility = External.Weather("seattle").visibility)
```
### Calling a shared assessment
```FraudProtectionLanguage
LET $response = Assessments.VerifyCustomer.evaluate(user = @@"user")
DO SetResponse(test=true)
WHEN $response.decisionDetails.MerchantRuleDecision =="Approve"
```




