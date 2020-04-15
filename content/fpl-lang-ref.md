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

Fraud Protection [Rules](rules.md) enable you to write business logic for automated decision making. Rules are made up of [conditions]( rules.md#conditions) and [clauses](rules.md#clauses). Conditions and clauses are written in a rich and expressive language that enables you to customize the logic required to meet your unique business needs. 

Fraud Protection language has significant overlap with C# and SQL. The **RETURN** and **WHERE** keywords define the clause, and the *@field* syntax is used to extract fields from the payload. Most C# comparison and arithmetic operators are also available.

For a complete list of available operators, review the [language reference](fpl-lang-ref.md#language-reference). 

## Quick start guide

### RETURN

Clauses adhere to the following basic structure: 

      RETURN *decision* 
      WHEN *condition is true*

You can return a decision of *Approve*, *Reject*, *Challenge*, or *Review*, and include optional parameters to send more information about the decision. Here are some examples of valid RETURN statements:

      RETURN Reject()
      RETURN Reject(“email is on block list”)
      RETURN Reject(“email is on block list”, “do not escalate”)

Everything following the **WHEN** keyword must evaluate to a Boolean value. If a **WHEN** expression evaluates to *True*, the **RETURN** decision is executed. 

For information on how to use decision types and their parameters, see [Decision types](fpl-lang-ref.md#decision-types). 


### WHEN

A **WHEN** expression is made up of one or more Boolean expressions. You can string together multiple Boolean expressions using the [joining operators](fpl-lang-ref.md#joining-operators) **AND (&&)** and **OR (||)**. 

A Boolean expression is formed by checking and/or comparing variables. There are two types of variables:

- Payload values
- Scores

You can access all variables with the syntax *@variable*. For example, to specify a variable is a part of an object, you can write *@”object.variable”*. 

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

### Supported operators
FPL supports methods for [String operators](fpl-lang-ref.md#string-operators), [Math operators](fpl-lang-ref.md#math-operators), [Geo operators](fpl-lang-ref.md#geo-operators), and [DateTime](fpl-lang-ref.md#datetime-operators) types. Click the links for information and examples.

## Language reference 

### Keywords

The Fraud Protection Language (FPL) includes two keywords that you must use in each clause.

| Syntax| Description     | Example|
|-------|-----------------|--------|
|**RETURN** |Must be followed by a valid [Decision type](fpl-lang-ref.md#decision-types): Approve, Reject, Challenge, or Review.<br>The Decision can also be followed by [Other](fpl-lang-ref.md#additional-return-types), used to pass key value pairs.|RETURN Reject()<br>RETURN Reject(), Other(key=@username)|
|**WHEN** |Must evaluate to a Boolean value. |WHEN @riskscore > 400|


#### Decision types

| Syntax   | Description     | Example|
|-------|-----------------|--------|
|Approve   |Approves the event.<br>Overloads:<br>Approve()<br>Approve(String *reason*)<br>Approve(String *reason*, String *supportMessage*)|Approve()<br><br>Approve("on safe list")<br>Approve ("on safe list", “do not escalate”) |
|Reject    |Rejects the event.<br>Overloads:<br>Reject()<br>Reject(String *reason*)<br>Reject(String *reason*, String *supportMessage*) |Reject()<br><br>Reject("embargo country")<br><br>Return Reject() <br>  Reject("embargo country", “do not escalate”) |
|Review    |Marks the transaction for further review.<br>Overloads:<br>Review()<br>Review(String *reason*)<br>Review(String *reason*, String *supportMessage*)|Review()<br><br>Review("user on watch list")<br><br>Review("user on watch list", “do not escalate”) |
|Challenge |Marks the transaction for further verification using the specified challenge type.<br> Overloads:<br>Challenge(String *challengeType*)<br>Challenge(String *challengeType*, String *reason*)<br>Challenge(String *challengeType*, String *reason*, String *supportMessage*)|Challenge ("SMS")<br><br>Challenge ("SMS”, “suspected bot")<br><br>Challenge ("SMS”, suspected bot", “do not escalate”) |


#### Additional RETURN types

| Syntax    | Description     | Example|
|-------|-----------------|--------|
|Other  |Can be used to pass key value pairs to the response payload.|Other(key="test", username=@email, countryRegion=Geo.CountryRegion(@ipAddress))|


#### Variables

For information on how these variables are typed, click [type inference](link).

| Syntax    | Description     | Example|
|-------|-----------------|--------|
|@	|Used to reference an AI score or a variable from the event payload.<br>If city exists in multiple places in the payload, then @city will return the first occurrence.<br>To avoid this, specify the full path. For example @”address.city”<br>If the variable isn’t found in the event payload, the default value for that type is returned – 0.0 for double, empty string for strings, etc.|@city<br>@"address.city"|
|@botscore    |Fraud Protection’s AI models generate a bot score between 0 and 999 for each Account Protection event, with a higher score indicating a higher probability that event was initiated by a bot.<br>You can reference this score in [post-bot-scoring clauses](rules.md#post-bot-scoring-clauses) and [post-risk-scoring clauses](rules.md#post-risk-scoring-clauses) with @botScore|@botScore|
|@riskscore	|Fraud Protection's AI models generate a risk score between 0 and 999 for all Purchase and Account Protection events, with a higher score indicating a higher risk.<br>You can reference this score in post-risk-scoring clauses with @riskScore.	|@riskScore |


#### Joining operators

| Syntax| Description     | Example|
|-------|-----------------|--------|
|**AND ( && )**  |Logical **And** |@botScore > 500 && @riskScore > 500<br>@botScore > 500 AND @riskScore > 500 |
|**OR ( \|\| )** |Logical **Or** |(@isEmailUsername == false  \|\| @isEmailValidated == false<br>@isEmailUsername == false OR @isEmailValidated == false |

#### Comparison operators

| Syntax| Description     | Example|
|-------|-----------------|--------|
|== |Checks for equality. |@"user.countryRegion" == @"shippingAddress.countryRegion" |
|!= |Checks for inequality.  |@"user.countryRegion" != @"shippingAddress.countryRegion" |
|> |Checks if the first value is greater than the second value. |@riskScore > 500 |
|< |Checks if the first value is less than the second value. |@riskScore < 500 |
|>= |Checks if the first value is greater than or equal to the second value. |@riskScore >= 500 |
|<= |Checks if the first value is less than or equal to the second value. |@riskScore <= 500 |

#### List operators

For information about using lists in rules, click [Using lists in rules](link).

| Syntax| Description     | Example|
|-------|-----------------|--------|
|ContainsKey |Checks if a key is contained within specified column of a pre-defined [list](lists.md)<br>ContainsKey(String *listName*, String *columnName*, String *key*) |ContainsKey("Email Support List", “Emails”, @email)<br>This checks if the variable @email is contained in column “Emails” of list “Email Support List”  |
|Lookup      |Looks up the value of a key in a list column.<br>If the key is not found, and *defaultValue* is not specified, “Unknown” is returned.<br>Overloads<br>Lookup(String *listName*, String *keyColumnName*, String *key*, String *valueColumnName*) <br>Lookup(String *listName*, String *keyColumnName*, String key, String valueColumnName, String defaultValue) |Lookup("Email Support List", “Emails”, @email, ”Status”) ==  ”Block”<br><br>This finds the variable @email in column “Emails” of list “Email Support List”, and returns its corresponding value in column “Status” |
|In          |Checks if a key is contained within a comma-separated list of values<br>In(String *key*, String *list*)  |In(@countryRegion, "US, MX, CA")|


#### Geo operators

These operators convert an IP address to a geographical address.

| Syntax| Description     | Example|
|-------|-----------------|--------|
|Geo.RegionCode    |Converts an IPv4 address to its US region code (the abbreviation of the name of the US state or territory)<br>For example, an IP address in Washington State will return "WA."  | Geo.RegionCode(@ipAddr)|
|Geo.Region    |Converts an IPv4 address to its US region (the name of the US state or territory).<br>For example, an IP address in Washington State will return "Washington."    |Geo.Region(@ipAddr)|
|Geo.CountryCode    |Converts an IPv4 address to its country code.<br>For example, an IP address in Australia will return "AU."| Geo.CountryCode(@ipAddr)|
|Geo.CountryRegion    |Converts an IP address to a region name.<br>For example, an IP address in Australia will return “Australia”.|Geo.CountryRegion(@ipAddress)|
|Geo.City    |Converts an IPv4 address to a city name. <br>For example, an IP address in New York City will return "New York City".|WGeo.City(@ipAddr)|
|Geo.PostalCode    |Converts an IPv4 address to its postal code. <br>For example, an IP address in Seattle might return  "98106."|Geo.PostalCode(@ipAddr)|
|Geo.Isp    |Converts an IPv4 address to the Internet Service Provider (ISP) that manages that IP. <br>For example, an IP address might return "Level 3 Communications."   |Geo.Isp(@ipAddr)|
|Geo.MarketCode    |Converts an IPv4 address to the market code of the IP. <br>For example, an IP address from Canada will return "NA" (North America).     |Geo.MarketCode(@ipAddr)|


#### String operators

Fraud Protection supports all .NET standard [String operators] (https://docs.microsoft.com/en-us/dotnet/api/system.string?view=netframework-4.8). This table includes some examples of methods which may be useful to you.

| Syntax| Description     | Example|
|-------|-----------------|--------|
|StartsWith |Checks if a string ends with a given suffix. <br>StartsWith(String *prefix*) |@phoneNumber.StartsWith("1-") |
|EndsWith |Checks if a string ends with a given prefix. <br>EndsWith(String *suffix*) |@email.EndsWith("@contoso.com") |
|Contains |Checks if a string contains another string. <br>Contains(String *substring*) |@productName.Contains("Xbox") |
|Exists| Checks if a variable exists in the event payload. <br>Exists(String *variable*)|Exists(@email)| 

#### Math operators

Fraud Protection supports all.NET’s standard [Math methods](https://docs.microsoft.com/en-us/dotnet/api/system.math?view=netframework-4.8). This table includes some examples of methods which may be useful to you.

| Syntax| Description     | Example|
|-------|-----------------|--------|
|Math.Min |Computes the minimum of two values.<br>Math.Min(Double value1, Double value2) |Math.Min(@riskScore,@botScore) |
|Math.Max |Computes the maximum of two values.<br>Math.Max(Double value1, Double value2) |Math.Max(@riskScore,@botScore) |


### DateTime operators

Fraud Protection supports all .NET’s standard [DateTime](https://docs.microsoft.com/en-us/dotnet/api/system.datetime?view=netframework-4.8) properties, methods, and operators. This table includes some examples of properties which may be useful to you.

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





