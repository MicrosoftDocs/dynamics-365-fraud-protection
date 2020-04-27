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
title: Manage rules

---

# Manage rules

## Overview

Microsoft Dynamics 365 Fraud Protection gives you the flexibility to create custom rules that are based on observed patterns, policies, or business objectives. Custom rules help your analysts write business logic for automated decision making and customize logic to meet your unique business needs. Rules use a combination of inputs to assess the risk of an event. These inputs include values in the event request payload and scores that are based on artificial intelligence (AI). Based on these inputs, you can configure rules to convert the assessment into a decision, such as *Approve*, *Reject*, *Review*, or *Challenge*.

> [!NOTE]
> You can't view or create rules in the INT environment. You must use the PROD environment.

## Access the Rules page

You can create custom rules and manage existing rules on the **Rules** page.

- To create and manage rules that are related to purchases, select **Purchase protection**, and then select **Rules** in the left navigation pane.
- To create and manage rules that are related to accounts, select **Account protection**, and then select **Rules** in the left navigation pane.

The **Rules** page for Account protection has tabs for two assessment types:

- On the **Account creation** tab, you can create rules that run on account creation events when someone tries to create a new account.
- On the **Account login** tab, you can create rules that run on account login events.

The **Rules** page shows a list of all the rules that are configured for an assessment type. For each rule, you can view the following information:

- The [name](rules.md#name-and-description)
- The [condition](rules.md#conditions) that you created
- The [status](rules.md#status): *Active* or *Inactive*
- The [description](rules.md#name-and-description)
- The number of [clauses](rules.md#clauses) that you created

> [!NOTE]
> On the **Rules** page, rules are listed in the order that they are run in.

## Components of a rule

A rule consists of the following components:

- A [name and description](rules.md#name-and-description) that describe the purpose of the rule.
- The current [status](rules.md#status) of the rule: *Active* or *Inactive*.
- A [sample](rules.md#samples) of fields, to help you write and evaluate the rule.
- Components that help you build the logic that automatically approves, rejects, challenges, or reviews events:

    - A [condition](rules.md#conditions)
    - One or more of the following types of [clauses](rules.md#clauses):

        - [Prior to all scoring clauses](rules.md#prior-to-all-scoring-clauses)
        - [Post-bot-scoring clauses](rules.md#post-bot-scoring-clauses)
        - [Post-risk-scoring clauses](rules.md#post-risk-scoring-clauses)

### Name and description

When you create a rule, you can add a name and description to help yourself and your team easily identify the rule. Rule names must be unique, and they are case-insensitive.

### Status

When you publish a rule, you can set the status to either *Active* or *Inactive*.

- If a rule is active, it affects real-time production traffic, and all events of this type are evaluated against the rule.
- If a rule is inactive, it doesn't affect production traffic.

### Samples

When you create or edit a rule, the **Sample** pane appears on the right side of the page. This pane has two sections: one for the *payload sample* and one for the *score sample*.

To view the sample variables that are used in your rule, select **Show used variables**.

#### Payload sample

The payload sample contains examples of fields that you can use in an application programming interface (API) request for a purchase, account creation, or account login event.

The payload sample is provided as an example and might not accurately reflect the data that you send to Fraud Protection. For example, the sample might include fields that you don't want to send, and it might not include custom data fields that you do want to send. In this case, you can replace the fields in the sample with custom data fields, and use custom data fields in your rules just as you would use any other payload variable.

#### Score sample

The score sample contains scores that are generated from Fraud Protection's AI models. You can reference score variables in rules after you run the associated AI model and generate the score. For example, you can use *@botScore* after the bot evaluation has run, and you can use *@riskScore* after the risk evaluation has run. For more information, see the [Clauses](rules.md#clauses) section later in this topic.

#### Edit the sample

To validate that your rule works on a variety of events, you can modify the sample as you require and then [evaluate](rules.md#evaluate-example) the sample data against the rule. All values in both the payload sample and the score sample can be modified. When you change a sample, the changes don't affect which data you send (or don't send) to Fraud Protection.

When you publish a rule, any changes that you make to the sample are saved and persisted as part of the rule.

To undo all changes that you or someone else made to the sample, select **Revert**.

### Conditions

Conditions start with the keyword **WHEN** and are followed by a Boolean expression that evaluates a statement to either *True* or *False*. A condition can be created to determine which rule is evaluated and to group related business logic. For example, the following condition is related to digital product transactions.

    WHEN @productType == "Digital"

You can then create clauses that configure a fraud strategy that is related to digital product transactions.

The addition of a condition to a rule is optional. If you want a rule to apply to all events, don't add a condition. For information about how to use conditions to order rules, see the [Rule ordering](rules.md#rule-ordering) section later in this topic.

### Clauses

Clauses are the building blocks of rules and contain the core standards of your fraud strategy. They use values in the event payload together with Fraud Protection's AI scores to approve, reject, review, or challenge events. Clauses have the following basic structure.

    RETURN *decision* 
    WHEN *condition is true*

You can use this structure to create a clause that returns a decision of *Approve*, *Reject*, *Challenge*, or *Review*. You can then add optional parameters that send more information about the decision.

Everything after **WHEN** must be able to be evaluated to either *True* or *False*. This Boolean expression can consist of values from the [event payload](rules.md#clauses), [user-defined lists](lists.md), and [AI-based bot and risk scores](rules.md#post-bot-scoring-clauses).

For information about the syntax for clauses, see the [Rules language guide](fpl-lang-ref.md).

When a clause is triggered (that is, the **WHEN** statement returns *True*), the *decision* that is specified in the **RETURN** statement is returned, and no subsequent clauses are run.

If a condition matches the decision but doesn't trigger a clause, the rule then runs.

    RETURN Approve("NO_CLAUSE_HIT")

Clauses run sequentially in the order in which they appear on the **Rules** page. You can use the arrow keys on the right side of a clause to change its position in the list.

The sequential ordering of clauses has three sections: *Pre-Score*, *Post-Bot Score*, and *Post-Risk Score*. These sections indicate when the clause is run relative to Fraud Protection's advanced AI score generation. The *Post-Bot Score* section is applicable only to account creation and account login rules.

#### Prior-to-all-scoring clauses

Prior-to-all-scoring clauses run before Fraud Protection's AI models are run. Therefore, they run before any bot or risk assessment scores have been generated. These clauses can use any combination of fields that are sent as part of the event payload and contained in [lists](lists.md). They can be configured to implement embargo, geofencing, or other business policies.

The following example helps you review purchases when users buy a product in a market outside their geographical location.

    RETURN Review("location inconsistency") 
    WHEN Geo.MarketCode("@device.ipAddress") != "@productList.market"

In this section, you can also write a clause to cross-reference lists. For example, if you have a custom list that is named *Risky Emails*, the following clause rejects events if the user's email address appears in the list.

    RETURN Reject ("risky email") 
    WHEN ContainsKey ("Risky Emails", "Emails", @email)

For information about the syntax that is used to reference lists in rules, see the [Rules language guide](fpl-lang-ref.md).

#### Post-bot-scoring clauses

Post-bot-scoring clauses run after Fraud Protection's AI models have generated a bot score for the event. This score represents the probability that a bot initiated the event. It's a number between 0 and 999. A higher score indicates a higher bot probability.

In post-bot-scoring clauses, you can use this score together with fields from the payload and lists to make decisions. You reference this score by using the *@botScore* variable. For example, the following clause rejects events from a specific email domain that has a bot score that is more than 700.

    RETURN Reject()
    WHEN @email.EndsWith("@contoso.com") && @botScore > 700

> [!NOTE]
> Post-bot-scoring clauses and the *@botScore* variable are available only for account protection rules.

#### Post-risk-scoring clauses

Post-risk-scoring clauses run after Fraud Protection's AI models have generated a risk assessment score for the event. This score is a number between 0 and 999. A higher score indicates a higher perceived risk.

In post-risk-scoring clauses, you can use this score together with fields from the payload and lists to make decisions. You referenced this score by using the *@riskScore* variable. For example, the following clause rejects expensive transactions that have a risk score that is more than 700.

    RETURN Reject("high price and risk score")
    WHEN @purchasePrice >= 199.99 && @riskScore > 700

## Rule ordering

The **Rules** page shows a list of the rules that you configured for the assessment. The order that the rules are listed in affects the order that they are evaluated in. An event runs through each rule condition, in order, until a condition is matched. The selected rule is then evaluated, and no subsequent rules are run.

For example, you configure the following three purchase rules.

| Name  | Condition | Status |
|-------|-----------|--------|
| Rule1 | WHEN @country == "US" | Active |
| Rule2 | WHEN @username == "Kayla | Inactive |
| Rule3 | WHEN @product == "Xbox" | Active |

In this case, the following behavior occurs:

- Rule2 has a status of *Inactive* and is never evaluated against real-time production traffic.
- Rule1 is evaluated only if a customer in the US makes a purchase.
- Rule1 is evaluated only if a customer in the US makes an Xbox purchase.
- Rule3 is evaluated only if a customer outside the US makes an Xbox purchase.
- No rules are evaluated if a customer outside the US makes a non-Xbox purchase.

If no rules are evaluated, because no conditions match the event, Fraud Protection runs the following.

    RETURN Approve("NO_RULE_HIT")

For information about how to reorder rules on the **Rules** page, see the [Change the order of a rule](rules.md#change-the-order-of-a-rule) section later in this topic.

## Create a new rule

You can create rules that make decisions that are related to purchase, account creation, and account login events.

> [!IMPORTANT]
> By default, a new rule appears at the bottom of the list on the **Rules** page. For information about how to reposition the rule, see the [Change the order of a rule](rules.md#change-the-order-of-a-rule) section.

Follow these steps to create a new rule.

1. On the [**Rules** page](rules.md#access-the-rules-page), select **New Rule**.
1. Optional: Select **Rename**, and then add a name and description to help yourself and your team easily identify the rule.

    Fraud Protection also prompts you to add a name and description when you publish your rule.

1. Add a [condition](rules.md#conditions) to your rule.
1. To create a new [clause](rules.md#clauses) from scratch, select **New clause** in the appropriate clause section, and then create your own fraud logic.

    –or–

    To create a new clause by using a pre-existing template, follow these steps:

    1. Select the arrow to the right of **New Clause**.

        Fraud Protection shows a list of templates names.

    1. To view the full list of available templates, and their titles, descriptions, and contents, select **See all**.
    1. Select a clause template to use as a starting point to create your own fraud logic in the clause. Then modify the values in the template to suit your business requirements.

1. To [evaluate your rule](rules.md#evaluate-a-rule) and make sure that it works as you expect, select **Expand** in the lower right of the **Rules** page to open the rule evaluation pane.
1. To publish your rule, select **Publish**. In the confirmation dialog box, change the name, description, and status, and then select **Publish**.
1. Set the [status](rules.md#status) to either *Active* or *Inactive*.
1. To reposition the rule in the list on the **Rules** page, select the rule, drag it to its new position, and then select **Save order**.

## Manage existing rules

On the **Rules** page, you can perform the following operations on an existing rule:

- [Rename](rules.md#update-the-name-and-description-of-a-rule)
- [Activate or deactivate](rules.md#change-the-status-of-a-rule)
- [Delete](rules.md#delete-a-rule)
- [Clone](rules.md#clone-an-existing-rule)
- [Edit](rules.md#edit-an-existing-rule)

### Update the name and description of a rule

To update the name and description of a rule, select the rule, select **Rename**, and then enter a unique name and description.

### Change the status of a rule

To change the status of a rule, select the rule, and then select **Activate** or **Deactivate**.

### Delete a rule

To delete a rule, select it, and then select **Delete**. Be aware that this operation can't be undone.

### Clone an existing rule

When you clone an existing rule, you create a copy of it that you can modify and save as a new rule.

To clone a rule, follow these steps.

1. Select a rule, and then select **Clone**.

    A copy of the selected rule is created, and its status is automatically set to *Inactive*.

1. Update the rule, and then select **Publish**.
1. To reposition the rule in the list on the **Rules** page, select the rule, drag it to its new position, and then select **Save order**.

### Edit an existing rule

To edit an existing rule, select it, and then select **Edit**. When you've finished making your changes, select **Update** to update the existing rule that is running in production.

### Search for a rule

When you search for a rule, all rule names and descriptions are searched, and the results are filtered accordingly.

To search for a rule, enter a keyword in the **Search** field.

To remove a filter, delete the keyword from the **Search** field, or select the **X** on the right side of the field.

### Change the order of a rule

Because rules appear on the **Rules** page in the order that they run in, the position of a rule significantly affects how events are evaluated.

#### Move a rule to a new position by using a drag-and-drop operation

1. Select the rule that you want to move, and then drag it to a new position.
1. Repeat step 1 to move as many other rules as you want, and then select **Save order**.

    To cancel your changes, select **Cancel re-ordering**.

#### Move a rule to a new position by using a keyboard

1. Select **Reorder**.

    Fraud Protection shows the rules as tiles that you can select and move.

1. Select the **Tab** key, and then select the **Spacebar** to select a tile. Use the arrow keys to move the tile, and then select the **Spacebar** to accept the new position.

    Select the **Esc** key to return the tile to its original position.

1. Repeat step 1 to move as many other tiles as you want, and then select **Save order**.
1. To save your changes, select **Save order**. 

    To cancel your changes, select **Cancel re-ordering**.

## Evaluate a rule

Before you publish your new rule, you can use the rule evaluation pane to make sure that it returns the results that you expect.

To open the rule evaluation pane, at the bottom of the **Rules** page, select **Expand**. The evaluation pane appears at the bottom of the **Rules** page.

To close the pane, select **Collapse**.

When the evaluation pane is open, you can watch your rule being evaluated against the [payload sample](rules.md#samples). The content in the evaluation pane is automatically updated when you make changes to the sample or clause.

The evaluation pane shows the following information:

- The decision that Fraud Protection returns for a sample event, and any values that are associated with the response.
- Any specified reason or support message.
- The clause that triggers the decision. This clause is outlined in green.

Fraud Protection's AI doesn't generate a true risk score or bot score to run the rule for the sample event. Instead, it uses placeholder values that are entered in the [score sample](rules.md#score-sample).

If the condition doesn't find a match, the rule isn't evaluated. If the condition finds a match, but none of the clauses triggers a return, the default decision is *Approve*, and the reason is *NO\_CLAUSE\_HIT*.

### Evaluation example

You create a rule that has the following three clauses:

1. `// Approves when email from contoso domain has been validated`<br>
`RETURN Approve()`<br>
`WHEN @isEmailValidated == true && @email.EndsWith("@contoso.com")`

2. `// Rejects when email has not been validated and high risk score`<br>
`RETURN Reject()`<br>
`WHEN @isEmailValidated == false && @riskscore > 700`

3. `// Reviews when email has not been validated and medium risk score`<br>
`RETURN Review()`<br>
`WHEN @isEmailValidated == false && @riskscore > 400`

The payload sample contains the following user object.

    "email": {
        "email": "Primary",
        "emailValue": "kayla@contoso.com",
        "isEmailValidated": true,
        "emailValidatedDate": "2020-02-25T15:12:26.9733817-08:00",
        "isEmailUsername": true
    },

You can set the following risk score.

    "riskScore": 500,

When the evaluation pane is opened, clause 1 is triggered and is highlighted in green, and a decision of *Approve* is returned.

You now change the **isEmailValidated** field in the payload.

    "isEmailValidated": false,

In this case, clause 2 is triggered and is highlighted in green, and a decision of *Review* is returned.

If you set **"riskScore"** to **700** instead of **500**, clause 3 is triggered and is highlighted in green, and the decision is updated to *Reject*.
