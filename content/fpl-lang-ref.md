---
author: yvonnedeq
description: This topic is a language reference guide to FDL.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 04/6/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Fraud Protection Language Reference Guide 

---
# Fraud Protection Language Reference Guide

## Using Fraud Protection Language with Rules

The Fraud Protection Language (FPL) includes two keywords that you use in every clause: **RETURN** and **WHEN**.

### The RETURN keyword

**RETURN** is a required element in any valid FPL clause. The keyword **RETURN** is followed by a decision type, which determines how a transaction is handled.

#### Decision Types

**RETURN** has four decision types.

| Syntax           | Description     | Example |
|------------------|-----------------|---------|
|**Approve**|Accepts transaction based on user-defined settings.|Return Approve() WHEN ContainsKey("iplist", "IPAddress", @ipAddress)|
|**Reject**    |Rejects transaction on user-defined settings.|Return Reject()WHEN ContainsKey("iplist", "IPAddress", @ipAddress)|
|**Review**|   |(reason = "")
|**Challenge** |Throws a challenge if user-defined settings are met or are not met.| Return Challenge("challenge type", "reason") WHEN @botScore < 900 AND @botScore > 400|

#### Parameters

Each decision type has at least two optional parameters: **Reason** and **SupportMessage**. Both parameters are represented with strings.

- The **Reason** parameter expresses the reason for the decision.
- The **SupportMessage** parameter provides a space for additional text specific to that decision. For example, you can use this parameter to alert a support agent that a transaction was rejected due to geofencing laws, and should not be escalated (moved forward to the next rule).

##### Using parameters with the Approve, Reject, and Review decision types

For the **Approve**, **Reject**, and **Review** decision types, Reason is assumed to be the first parameter. and SupportMessage is assumed to be the second parameter. For example:

    RETURN Approve("myreason", "mymessage"). 
You can specify a **Reason** without a **SupportMessage** by including only the first parameter:

    RETURN Approve("myreason"). 
You can specify a **supportMessage** without a **Reason** by including only the second parameter:

    RETURN Approve(supportMessage="mymessage"). 
And you can choose not to specify either parameter:

    RETURN Approve() 

##### Using parameters with the Challenge decision type

For **Challenge**, the first parameter is always **challengeType** (for example, SMS), and is required.

**Reason** and **SupportMessage** are optional parameters and follow the same patterns as the examples above. For example:

    RETURN Challenge("SMS", "reason", "message") 
or

    Challenge("SMS"). 

### THe WHEN keyword

Everything that follows **WHEN** must evaluate to a Boolean value.

If the **WHEN** expression evaluates to True, the RETURN decision is executed. 
In constructing a **WHEN** expression, you can string together multiple Boolean expressions using the logical operators **AND (&&)** and **OR (||)**. Basic comparison operators such as **==**, **>**, **<**, **!=** are also supported.

To reference a variable in the payload, or a variable returned from model evaluation, preface the variable name with the @ operator. For example:
    @username
or
    @botscore)

This is an example of a valid clause:
    RETURN Approve("whitelisted user")
    WHEN @username == johndoe@gmail.com

### Using operators in rules

FPL also supports methods for **String** operators, **Math** operators, **Geo** operators, and **DateTime** types. Click the links for more information and examples about the operators.

#### Using the Lookup operator in a rule

You can create a rule with the Lookup operator to check the value of an entry within a specific list.

First, you create a list of all email address marked either Safe or Risky. For example:

|**Risky Emails**|**Status**|
|---------|---------|
|alia@gmail.com|Safe|
|sarah@gmail.com|Risky|
|michael@gmail.com|Risky|
|jake@gmail.com|Safe|

Then, you create a rule using the Lookup operator to check if an email address is marked either *Safe* or *Risky*. 
In the Lookup clause, specify the List you want to check (****Email List*), the column heading within that list you want to check (*Emails*), the key you're looking for (*username*), and the column name of the value you'd like to extract (*Status*). For example:

    Lookup("Email List", "Emails", @username, "Status")

When you run the rule, if any username represented by @username is located, it will return the corresponding status. If @username is not contained within the list, it will return a default return ???. 

This is an example of a clause using the Lookup operation:

    RETURN Reject("email marked as risky")
    WHEN Lookup("Email List", "Emails", @username, "Status") == "Risky"

### Using lists in rules

You can use any custom List you've previously created in your Rules. To check if a specific value is contained in one of your Lists, use the **ContainsKey** operation. Specify the **List** name you want to check, the column name within that *List* to look in, and the key to check for.
For example, if you have a single-column **List** of risky email addresses, titled **Risky Email List**, as shown below:

You can add a clause to your rule to check membership in the Risky Email List. For example:

    RETURN Reject("in risky email list")
    WHEN ContainsKey("Risky Email List", "Risky Emails", @username)

When you run this rule, DFP checks if *@username* is contained in the *Risky Emails* column within the *Risky Email* List.


## Fraud Protection Language Reference Guide

> [!NOTE]
> Rule syntax is not case-sensitive.

### Keywords

The Fraud Protection Language (FPL) includes two keywords that you must use in each clause.

| Syntax| Description     | Example|
|-------|-----------------|--------|
|**RETURN** |User defined clauses that return a decision based on specific conditions. Clauses run in sequential order based on user-defined settings.|Return Approve() WHEN ContainsKey("iplist", "IPAddress", @ipAddress)|
|**WHEN** |Accepts transaction based on user-defined settings. |Return Approve() WHEN ContainsKey("iplist", "IPAddress", @ipAddress) |
| |Rejects transaction based on user-defined settings. |Return Reject() WHEN ContainsKey("iplist", "IPAddress", @ipAddress) |
| |Throws a challenge if user-defined settings are met or not met. |Return Challenge("challenge type", "reason") WHEN @botScore < 900 AND @botScore > 400 |

### Logical operators

These operators take inputs that are either *True* (1) or *False* (0) and produce a single output value that is also either *True* or *False*.

#### Joining operators

These operators compare their operands.

| Syntax| Description     | Example|
|-------|-----------------|--------|
|**AND ( && )** |Logical **And** returns the Boolean value TRUE if either or both operands are TRUE and returns FALSE otherwise. |(x < 10 && y > 1) is true |
|**OR ( || )** |Logical **Or** returns the Boolean value TRUE if either or both operands are TRUE and returns FALSE otherwise. |(x == 5 || y == 5) is false |

#### Comparison operators

| Syntax| Description     | Example|
|-------|-----------------|--------|
|- |Returns inputs that do not contain the specified value. | |
|== |Checks for equality and returns *True* (1) if both operands have the same value; otherwise, it returns *False* (0). | |
|!= |Checks for inequality and returns *True* (1) if the operands do not have the same value; otherwise, it returns *False* (0). | |
|> |Checks if the first value is greater than the second value; otherwise, it returns *False* (0). | |
|>= |Checks if the first value is greater than or equal to the second value; otherwise, it returns *False* (0). | |
|<> |Checks if the first value is less than the second value; otherwise, it returns *False* (0). | |
|<=> |Checks if the first value is less than or equal to the second value; otherwise, it returns *False* (0). | |

#### List operators

| Syntax| Description     | Example|
|-------|-----------------|--------|
|ContainsKey("dataset name", "index name", @index_key) |Checks whether a key is being mapped. | |
|Lookup("dataset name", "index name", @index_key, "value name") |Returns a value from a one-row, a one-column range, or from an array. | |

#### String operators

These operators verify that the object on the left side of the operator is equal to the string object on the right side.

| Syntax| Description     | Example|
|-------|-----------------|--------|
|StartsWith |Returns a value after determining that the beginning of this string instance matches the specified string. |(string)@ExceptionName.StartsWith("Argument") |
|EndsWith |Returns a value after determining that the end of this string instance matches a specified string. |(string)@ExceptionName.EndsWith("Error") |
|Contains |Returns a value indicating whether a specified character occurs within this string |(string)@ExceptionName.Contains("Argument") |
|IndexOf | | |
|IsNullOrEmpty | | |

#### Math operators

These operators use a symbol that indicates the operation to be performed.

| Syntax| Description     | Example|
|-------|-----------------|--------|
|Math.Min |Computes the minimum of two values. |Math.Min(@number) |
|Math.Max |Computes the maximum of two values. |Math.Max(@number) |


#### Geo operators

These operators convert an IP address to a geographical address.

| Syntax| Description     | Example|
|-------|-----------------|--------|
|Geo.RegionCode    |Converts an IPv4 address to its US region code. The region code is the abbreviation of the name of the state or territory. For example, an IP address from Washington State will turn into the region code "WA."    |What is the region code of the IP address at the field "ipAddr"? Geo.RegionCode(@ipAddr)|
|Geo.Region    |Converts an IPv4 address to its US region code (the abbreviation of the name of the state or territory). For example, an IP address from Washington State will turn into the region code "WA."    |What is the region name of the IP address at the field "ipAddr"? Geo.Region(@ipAddr)|
|Geo.CountryCode    |Converts an IPv4 address to its country code. For example, an IP address in Australia will turn into "AU."    |What is the country code of the IP address at the field "ipAddr"? Geo.CountryCode(@ipAddr)|
|Geo.CountryRegion    |Converts an IP address to a region name.    |Geo.Region(@clientIp)|
|Geo.City    |Converts an IPv4 address to a city name. For example, an IP address in New York City will turn into "New York City."    |What is the city of the IP address at the field "ipAddr"? Geo.City(@ipAddr)|
|Geo.PostalCode    |Converts an IPv4 address to its postal code. For example, an IP address in Seattle might turn into "98106."    |What is the postal code of the IP address at the field "ipAddr"? Geo.PostalCode(@ipAddr)|
|Geo.Isp    |Converts an IPv4 address to the Internet Service Provider (ISP) that manages that IP. For example, an IP address might turn into "Level 3 Communications."    |What is the ISP of the IP address at the field "ipAddr"? Geo.Isp(@ipAddr)|
|Geo.MarketCode    |Converts an IPv4 address to the market code of the IP. For example, an IP address from Canada will turn into "NA" (North America).     |What is the market code of the IP address at the field "ipAddr"? Geo.MarketCode(@ipAddr)|


### DateTime types

| Syntax| Description     | Example|
|-------|-----------------|--------|
| | | |
| | | |


### Variables

| Syntax| Description     | Example|
|-------|-----------------|--------|
|@    |Looks up a specified variable.    |@field @"findthis.thenthis.thenthis"|
|@botscore    |A clause executed in sequential order after bot model scoring.    |RETURN Challenge("challenge type", "reason") WHEN @botScore < 900 AND @botScore > 400|
|@riskscore    |A clause executed in sequential order after risk model scoring.    |@riskScore|


### Miscellaneous

| Syntax| Description     | Example|
|-------|-----------------|--------|
|Exists    |Checks if the variable name exists in the string    |@ext.Exists(@field) select Exists(@ext)|
|In    |Finds the value of the specified variable and checks if its value exists in the list of comma-separated tokens. Note that Search is not case-sensitive and does not require spaces after commas.    |In(@hello, "abc,xyz,mag")|
|Other    |    | |

