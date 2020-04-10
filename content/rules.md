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

Dynamics 365 Fraud Protection gives you the flexibility to create custom rules based on observed patterns, policies, or business objectives. Custom rules enable your analysts to write business logic for automated decision making and customize this logic to meet your unique business needs. Rules use a combination of inputs including values in the event response payload and machine learning-based scores to assess the risk of an event. You can configure rules to automatically accept, block, review, or challenge events based on these inputs. For example, you could create a rule that rejects account logins from certain email domains, when the risk score is high. 

> [!NOTE]
> You cannot view or create rules in the INT environment. You must use the PROD environment. 

### Purchase, account creation, and account login events

You can create rules for *purchase*, *account creation*, and *account login* events in Fraud Protection. 
- To access purchase rules, click **Purchase protection** on the left navigation. 
- To access account creation and account login rules click **Account Protection (preview)** on the left navigation. There are two tabs on the **Account Protection** page, **Account Creation** and **Account Login**.

### Details (name and description)

When you create a rule, you can add details that make it easily identifiable for you and your team, such as a name and description. Rule names must be unique. 

### Status

#### Active or inactive rules

Once a rule has been published, it can be set to either *Active* or *Inactive*. 
- If a rule is *Active*, it affects real time production traffic. This means that all events of this type are evaluated against the rule. 
- If a rule is *Inactive*, it does not affect production traffic. 
For information on how to change the order in which Fraud Protection rules are run, see [Rule Ordering](rules.md#rule-ordering).

#### Draft rules

If you make changes to a rule that has previously been published, but have not yet published the changes, the modified rule is saved as a *Draft*, and its status is set to *Draft only*.

A published rule with unpublished changes can have a status of either *Active (with Draft)* or *Inactive (with Draft)*. 

### Payload

When you create or edit a rule, the *Sample Payload* panel displays on the right side of the page.  This panel is split into two sections that display sample API request code. 

#### Sample API request code

The upper section of the **Payload** panel displays a sample of the API request code for the purchase, account creation, or account login event you are creating. This sample provides you with an example of the fields you can use to create a new rule. Sample payloads for purchase, account creation, and account login events are different and cannot be used interchangeably. When you create a rule, you may not use all the fields shown in the payload, or you may use additional fields not shown in the payload panel. 

You can modify the sample payload to better reflect the data you want to send to Fraud Protection. When you change the payload, it has no impact on which data you are sending or not sending. It is provided as an example of the fields and the values you can use in the rule you are creating.
For information on how to reference payload fields in rule clauses, see [Clauses](rules.md#clauses).

 The lower section of this panel contains the scores available to use from Fraud Protection’s adaptive AI. Note that the values shown are simply samples. The value itself can be edited and is not itself meaningful. Also, note that in [prior-to-all scoring clauses](rules.md#prior-to-all-scoring-clauses) the scores shown here cannot be used. 

For information on how to evaluate your rule against the sample payload and scores, see [Payload](rules.md#payload).

### Conditions

A condition starts with the keyword **WHEN** and is followed by a valid Boolean expression, which means the statement must evaluate to either *True* or *False*. The condition determines which rule is evaluated and can be used as a mechanism to group related business logic. For example, this is a valid condition:

    WHEN @productType == “Digital”

Clauses that follow this condition can be used to configure fraud strategy pertaining to digital product transactions only. 

Conditions are optional fields within a rule, and if you want the rule to apply to all events, do not enter a condition. For information on how conditions are used in rule ordering, see [Rule ordering](rules.md#rule-ordering).

### Clauses

Clauses are the core components of rules and contain the heart of your fraud strategy. They follow the basic structure of: 

    RETURN x 
    WHEN y

Where **x** represents a one of four types of decision: *Approve*, *Reject*, *Challenge*, and *Review*. This decision is executed only when **y** evaluates to *True*. 

**y** represents a Boolean expression which can be formed using a combination of values from the [event payload](rules.md#payload), [user-defined lists](lists.md), and [machine learning-based bot and risk scores](rules.md#post-bot-scoring-clauses). 

For information about the syntax used for writing clauses see the [Fraud Protection language guide](fpl-lang-ref.md).

Clauses run sequentially in the order they are displayed on the page. Click the arrows to the right of each clause to re-order a clause. 

When a clause is triggered (that is, the **WHEN** statement returns True), the decision specified in the **RETURN** statement is returned, and no subsequent clauses are run. If a condition matches the decision but no clause within the rule is triggered, by default the rule is executed, as shown in the following example. 

    RETURN Approve(“NO_CLAUSE_HIT”).

The sequential ordering of a clause is divided into three distinct sections: *Pre-Score*, *Post-Bot Score* (which is applicable only for account creation and account login rules), and *Post-Risk Score*. These sections indicate when the clause is run relative to Fraud Protection’s advanced, adaptive AI score generation. 

#### Prior-to-all-scoring clauses

Once an event matches a condition, it is then run through the prior-to-all-scoring clauses. These clauses are run prior to Fraud Protection’s adaptive AI score generation. They can use any combination of fields sent as part of the event payload, and can be configured to implement embargo, geofencing, or other business policies. For example, the following clause enables you review purchases whenever a user buys a product outside of the market in which they are located:

    RETURN Review("user location and product market mismatch") 
    WHEN Geo.MarketCode(“@device.ipAddress”) != “@productList.market”

For information about supported geo operators, see[Geo operators](fpl-lang-ref.md#geo-operators). 

You can also use the clause in this section to reference lists. For example, if you have a custom list titled *Risky Emails* the following clause enables you to reject events if the user’s email appears on the list. 

    RETURN Reject ("email is on Risky Email list") 
    WHEN ContainsKey ("Risky Email List", "Emails", @username)

For information about the syntax for referencing lists in rules, the [Fraud Protection language guide](fpl-lang-ref.md).

#### Post-bot-scoring clauses

For account protection, Fraud Protection’s advanced, adaptive AI enables dynamic and robust bot-detection by providing a score that maps to the probability that a bot is initiating the event. The score is a number between 0 and 999, with a higher score indicating a higher bot probability. 

In post-bot-scoring clauses, you can make decisions using the score referenced with @botscore, in conjunction with other fields from the payload. For example, the following clause enables you to reject events from a specific email domain that also has a high bot score. 

    RETURN Review()
    WHEN @email.EndsWith("@contoso.com") && @botScore > 700

> [!NOTE]
>Post-bot-scoring clauses and the @botScore variable are available only for account creation and account login rules. 

#### Post-risk-scoring clauses

The machine learning model in Fraud Protection evaluates every transaction using advanced adaptive AI. It then assigns a risk score. This score is a number between 0 and 999. The higher the risk score, the higher the perceived risk.

In post-risk-scoring clauses, you can use this score, which is referenced with @riskscore, in conjunction with other fields from the payload to make decisions. For example, the following clause enables you to reject expensive transactions that also have a high-risk score. 

    RETURN Reject(“Risky US transaction”)
    WHEN @purchasePrice >= 199.99 && @riskScore > 700

## Rule ordering

The **Rules** page for an event (purchase, account login, or account creation) displays a list of all the rules you have configured for that event. The order of these rules is important because an event runs through each rule condition in the order that they appear on the Rules page, until a condition is matched. Once a condition is matched, the selected rule is evaluated. 

For example, you can configure the following three rules for Purchase events:

|Name	|Condition |Status|
|------|---------|------|
|Rule1  WHEN @country == “US”|    |Active|
|Rule2 	WHEN @product == “Xbox”|    |Inactive|
|Rule3 	WHEN @username == “Kayla|    |Active|

If a purchase transaction that takes place in the US matches with Rule1, Rule1 is evaluated, and Rule3 is not. 

Since Rule2 has a status of *Inactive*, it is never evaluated with real time production traffic.

For example: 

  - If a customer makes a purchase, and if they are in the US, only Rule1 is evaluated.
  - If a customer makes a purchase, and if they are from a different country, Rule3 is evaluated instead. 

If no conditions match the event, by default Fraud Protection executes: 

    RETURN Approve(“NO_RULE_HIT”)

##  Access the Rules management page

You can manage existing rules and create custom rules on the **Rules** management page. There are two rules management pages, one is for purchase protection and the other is for account protection. 

- To display rules related to purchases, click **Purchase protection** and then click **Rules** on the left navigation.

- To display rules related to accounts, click **Account protection** and then click the **Rules** on the left navigation.

The **Account protection Rules** page has two tabs:

- On the **Account creation** tab, you can create rules that check for fraud user credentials when someone is trying to create a new account.
    
- On the **Account login** tab, you can create rules that check for fraudulent login credentials when someone logs into an existing account.

You can view all the rules configured for an event type in the **Rules** management page. 
The [order](rules.md#rule-ordering) in which rules are displayed determines the order in which rules are executed. 

You can view the following information for each rule:
-	The descriptive [Name](rules.md#details-name-and-description) of the rule.
-	The [Condition](rules.md#conditions) you creeated for the rule.
-	The [Status](rules.md#status)of the rule (**Active**, **Inactive**, or **Draft**).
-	The [Description](rules.md#details-name-and-description) of the rule.
-	The [Number of Clauses](rules.md#clauses) in the rule.


## Create a new rule
You can create two types of rules to automatically accept, block, review, and challenge events based on these inputs: rules for *purchase protection*, and rules for *account and login protection*. 

#### To create a new rule:

1. Depending on the type of rule you want to create, select the appropriate **Rules** management page on the left navigation:

    - To create rules for protecting purchases, click **Purchase protection**. 
    - To create rules for protecting account creation and login, click **Account protection**. 
  
1. If you selected **Account protection**: 

    - To create a rule to protect account creation, click **Account Creation**.
    - To create a rule to protect account login, click **Account Login**.
  
1. Click **New Rule**, click **Rename**, and then add a name and description so that the rule is easily identifiable to you and your team.
1. Add a [condition](rules.md#conditions) to your rule.
1. To create a new [clause](rules.md#clauses) from scratch, click **+ new clause**, located under the appropriate clause section.

    Or, to create a new clause using a pre-existing template:
    
    1. Click the arrow to the right of **New Clause**. 
        Fraud Protection displays a short list of templates. 
            
    1. To display the full selection of templates and their titles, descriptions, and contents, click **See all**. 
        
    1. Select a clause template as a starting point to create your own fraud logic in the clause. 
        
    You can modify the placeholder values in the template to suit your business requirements. 
            
1. Review your rule.

  You can add, remove, and re-order clauses using the controls to the right of the clause box. 
    
1. To publish your rule, click **Publish**. 
1. (Optional) In the confirmation dialog, update the name and description.
1. Set the [status](rules.md#status) of the rule to either **Active** or **Inactive**, and then click **Publish**.

    By default, the new rule displays at the bottom of the page.
    
1. To move the rule to a new position: 
    1. Navigate to the **Rules** management page.
    1. Select the rule, drag it to its new position, and then click **Save order**. 

## Manage existing rules
You can perform the following operations on an existing rule on the Rules management page:
-	[Clone](rules.md#clone-an-existing-rule)
-	[Edit](rules.md#edit-an-existing-rule)
-	[Rename](rules.md#update-the-name-and-description-of-a-rule)
-	[Activate or Deactivate](rules.md#change-the-status-of-a-rule)
-	[Delete](rules.md#delete-a-rule)
 
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
  By default, the new rule displays at the bottom of the page.
1. To move the rule to a new position: 
  1. Navigate to the **Rules** management page.
  1. Select the rule, drag it to its new position, and then click **Save order**. 

### Search for a rule

When you search for a rule, all rule names and descriptions are searched, and the results are filtered accordingly. 

- To search for a rule, type a keyword into the **Search** box. 
- To remove the filter, delete the keyword from the **Search** box, or click the **x** to the right.

### Edit an existing rule

To edit an existing rule, select the rule, click **Edit**, make your changes, and then click **Update**. 

### Change the order of a rule

The order in which rules display on the **Rules** page is significant because an event runs through each rule in the order in which it appears until a condition is matched. By moving more important rules to the top of the list, you receive a quicker response when you run your rules.

#### To move a rule to a new position using a keyboard: 

1.	Navigate to the **Rules** management page.
2.	Select the rule you want to move, and then click **Reorder**.
    Fraud Protection displays the rules as draggable tiles.
3.	Press the **Tab** key to choose a tile and then press **Spacebar** to activate the tile. 
4.	Use the arrow keys to move the tile up or down the list, and then press **Spacebar** to accept the new position.
5.	To save your changes, click **Save order**. 
    If you want to cancel your changes, click **Cancel re-ordering**. 

#### To move a rule to a new position using drag-and-drop:

1.	Navigate to the **Rules** management page.
2.	Select the rule you want to move, drag it to its new position, and then click **Save order.** 
    If you want to cancel your changes, click **Cancel re-ordering**. 






