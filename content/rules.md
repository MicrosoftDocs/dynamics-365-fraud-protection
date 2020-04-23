---
author: yvonnedeq
description: This topic explains how to use rules.
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

Dynamics 365 Fraud Protection gives you the flexibility to create custom rules based on observed patterns, policies, or business objectives. Custom rules help your analysts write business logic for automated decision making and customize logic to meet unique business needs. Rules use a combination of inputs including values in the event request payload and AI-based scores to assess the risk of an event. Based on these inputs, you can configure rules to convert the assessment into a decision such as *approve*, *reject*, *review*, or *challenge*.  

> [!NOTE]
> You can't view or create rules in the INT environment. You must use the PROD environment. 

##  Access the Rules page

You can create custom rules and manage existing rules on the **Rules** page. 

- To create and manage rules related to purchases, select **Purchase protection** and then select **Rules** on the left navigation.

- To create and manage rules related to accounts, select **Account protection** and then select **Rules** on the left navigation.

The **Rules** page for **Account protection** has two assessment type tabs:

-  On the **Account creation** tab, you can create rules that run on account creation events when someone is trying to create a new account.
-  On the **Account login** tab, you can create rules that run on account login events.

The **Rules** page displays a list of all the rules configured for an assessment type. You can view the following information for each rule:

-  The  [name](rules.md#name-and-description).
-  The [condition](rules.md#conditions) you created.
-  The [status](rules.md#status): *active* or *inactive*.
-  The [description](rules.md#name-and-description).
-  The number of [clauses](rules.md#clauses) you created.

> [!NOTE]
>Rules are listed on the **Rules** page in the order they are executed. 

## Components of a rule

A rule consists of:
-  A [name and description](rules.md#name-and-description) that describe its purpose.
-  Its current [status](rules.md#status): *active* or *inactive*.
-  A [sample](rules.md#samples) of fields to help you write and evaluate the rule.
-  Components that help you build the logic that automatically approves, rejects, challenges, or reviews events. This includes:
    -  A [condition](rules.md#conditions).
    -  One or more of the following types of [clauses](rules.md#clauses):
       -  [Prior to all scoring clauses](rules.md#prior-to-all-scoring-clauses).
       -  [Post bot scoring clauses](rules.md#post-bot-scoring-clauses).
       -  [Post risk scoring clauses](rules.md#post-risk-scoring-clauses).

### Name and description

When you create a rule, you can add a name and description to make the rule easily identifiable for you and your team. Rule names must be unique and case insensitive.

### Status

When you publish a rule, you can set the status to either *active* or *inactive*. 

- If a rule is active, it affects real time production traffic, and all events of this type are evaluated against the rule. 
- If a rule is inactive, it doesn't affect production traffic. 

#### Samples
When you create or edit a rule, the **Sample** pane displays on the right side of the page. This pane has two sections: *payload sample* and *score sample*.

- To view sample variables used in your rule, select **Show used variables**. 

##### Payload sample 

The payload sample contains examples of fields you can use in an API request for a purchase, account creation, or account login event. If the fields in the sample don’t accurately reflect the data you want to send to Fraud Protection, you can replace them with custom data fields.

The payload sample is provided as an example and may not accurately reflect the data you send to Fraud Protection. For example, the sample may include fields which you don't want to send, and may not include custom data fields which you do want to send. You can, however, use custom fields in your rules as you would any other payload variable.

##### Score Sample

The score sample contains scores generated from Fraud Protection’s AI models. You can reference score variables in rules after you run the associated AI model and generate the score. For example, you can use **@botScore** after the *bot* evaluation has run, and **@riskScore** after the *risk* evaluation has run. For more information, see [Clauses](rules.md#clauses).

#### Edit the sample
To test that your rule works on a variety of events, you can modify the sample as required, and then [evaluate](rules.md#evaluate-example) the sample data against the rule. All values in both samples can be modified. When you change a sample, it has no impact on which data you send (or don't send) to Fraud Protection.

When you publish a rule, changes you make to the sample are saved and persisted as part of the rule.

- To undo all changes made to the sample by you or  someoneone else, select **Revert**. 

### Conditions

A condition starts with the keyword **WHEN** and is followed by a Boolean expression which evaluates the statement to either *True* or *False*. It can be created to determine which rule is evaluated and to group related business logic. This is an example of a condition related to digital product transactions:

    WHEN @productType == “Digital”

You can then create clauses that configure a fraud strategy related to digital product transactions.

Adding a condition to a rule is optional.  if you want a rule to apply to all events, don't enter a condition. For information about how to use conditions to order rules, see [Rule ordering](rules.md#understand-rule-ordering).

### Clauses

Clauses are the building blocks of rules and contain the core standards of your fraud strategy. They use values in the event payload with Fraud Protection’s AI scores to approve, reject, review, or challenge events. This is the basic structure of a clause: 

    RETURN *decision* 
    WHEN *condition is true*

You can use this structure to create a clause that returns a decision of *approve*, *reject*, *challenge*, or *review*, and then add optional parameters that sends more information about the decision.

Everything that follows **WHEN** must evaluate to either True or False. This Boolean expression can consist of values from the [event payload](rules.md#clauses), [user-defined lists](lists.md), and [AI-based bot and risk scores](rules.md#post-bot-scoring-clauses). 

For information about the syntax for clauses, see the [Rules language guide](fpl-lang-ref.md).

When a clause is triggered (that is, the **WHEN** statement returns *True*), the *decision* specified in the **RETURN** statement is returned, and no subsequent clauses are run. 

If a condition matches the decision but doesn't trigger a clause, the rule then executes: 

    RETURN Approve(“NO_CLAUSE_HIT”).

Clauses run sequentially in the order they  display on the **Rules** page. Use the arrow keys on the right of the clause to change its position on the list.  

The sequential ordering of clauses has three sections: *Pre-Score*, *Post-Bot Score* (which is applicable only for account creation and account login rules), and *Post-Risk Score*. These sections indicate when the clause is run relative to Fraud Protection’s advanced AI score generation. 

#### Prior-to-all-scoring clauses

Prior-to-all-scoring clauses run before Fraud Protection’s AI models are run, and thus before any bot or risk assessment scores have been generated. These clauses can use any combination of fields sent as part of the event payload, and contained in [Lists](lists.md). They can be configured to implement embargo, geofencing, or other business policies. 

The following example helps you to review purchases when a user buys a product in a market outside their geographical location.

    RETURN Review("location inconsistency") 
    WHEN Geo.MarketCode(“@device.ipAddress”) != “@productList.market”
 
You can also write a clause in this section to cross reference lists. For example, if you have a custom list titled *Risky Emails* the following clause rejects events if the user’s email address is on the list. 

    RETURN Reject ("risky email") 
    WHEN ContainsKey ("Risky Emails", "Emails", @email)

For information about the syntax for referencing lists in rules, see the [Rules language guide](fpl-lang-ref.md).

#### Post-bot-scoring clauses

Post-bot-scoring clauses run after Fraud Protection’s AI models have generated a bot score for the event. This score maps to the probability that a bot initiated the event. This score is a number between 0 and 999. A higher score indicate a higher bot probability. 

In post-bot-scoring clauses, you can use this score, referenced with **@botScore**, with fields from the payload and Lists to make decisions. For example, the following clause rejects events from a specific email domain with a bot score greater than 700. 

    RETURN Reject()
    WHEN @email.EndsWith("@contoso.com") && @botScore > 700

> [!NOTE]
>Post-bot-scoring clauses and the **@botScore** variable are available only for account protection rules. 

#### Post-risk-scoring clauses

Post-risk-scoring clauses run after Fraud Protection’s AI models have generated a risk assessment score for the event. This score is a number between 0 and 999.  higher score indicating a higher perceived risk.

In post-risk-scoring clauses, you can use this score, referenced with **@riskScore**, with fields from the payload and lists to make decisions. For example, the following clause rejects expensive transactions with a risk score greater than 700. 

    RETURN Reject(“high price and risk score”)
    WHEN @purchasePrice >= 199.99 && @riskScore > 700

## Understand rule ordering

The **Rules** page displays a list of rules you configured for the assessment. The order in which they are listed affects in order in which they are evaluated. An event runs through each rule condition in order until a condition is matched. Then the selected rule is evaluated and no subsequent rules are run. 

For example, when you configure the following three purchase rules:

|Name	|Condition |Status|
|------|---------|------|
|Rule1  |WHEN @country == “US”    |Active|
|Rule2 	|WHEN @username == “Kayla    |Inactive|
|Rule3 	|WHEN @product == “Xbox”    |Active|

The following behavior occurs:

- Rule2 has a status of Inactive, and is never evaluated against real time production traffic.
- Rule1 is evaluated only if a customer in the US makes a purchase.
- Rule1 is evaluated only if a customer in the US makes an Xbox purchase.
- Rule3 is evaluated only if a customer outside the US makes an Xbox purchase.
- No rules are evaluated if a customer outside the US makes a non-Xbox purchase.

If no rules are evaluated because no conditions match the event, Fraud Protection then executes: 

    RETURN Approve(“NO_RULE_HIT”)

For information about how to reorder rules on the **Rules** page, see [Change the order of a rule](rules.md#change-the-order-of-a-rule).

## Create a new rule
You can create rules that make decisions related to purchase, account creation, and account login events.

> [!IMPORTANT]
>By default, a new rule displays at the bottom of the list on the **Rules** page. To reposition the rule, see [Change the order of a rule](rules.md#change-the-order-of-a-rule).

#### To create a new rule:

1. Navigate to the [**Rules** page](rules.md#access-the-rules-page).
1. Select **New Rule**.
1. (Optional) Select **Rename**, and then add a name and description so that the rule is easily identifiable to you and your team.

    Fraud Protection also prompts you to add a name and description when you publish your rule.
    
1. Add a [condition](rules.md#conditions) to your rule.

1. To create a new [clause](rules.md#clauses) from scratch, select **+ new clause** located under the appropriate clause section, and then create your own fraud logic.

    Or, to create a new clause using a pre-existing template:
    
    1. Select the arrow to the right of **New Clause**. 
    
        Fraud Protection displays a list of  templates names. 
            
    1. To display the full selection of available templates and their titles, descriptions, and contents, select **See all**. 
        
    1. Select a clause template as a starting point to create your own fraud logic in the clause. Then modify the values in the template to suit your business requirements.     
1. To [evaluate your rule](rules.md#evaluate-a-rule) and ensure it works as expected, select **Expand** on the bottom right of the **Rules** page to expand the evaluation pane.
1. To publish your rule, select **Publish**, change the name, description, and status in the confirmation dialog, and then select **Publish**.
1. Set the [status](rules.md#status) to either **Active** or **Inactive**.
1. To reposition the rule on the order list: 
    1. Navigate to the **Rules** page.
    1. Select the rule, drag it to its new position, and then select **Save order**. 

## Manage existing rules
You can perform the following operations on an existing rule on the Rules page:
-	[Rename](rules.md#update-the-name-and-description-of-a-rule)
-	[Activate or deactivate](rules.md#change-the-status-of-a-rule)
-	[Delete](rules.md#delete-a-rule)
-	[Clone](rules.md#clone-an-existing-rule)
-	[Edit](rules.md#edit-an-existing-rule)
 
### Update the name and description of a rule

To update the name and description of a rule, select a rule, select **Rename**, and then enter a unique name and description.

### Change the status of a rule

To change the status of a rule, select a rule, and then select **Activate** or **Deactivate**.

### Delete a rule

To delete a rule, select a rule, and then select **Delete**. When you delete a rule, the action can't be undone. 

### Clone an existing rule

When you clone a rule, you create a copy of an existing rule that you can modify and save as a new rule.

#### To clone a rule:
1. Select a rule, and then select **Clone**. 
  
   This creates a copy of the selected rule and automatically sets the status to **Inactive**. 
  
1. Update the rule, and then select **Publish**. 
1. To reposition the rule on the order list: 
   1. Navigate to the **Rules** page.
   1. Select the rule, drag it to its new position, and then select **Save order**. 

### Edit an existing rule
To edit an existing rule, select a rule, and then select **Edit**. When you finish making your changes, select **Update** to update the existing rule running in production.

### Search for a rule

When you search for a rule, all rule names and descriptions are searched, and the results are filtered accordingly.

- To search for a rule, type a keyword into the **Search** box.

  To remove a filter, delete the keyword from the **Search** box or select **x** in the right of the box.

### Change the order of a rule

Because rules display on the **Rules** page in the order in which they run, the position of a rule has a signficant impact on how events are evaluated. 

#### To move a rule to a new position using drag-and-drop:

1. Select the rule you want to move, and then drag-and-drop it to a new position.
1. Repeat Step 1 to move as many rules as you want, and then select **Save order.** 

    To cancel your changes, select **Cancel re-ordering**. 
    
#### To move a rule to a new position using a keyboard: 

1. Select **Reorder**.

   Fraud Protection displays the rules as tiles which you can select and move.
   
1. Press the **Tab** key and then press **Spacebar** to select a tile, use the arrow keys to move it, and then press **Spacebar** to accept the new position. 

   Press the **ESC** key to return the tile to its original position.

1. Repeat Step 1 to move as many tiles as you want, and then select **Save order.** 
1. To save your changes, select **Save order**. 

   To cancel your changes, select **Cancel re-ordering**. 

## Evaluate a Rule

You can use the rule evaluation pane at the bottom of the **Rules** page to ensure your new rule returns the results you expect before you publish it.

#### To display the rule evaluation pane:

- At the bottom of the **Rules** page, select **Expand**. 

    The evaluation pane appears at the bottom of the **Rules** page. 
  
- To collapse the pane, select **Collapse**.

When the evaluation pane is expanded, you can watch your rule being evaluated against the [payload sample](rules.md#samples). The content in the evaluation pane automatically updates when you make changes to the sample or clause.

The evaluation pane displays:

- The decision Fraud Protection returns for a sample event and any values associated with the response. 
- Any specified reason or support message. 
- The clause that triggers the decision, outlined in green. 

Fraud Protection’s AI doesn't generate a true risk score or bot score to run the rule for the sample event. Instead, it uses placeholder values entered in the [score sample](rules.md#score-sample). 

If the condition doesn't find a match, the rule is not evaluated. 
If the condition finds a match but none of the clauses triggers a return, the default decision is *Approve*, with *NO_CLAUSE_HIT* as the reason. 

### Evaluate Example

You can create a rule with the following three clauses:

1. // Approves when email from contoso domain has been validated
RETURN Approve()<br>
WHEN @isEmailValidated == true && @email.EndsWith("@contoso.com")

2. // Rejects when email has not been validated and high risk score
RETURN Reject()<br>
WHEN @isEmailValidated == false && @riskscore > 700

3. // Reviews when email has not been validated and medium risk score
RETURN Review()<br>
WHEN @isEmailValidated == false && @riskscore > 400

The payload sample contains the following user object:

    "email": {
        "email": "Primary",
        "emailValue": "kayla@contoso.com",
        "isEmailValidated": true,
        "emailValidatedDate": "2020-02-25T15:12:26.9733817-08:00",
        "isEmailUsername": true
    },

And you can set a risk score of: 

    "riskScore": 500,

When the evaluation pane is expanded, Clause #1 is triggered, highlighted in green, and the decision of *Approve* is returned. 

If you change the payload **isEmailValidated** field to:

        "isEmailValidated": false,

Clause #2 is triggered, highlighted in green, and the evaluation pane displays the decision as *Review*. 

If you change "riskScore" to 700 instead of 500, Clause #3 is triggered, highlighted in green, and the decision is updated to *Reject*. 









