---
author: yvonnedeq
description: This topic provides details on how to use rules.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 04/03/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Manage Rules

---

# Manage Rules

## Overview

Dynamics 365 Fraud Protection gives you the flexibility to create custom rules based on observed patterns, policies, or business objectives. Custom rules enable your analysts to write business logic for automated decision making and to customize this logic to meet your unique business needs. Rules use a combination of inputs including values in the event request payload and AI-based scores to assess the risk of an event. You can configure rules to convert the assessment into a decision such as ,accept, block, review, or challenge events based on these inputs.  

> [!NOTE]
> You cannot view or create rules in the INT environment. You must use the PROD environment. 

##  Access the Rules management page

You can create custom rules and manage existing rules on the Rules page. 

- To create and manage rules related to purchases, click **Purchase protection** and then click **Rules** on the left navigation.

- To create and manage rules related to accounts, click **Account protection** and then click the **Rules** on the left navigation.

The **Rules** page for **Account protection** has a tab for each assessment type:

-  On the **Account creation** tab, you can create rules that run on account creation events.
-  On the **Account login** tab, you can create rules that run on account login events.

The **Rules** page displays a list of all the rules configured for an event type. You can view the following information for each rule:

-  The  [name](rules.md#details-name-and-description) of the rule.
-  The [condition](rules.md#conditions) you creeated for the rule.
-  The [status](rules.md#status) of the rule(*active*, *inactive*, or *draft*).
-  The [description](rules.md#details-name-and-description) of the rule.
-  The [number of clauses](rules.md#clauses) in the rule.

> [!NOTE]
>The [order](rules.md#understand-rule-ordering) in which rules are listed on the **Rules** page determines the order in which the rules are executed. 

## Components of a rule

A rule consists of:
-  A [name and description](rules.md#details-name-and-description) that describe the purpose of the rule.
-  A [status](rules.md#status) that indicate its current state.
-  A [sample](rules.md#samples) that assists you in writing and evaluating the rule.
-  Components that enable you to build the logic to automatically approve, reject, challenge, and review certain events. This includes:
    -  A [condition](rules.md#conditions).
    -  One or more of the following types of [clauses](rules.md#clauses):
       -  [Prior to all scoring clauses](rules.md#prior-to-all-scoring-clauses).
       -  [Post bot scoring clauses](rules.md#post-bot-scoring-clauses).
       -  [Post risk scoring clauses](rules.md#post-risk-scoring-clauses).

### Details (name and description)

When you create a rule, you can add details that make it easily identifiable for you and your team, such as a name and description.

Rule names must be unique and do not have to be case sensitive. However, you cannot create rules using the same text with a different case (for example, *riskycountry*, *RiskyCountry*, and *RISKYCOUNTRY*). Fraud Protection does not recognize case and therefore considers these examples to be the same name.
 
### Status

#### Active or inactive rules

Once a rule has been published, it can be set to either *Active* or *Inactive*. 
- If a rule is *Active*, it affects real time production traffic. This means that all events of this type are evaluated against the rule. 
- If a rule is *Inactive*, it does not affect production traffic. 

#### Draft rules

When you create or modify rules, Fraud Protection automatically saves your work in progress with the status of *Draft*.

- If you create a new rule which has never been published before, Fraud Protection automatically sets the rule status to **Draft only**.
- If you make changes to a rule that has previously been published, your modifications are also saved in progress. Fraud Protection automatically sets the rule status as either **Active (with Draft)** or **Inactive (with Draft)**, depending on the status of the original published rule.

Rules with draft status are accessible only to the author. If you want to share your rules with your team, you must publish them.

#### Samples
When you create or edit a rule, the **Sample** panel displays on the right side of the page. This panel has two sections: *payload sample* and *score sample*. 

##### Payload sample 

The payload sample is an example of the fields that can be included in an API request for a purchase, account creation, or account login event, and can be used in your rule. 

The payload sample is provided as an example and may not accurately reflect the data you send to Fraud Protection. For example, the sample may include fields you do not send, and may not include custom data fields that you do send. You can, however, still use these custom fields in your rules as you would any other payload variable. 

##### Score Sample

The score sample contains the scores generated from Fraud Protection’s AI models. You can reference these score variables in rules after the associated AI model generating the score has run. For example, you can use **@botScore** only after the bot evaluation has run, and **@riskScore** only after the risk evaluation has run. For more information see  [Clauses](rules.md#clauses).

#### Edit the sample
In order to test that your rule works as expected on a variety of events, you can modify the sample and [evaluate your rule](rules.md#evaluate-example) against it. All values in both the payload sample and score sample can be modified. However, when you change a sample, it does not affect which data yousend or do not send to Fraud Protection.

Any changes you make to a sample are saved and become a part of the rule. This means that if someone else accesses the sample, it will include changes you made. To undo all changes that have ever been made to the sample at any time, by anyone, click **Revert**. 


### Conditions

A condition starts with the keyword **WHEN** and is followed by a valid Boolean expression, which means the statement must evaluate to either *True* or *False*. The condition determines which rule is evaluated and can be used as a mechanism to group related business logic. For example, this is a valid condition:

    WHEN @productType == “Digital”

Clauses that follow this condition can be used to configure fraud strategy pertaining to digital product transactions only. 

Conditions are optional fields within a rule, and if you want the rule to apply to all events, do not enter a condition. For information on how conditions are used in rule ordering, see [Rule ordering](rules.md#understand-rule-ordering).

### Clauses

Clauses are the building blocks of rules and contain the heart of your fraud strategy. They use values in the event payload with Fraud Protection’s AI scores to accept, reject, review, or challenge events. They follow the basic structure of: 

    RETURN *decision* 
    WHEN *condition is true*

You can create a clause to return a decision of Approve, Reject, Challenge, or Review, and include optional parameters to send more information about the [decision](fpl-lang-ref.md).

Everything following the WHEN keyword must evaluate to either True or False. This Boolean expression can be formed using a combination of values from the [event payload](rules.md#clauses), [user-defined lists](lists.md), and [AI-based bot and risk scores](rules.md#post-bot-scoring-clauses). 

For information about the syntax used for writing clauses see the [Rules language guide](fpl-lang-ref.md).

Clauses run sequentially in the order they are displayed on the page. Click the arrows to the right of each clause to re-order a clause. 

When a clause is triggered (that is, the **WHEN** statement returns True), the decision specified in the **RETURN** statement is returned, and no subsequent clauses are run. If a condition matches the decision but no clause within the rule is triggered, by default the rule is executed, as shown in the following example. 

    RETURN Approve(“NO_CLAUSE_HIT”).

The sequential ordering of clauses is divided into three distinct sections: *Pre-Score*, *Post-Bot Score* (which is applicable only for account creation and account login rules), and *Post-Risk Score*. These sections indicate when the clause is run relative to Fraud Protection’s advanced, adaptive AI score generation. 

#### Prior-to-all-scoring clauses

Prior-to-all-scoring clauses are run before Fraud Protection’s AI models are run, and thus before any bot or risk assessment scores have been generated. These clauses can use any combination of fields sent as part of the event payload, as well contained in [Lists](lists.md), and can be configured to implement embargo, geofencing, or other business policies. For example, the following clause enables you review purchases whenever a user buys a product outside of the market in which they are located:

    RETURN Review("location inconsistency") 
    WHEN Geo.MarketCode(“@device.ipAddress”) != “@productList.market”
 
You can also write a clause in this section to reference lists. For example, if you have a custom list titled *Risky Emails* the following clause enables you to reject events if the user’s email appears on the list. 

    RETURN Reject ("risky email") 
    WHEN ContainsKey ("Risky Emails", "Emails", @email)

For information about the syntax for referencing lists in rules, the [Rules language guide](fpl-lang-ref.md).

#### Post-bot-scoring clauses

Post-bot-scoring clauses are run after Fraud Protection’s  AI models have generated a bot score for the event. This score maps to the probability that a bot initiated the event. This score is a number between 0 and 999, with a higher score indicating a higher bot probability. 

In post-bot-scoring clauses, you can use this score (referenced with @botScore), in conjunction with other fields from the payload and in Lists to make decisions. For example, the following clause enables you to reject events from a specific email domain with a bot score greater than 700. 

    RETURN Reject()
    WHEN @email.EndsWith("@contoso.com") && @botScore > 700

> [!NOTE]
>Post-bot-scoring clauses and the @botScore variable are available only for account protection rules. 

#### Post-risk-scoring clauses

The machine learning model in Fraud Protection evaluates every transaction using advanced  AI. It then assigns a risk score. This score is a number between 0 and 999. The higher the risk score, the higher the perceived risk.

In post-risk-scoring clauses, you can use this score, which is referenced with @riskScore, in conjunction with other fields from the payload to make decisions. For example, the following clause enables you to reject expensive transactions with a risk score greater than 700. 

    RETURN Reject(“high price and risk score”)
    WHEN @purchasePrice >= 199.99 && @riskScore > 700

## Understand rule ordering

The **Rules** page for an event (purchase, account login, or account creation) displays a list of all the rules you have configured for that event. The order of these rules is important because an event runs through each rule condition in the order that they appear on the Rules page, until a condition is matched. Once a condition is matched, the selected rule is evaluated. 

For example, if you configure the following three purchase rules:

|Name	|Condition |Status|
|------|---------|------|
|Rule1  |WHEN @country == “US”    |Active|
|Rule2 	|WHEN @username == “Kayla    |Inactive|
|Rule3 	|WHEN @product == “Xbox”    |Active|

The following behavior would hold true:
-  Since Rule2 has a status of *Inactive*, it is never evaluated against real time production traffic.
-  If a customer makes a purchase and they are in the US, only Rule1 is evaluated.
-  If a customer makes an Xbox purchase and they are in the US, only Rule1 is evaluated.
-  If a customer makes an Xbox purchase and they are outside of the US, only Rule3 is evaluated.
-  If a customer makes a non-Xbox purchase and they are outside of the US, no rules are evaluated.

If no rules are evaluated because no conditions match the event, by default, Fraud Protection then executes: 

    RETURN Approve(“NO_RULE_HIT”)

For information on how to reorder rules, see [Understand rule ordering](rules.md#understand-rule-ordering).

## Create a new rule
You can create rules to make decisions for purchase, account creation, and account login events.

> [!NOTE]
>When you create a new rule, it displays at the bottom of the Rules management page. You can move the rule to a different position on the list of rules at any time. For more information, see [Understand rule ordering](rules.md#understand-rule-ordering).


#### To create a new rule:

1. Navigate to the [Rules management page](rules.md#access-the-rules-management-page).
1. Click **New Rule**.
1. (Optional) Click **Rename**, and then add a name and description so that the rule is easily identifiable to you and your team.
    Fraud Protection also prompts you to add a name and description when you publish your rule.
1. Add a [condition](rules.md#conditions) to your rule.

1. To create a new [clause](rules.md#clauses) from scratch, click **+ new clause**, located under the appropriate clause section.

    Or, to create a new clause using a pre-existing template:
    
    1. Click the arrow to the right of **New Clause**. 
        Fraud Protection displays a short list of templates. 
            
    1. To display the full selection of templates and their titles, descriptions, and contents, click **See all**. 
        
    1. Select a clause template as a starting point to create your own fraud logic in the clause. 
        
    You can modify all values in the template to suit your business requirements. 
    
1. To [evaluate your rule](rules.md#evaluate-a-rule) and ensure it works as expected, click **Expand** on the bottom right of the **Rules** page to expand the evaluation panel.
1. To publish your rule, click **Publish**, change the name, description, and status in the confirmation dialog, and then click **Publish**.
 1. You can set the [status](rules.md#status) to either **Active** or **Inactive**.
1. To move the rule to a new position on the order list: 
    1. Navigate to the **Rules** management page.
    1. Select the rule, drag it to its new position, and then click **Save order**. 

## Manage existing rules
You can perform the following operations on an existing rule on the Rules management page:
-	[Rename](rules.md#update-the-name-and-description-of-a-rule)
-	[Activate or Deactivate](rules.md#change-the-status-of-a-rule)
-	[Delete](rules.md#delete-a-rule)
-	[Clone](rules.md#clone-an-existing-rule)
-	[Edit](rules.md#edit-an-existing-rule)
 
### Update the name and description of a rule

To update the name and description of a rule, select a rule, click **Rename**, and then enter a unique name and description.

### Change the status of a rule

To change the status of a rule, select a rule, and then click **Activate** or **Deactivate**.

### Delete a rule

To delete a rule, select a rule, and then click **Delete**. When you delete a rule, the action cannot be undone. 

### Clone an existing rule

When you clone a rule, you create a copy of an existing rule that you can modify and save as a new rule.

#### To clone a rule:
1. Select a rule, and then click **Clone**. 
  This action creates a copy of the selected rule and automatically sets the status to **Inactive**. 
1. Update the rule, and then click **Publish**. 
1. By default, the new rule displays at the bottom of the page. To move the rule to a new position: 
  1. Navigate to the **Rules** management page.
  1. Select the rule, drag it to its new position, and then click **Save order**. 

### Edit an existing rule
When you modify a rule that has been published, Fraud Protection saves the changes you make as a *draft* until you publish your changes. A draft is visible only to the person who creates it, until it is published.

To edit an already-published rule: 
1.	Select the rule and click **Edit**.
    A **Draft** tab and a **Published** tab appears. 
1.	Select the **Draft** tab and make your changes to the rule. 
    As you make changes, Fraud Protection automatically saves a draft. 
1.	To publish your changes, click **Publish**. 
    When you publish a draft, Fraud Protection overwrites the original published version of the rule with the changes you made in the draft version of the rule. 
1.	To discard your changes, click **Discard**. 
    When you discard your changes, Fraud Protection deletes the draft but retains the original published rule. 

> [!NOTE]
>If a teammate updates and publishes a rule while you are still editing it, your changes may be out of date. When this is the case, a warning appears asking if you still want to publish your changes.<br>If you click **Publish**, your changes overwrite all changes that were made previously.<br>If you click **Cancel**, you can review the changes others have made before you publish your version.  


### Search for a rule

When you search for a rule, all rule names and descriptions are searched, and the results are filtered accordingly.

- To search for a rule, type a keyword into the **Search** box.

- To remove the filter, delete the keyword from the **Search** box, or click the **x** to the right of the box.

### Change the order of a rule

The [order in which rules](rules.md#understand-rule-ordering) display on the **Rules** page has a signficant impact on how your events are evaluated. 

#### To move a rule to a new position using drag-and-drop:

1.	Navigate to the **Rules** management page.
1.	Select the rule you want to move, drag it to its new position, and then click **Save order.** 
    To cancel your changes, click **Cancel re-ordering**. 
    
#### To move a rule to a new position using a keyboard: 

1. Click **Reorder**.
   Fraud Protection displays the rules as draggable tiles.
1. Press the **Tab** key to choose a tile and then press **Spacebar** to activate the tile. 
1. Use the arrow keys to move the tile up or down the list
1. Press  **Spacebar** to accept the new position, or press the **ESC** key to return the tile to its original position.
1. To save your changes, click **Save order**. 
    If you want to cancel your changes, click **Cancel re-ordering**. 

## Evaluate a Rule

You can use the rule evaluation panel at the bottom of the **Rules** page to ensure your new rule returns the results you expect before you publish it.

#### To display the rule evaluation panel:

- At the bottom of the **Rules** page, click **Expand**. 

    The evaluation panel appears at the bottom of the **Rules** page. 
  
- To collapse the panel, click **Collapse**.

When the evaluation panel is expanded, your can watch your rule being evaluated against the [payload sample](rules.md#samples). As you make changes to the sample or to a clause, the content in the evaluation panel updates.

The evaluation panel displays the decision Fraud Protection returns for this sample event, as well as any values associated with the response. If a reason or support message was specified, it also appears here. The clause that triggers the decision is outlined in green. 

Fraud Protection’s AI does not generate a true risk score or bot score for the sample event. Instead, it uses the placeholder values entered in the score sample (link) to run the rule. 

If the condition does not find a match, the rule is not evaluated. If the condition finds a match but none of the clauses triggers a return, the default decision is Approve, with NO_CLAUSE_HIT as the reason. 

### Evaluate Example

If you create a rule with the following three clauses:

1. // Approves when email from contoso domain has been validated
RETURN Approve()<br>
WHEN @isEmailValidated == true && @email.EndsWith("@contoso.com")

2. // Rejects when email has not been validated and high risk score
RETURN Reject()<br>
WHEN @isEmailValidated == false && @riskscore > 700

3. // Reviews when email has not been validated and medium risk score
RETURN Review()<br>
WHEN @isEmailValidated == false && @riskscore > 400

Your payload sample contains the following user object:

    "email": {
        "email": "Primary",
        "emailValue": "kayla@contoso.com",
        "isEmailValidated": true,
        "emailValidatedDate": "2020-02-25T15:12:26.9733817-08:00",
        "isEmailUsername": true
    },

And you set a risk score of: 

    "riskScore": 500,

When the evaluation panel is expanded, Clause #1 will be triggered, and therefore highlighted in green, and the decision of *Approve* is returned. 

If you change the payload isEmailValidated field to:

        "isEmailValidated": false,

Clause #2 is triggered and the evaluation panel displays the decision as *Review*. 

If you change "riskScore" to 700 instead of 500, Clause #3 is triggered and the decision is updated to *Reject*. 









