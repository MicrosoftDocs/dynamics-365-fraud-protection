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
title: Managing Rules

---

# Managing Rules

## Elements of a Rule

### Details

When you create a rule, you can add details that make it easily identifiable, for example, a descriptive name and a brief description of what your rule is designed to do.

### Conditions

A condition is an expression that evaluate to a *True* or *False* (Boolean) value. That means that when a specified condition is true, DFP performs the task you specify. A condition always starts with **WHEN** and is followed by any valid expression that results in a Boolean value. For example:
    WHEN Geo.CountryCode(@ipAddress) == "BR"
    WHEN @username.endsWith("contoso.com")

Conditions can be used to group together related rules. These rules are  run only if the initial condition is evaluated as *True*.

### Clauses

A clause returns a decision, based on specific conditions. Clauses are run in sequential order, and you can change the order in which rules are run. For example, clauses can be run before the machine learning (ML) model (that is, before any ML model score has been generated) or after a score has been generated. For example:

    Return Challenge("challenge type", "reason")
    WHEN @botScore < 900 AND @botScore > 400:

This clause throws a challenge if the bot score is between 400 and 900.

#### Types of Clauses

There are three types of clauses in DFP:

- Pre-score clause: A clause executed prior to all scoring clauses in sequential order. For example:

    RETURN Approve()
    WHEN ContainsKey("iplist", "IPAddress", @ipAddress)

- Post-bot model scoring clause: A clause executed in sequential order after bot model scoring. To use bot score in the clause, type @botScore. For example:

    RETURN Challenge("challenge type", "reason")
    WHEN @botScore < 900 AND @botScore > 400

- Post risk model scoring clause: A clause executed in sequential order after risk model scoring. To use risk score in the clause, type @riskScore. For example:

    example @riskScore
    You can add multiple clauses to a rule.

### Status

When you create and publish a new rule, you can set the status to:

- **Active**, so DFP runs in sequence when the rule is run.
- **Inactive**, so DFP skips forward in the sequence and does not run the rule.
- **Draft**, to save a copy of a rule without publishing. You can return to a draft, modify it, and publish it later.

### Payload

The Payload displays a sample of what the payload for the account protection API looks like for a given event. Changes you make in the conditions and clauses of your rule are reflected here. If you type code in the clause box that exists in the payload, DFP highlights the text in both the payload and in the clause text.

## Access the Rules management page

Use the Rules management page to manage existing rules and create custom rules.

#### To access the Rules management page:

- In the left navigation, click **Account Protection** and then click **Rules**.

The **Rules** page has two tabs:

- On the **Account creation** tab, you can create rules that check for fraud user credentials when someone is trying to create a new account.
- On the **Account login** tab, you create rules that check for fraudulent login credentials when someone logs into an existing account.

You can view the following information about rules listed on both tabs:

- The descriptive **Name** of the rule.
- The **Condition** you created for the rule.
- The **Status** of the rule (Active, Inactive, or Draft).
- A **Description** of the rule.
- The **Number of Clauses** in the rule.

You can also perform the following operations on rules listed on both tabs:

- Create a **New rule**.
- **Reorder** (change the sequence) in which multiple rules are executed. 
- **Clone** an existing rule as a basis for creating a new rule.
- **Edit** an existing draft in order to update rule that is currently in production.
- **Rename** a rule.
- **Activate/Deactivate** a rule to determine if the rule affects the assessment application programming interface (API). (add link)
- Permanently **Delete** an existing draft or rule.

## Update a rule using a saved draft

While you create a rule, DFP automatically saves your work as a draft. When you publish a rule and activate it, the rule is available to run in production mode, but you can no longer modify it.
If you want to change a file that is running in production, you can open the draft version, modify it, and then republish it. When you republish a rule, it replaces the version currently in production.

## Simplify your work with template code

When you create a new clause, you have the option of either creating the clause from scratch or using a block of sample code that is made available for your use. Each template code block performs a specific fraud protection task.

## Evaluate that a rule is running as intended

As you create a clause, DFP constantly checks the payload to confirm that the clause is working as you intended and producing the results you want. This enables you to correct your clauses as you create them.

## Using highlighting in code

If you enter code in your clause that is currently in the Payload, it highlights the text in both the payload and the clause. This enables you to reuse existing code and track changes as you make them.

## Create a rule

#### To create a rule:

1. In the left navigation, click **Account Protection** and then click **Rules**.
1. Click **Create a rule**.
1. Click the **Condition** box and enter your condition. For example:

    WHEN Geo.CountryCode(@ipAddress) == "BR"
    WHEN @username.endsWith("contoso.com")
1. Click the arrow to the left of **Prior to all scoring** and enter a clause in the box. For example:

    RETURN Approve()
    WHEN ContainsKey("iplist", "IPAddress", @ipAddress)
1. Click the arrow to the left of **Post bot model scoring** and enter a clause in the box starting with @botScore. For example:

    RETURN Challenge("challenge type", "reason")
    WHEN @botScore < 900 AND @botScore > 400
1. Click the arrow to the left of **Post risk model** scoring and enter a clause in the box starting with @riskScore. For example:

    example @riskScore
1. Click **Rename** and enter a name and description for your rule. Then click **Done**.
1. Click **Status** and then select:
    - **Active** to activate the rule.
    - **Inactive** to save the rule without activating it.
1. Click **Publish** twice to complete your rule.
1. Click the arrow to the right of the rule name to return to the **Rules** management page.

## Add a new rule

#### To add a new rule:

1. Click **New rule**.
1. Click **Templates** if you want to use an layout sample to create your own rules.
1. Click the **Condition** box and enter your condition. For example:

    WHEN Geo.CountryCode(@ipAddress) == "BR"
    WHEN @username.endsWith("contoso.com")
1. Click the arrow to the left of **Prior to all scoring** and enter a clause in the box. For example:

    RETURN Approve() 
    WHEN ContainsKey("iplist", "IPAddress", @ipAddress)
1. Click the arrow to the left of **Post bot model scoring** and enter a clause in the box starting with @botScore. For example:

    RETURN Challenge("challenge type", "reason")
    WHEN @botScore < 900 AND @botScore > 400
1. Click the arrow to the left of **Post risk model** scoring and enter a clause in the box starting with @riskScore. For example:

    example @riskScore
1. Click **Rename** and enter a name and description for your rule. Then click **Done** to save the name.
1. Click **Status** and then select:
    - **Active** to activate the rule.
    - **Inactive** to save the rule without activating it.
1. Click **Publish** twice to complete your rule.

## Update a rule

If you want to change a file that is running in production, you can open the draft version, modify it, and then republish it. When you republish a rule, it replaces the version currently in production.

#### To edit a rule:

1. Select the required draft and then click **Edit**.
1. Make the changes as required.
1. To save your changes under the same rule name, click **Update**.
1. Click **Rename** and enter a name and description for your rule. Then click **Done** to save the name.
1. Click **Status** and then select:
    - **Active** to activate the rule.
    - **Inactive** to save the rule without activating it.
1. Click **Publish** twice to complete your rule.

## Manage rules

The following operations are typically associated with rules. They are available on the DFP user interface when you select an existing rule.

- Create a **New rule**.
- **Reorder** how rules are run by changing the sequence in which multiple rules are executed.
- **Clone** an existing rule by creating a copy and using it as a basis to create a new rule.
- **Edit** an existing draft in order to update rule that is currently in production.
- **Rename** a rule.
- **Activate/Deactivate** a rule to determine if the rule affects the assessment application programming interface (API). (link)
- Permanently **Delete** an existing draft or rule.

#### To rename a rule:

1. Select a rule and click **Rename**.
1. Enter a new name and description for the rule and then click **Done**.

#### To activate or deactivate a rule:

- Select a rule and click **Activate** or **Deactivate**.

#### To delete a rule:

- Select a rule and click **Delete**.

#### To change the order of the rules:

- Click **Reorder** and then select a rule and drag it to the required location on the list.
    Or, select a rule and drag it to the required location on the list.

#### To clone an existing rule:

1. Select a rule and click **Clone**.
1. Make the changes as required.
1. Click **Rename** and enter a name and description for your rule. Then click **Done**.

#### To search for a rule:

- Click **Search**, type a keyword in the **Search** text box, and then press **Enter**.
