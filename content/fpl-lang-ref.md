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
title: Fraud Protection language guide 

---
# Fraud Protection language guide 

## Overview

Fraud Protection [Rules](rules.md) enable you to write business logic for automated decision making. Rules are made up of [conditions]( rules.md#conditions) and [clauses](rules.md#clauses). Clauses are written in a rich and expressive language that enables you to customize the logic required to meet your unique business needs. 

Fraud Protection language has significant overlap with C# and SQL. The **RETURN** and **WHERE** keywords define the clause and the *@field* syntax is used to extract fields from the payload. Most C# comparison and arithmetic operators are also available. Review the [language reference](fpl-lang-ref.md#language-reference) for a complete list of available operators. 

## Quick start guide

### RETURN

Clauses adhere to the following basic structure: 

      RETURN decision 
      WHEN condition is true

You can return a decision of *Approve*, *Reject*, *Challenge*, or *Review*, and include optional parameters to send more information about the decision. For example:

      RETURN Reject()
      RETURN Reject(“email is on block list”)
      RETURN Reject(“email is on block list”, “do not escalate”)

For information about how to use  decision types and their parameters, see [Decision types](fpl-lang-ref.md#decision-types). 

Everything following the WHEN keyword must evaluate to a Boolean value. If a **WHEN** expression evaluates to *True*, the **RETURN** decision is executed. 

### WHEN

A **WHEN** expression is made up of one or more Boolean expressions. You can string together multiple Boolean expressions using the [joining operators](fpl-lang-ref.md#joining-operators) **AND (&&)** and **OR (||)**. 

A Boolean expression is formed by checking and/or comparing variables. These variables come in two forms:

- Payload values
- Scores

You can access all variables with the syntax *@variable*. To specify a variable is a part of an object, you can write *@”object.variable”*. 

Fraud Protection language also provides functions that allow you to extract certain information from variables. For example, you can use a class of [Geo operators](fpl-lang-ref.md#geo-operators) to convert an IP address to a geographical address.

To use variables to form a Boolean expression, you can:

- [Compare](fpl-lang-ref.md#comparison-operators) variables to other variables, or to constants. 

      WHEN @email == “kayla@contoso.com”
      WHEN @”user.firstName” == @”shippingAddress.firstName”
      WHEN @riskscore > 700 
      WHEN Geo.CountryCode(@ipAddress) == “US”

- Check if a variable is contained within a [list](fpl-lang-ref.md#list-operators-1).

      WHEN ContainsKey(“Safe List”, “Emails”, @email)

- Check the value of a key within a [list](fpl-lang-ref.md#list-operators-1).

      WHEN Lookup(“Email List”, “Emails”, @email, “Status”) == “Safe”
      WHEN Lookup(“Country List”, “Country”, @country, “Score Cutoff”) < @riskScore

- Evaluate a [string](fpl-lang-ref.md#string-operators).

       WHEN @phoneNumber.startsWith(“1-“)
       WHEN @email.endsWith(“@contoso.com”)

## Advanced topics

### Typing


### List operators


### Supported operators
FPL supports methods for [String operators](fpl-lang-ref.md#string-operators), [Math operators](fpl-lang-ref.md#math-operators), [Geo operators](fpl-lang-ref.md#geo-operators), and [DateTime](fpl-lang-ref.md#datetime-types) types. Click the links for information and examples.

### Lists 
You can create a rule with a previously created [custom list](lists.md). To check if a specific value is contained in one of your lists, use the **ContainsKey** operation. Specify the list name, the column, and the key you want to check.
For example, if you have a single-column list of risky email addresses, titled *Risky email* list

|Risky email |
|--------------|
|Kayla@contoso.com |
|Jamie@bellowscollege.com |
|Marie@atatum.com |

You can add a clause to your rule to check membership in the *Risky email* list. For example:

      RETURN Reject(“in risky email list”) 
      WHEN ContainsKey(“Risky Email List”, “Risky Emails”, @username) 

When you run this rule, Fraud Protection checks if the *Risky emails* column in the Risky email list contains *@username*.

### The Lookup operator

You can create a rule with the **Lookup** operator to check the value of an entry in a specific list.  
First, you create a list of all email address marked either *Safe* or *Risky*. For example: 

|Email address|Status|
|--------------|--------------|
|Kayla@contoso.com |Risky|
|Jamie@bellowscollege.com|Risky|
|Marie@atatum.com|Risky|
|Camille@fabrikam.com|Safe|
|Miguel@proseware.com |Safe |
|Tyler@contoso.com |Safe |

Next, you create a rule using the Lookup operator to check if an email address is marked either *Safe* or *Risky*.
When you write the **Lookup** clause, specify the list you want to check (*Email* list), the column heading you want to check (*Emails*), the key you’re looking for (*username*), and the column name of the value you want to extract (*Status*). For example: 

      Lookup(“Email List”, “Emails”, @username, “Status”)

When you run the rule, if any username represented by *@username* is located, Fraud Protection will return the corresponding status. For example:

      RETURN Reject(“email marked as risky”) 
      WHEN Lookup(“Email List”, “Emails”, @username, “Status”) == “Risky” 

### Decision parameters


### Examples of clauses


## Language reference 

### Keywords

The Fraud Protection Language (FPL) includes two keywords that you must use in each clause.

| Syntax| Description     | Example|
|-------|-----------------|--------|
|**RETURN** |User defined clauses that return a decision based on specific conditions. Clauses run in sequential order based on user-defined settings.|Return Approve()<br>WHEN ContainsKey("iplist", "IPAddress", @ipAddress)|
|**WHEN** |Accepts transaction based on user-defined settings. |Return Approve()<br>WHEN ContainsKey("iplist", "IPAddress", @ipAddress) |
| |Rejects transaction based on user-defined settings. |Return Reject()<br>WHEN ContainsKey("iplist", "IPAddress", @ipAddress) |
| |Throws a challenge if user-defined settings are met or not met. |Return Challenge("challenge type", "reason")<br>WHEN @botScore < 900 AND @botScore > 400 |

#### Decision types

| Syntax   | Description     | Example|
|-------|-----------------|--------|
|Approve   |Accepts transaction based on user-defined settings.                 |Return Approve()<br>WHEN ContainsKey(“iplist”, “IPAddress”, @ipAddress) |
|Reject    |Rejects transaction on user-defined settings.                       |Return Reject()<br>WHEN ContainsKey(“iplist”, “IPAddress”, @ipAddress) |
|Review    |                                                                    |(reason = "") |
|Challenge |Throws a challenge if user-defined settings are met or are not met. |Return Challenge(“challenge type", "reason")<br>WHEN @botScore < 900 AND @botScore > 400 |

#### Variables

| Syntax    | Description     | Example|
|-------|-----------------|--------|
|@          |Looks up a specified variable.                                    |@field @"findthis.thenthis.thenthis"|
|@botscore  |A clause executed in sequential order after bot model scoring.    |RETURN Challenge(“challenge type", "reason")<br>WHEN @botScore < 900 AND @botScore > 400 |
|@riskscore |A clause executed in sequential order after risk model scoring.   |@riskscore |



#### Joining operators

| Syntax| Description     | Example|
|-------|-----------------|--------|
|**AND ( && )** |Logical **And** returns the Boolean value TRUE if either or both operands are TRUE and returns FALSE otherwise. |(x < 10 && y > 1) is true |
|**OR ( \|\| )** |Logical **Or** returns the Boolean value TRUE if either or both operands are TRUE and returns FALSE otherwise. |(x == 5 \|\| y == 5) is false |

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
|In      |Finds the value of the specified variable and checks if its value exists in the list of comma-separated tokens. Search is not case-sensitive and does not require spaces after commas.|In(@hello, "abc,xyz,mag")|

#### String operators

These operators verify that the object on the left side of the operator is equal to the string object on the right side.

| Syntax| Description     | Example|
|-------|-----------------|--------|
|StartsWith |Returns a value after determining that the beginning of this string instance matches the specified string. |(string)@ExceptionName.StartsWith("Argument") |
|EndsWith |Returns a value after determining that the end of this string instance matches a specified string. |(string)@ExceptionName.EndsWith("Error") |
|Contains |Returns a value indicating whether a specified character occurs within this string |(string)@ExceptionName.Contains("Argument") |
|IndexOf | | |
|IsNullOrEmpty | | |
|Exists| Checks if the variable name exists in the string|@ext.Exists(@field)    select Exists(@ext)| 

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
|TruncateTo  |Rounds the DateTime toward the past based on the timeSpan. |(DateTime)@time.TruncateTo(TimeSpan.FromDays(1))<br>DateTime.UtcNow.TruncateTo(TimeSpan.FromMinutes(1))|
|TruncateToMillisecond|Returns the DateTime rounded to the past millisecond. |(DateTime)@time.TruncateToMillisecond()|
|TruncateToMinute|Returns the DateTime rounded to the past minute. |(DateTime)@time.TruncateToMinute()|
|TruncateToHour|Returns the DateTime rounded to the past hour. |(DateTime)@time.TruncateToHour()|
|TruncateToDay|Returns the DateTime rounded to the past day. |(DateTime)@time.TruncateToDay()|
|TruncateToWeek|Returns the DateTime rounded to the past week. |(DateTime)@time.TruncateToWeek()|
|TruncateToMonth|Returns the DateTime rounded to the past month. |(DateTime)@time.TruncateToMonth()|
|TruncateToYear |Returns the DateTime rounded to the past year. |(DateTime)@time.TruncateToYear()|




### Typing

| Syntax| Description     | Example|
|-------|-----------------|--------|
| | | |
| | | |

### Additional RETURN types

| Syntax| Description     | Example|
|-------|-----------------|--------|
|Other | | |
| | | |





