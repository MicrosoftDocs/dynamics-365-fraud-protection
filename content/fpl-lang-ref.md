---
author: yvonnedeq
description: This topic is a language guide for DFP rules.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 04/6/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Rules language guide 

---
# Rules language guide 

## Overview

Fraud Protection [rules](rules.md) are written in a rich and expressive language. This language contains many similarities to C# and SQL and is designed to provide you with the power and flexability you need to customize your fraud strategy and enforce unique business policies. 

To get started, read the [Quick start guide](fpl-lang-ref.md#quick-start-guide). For a complete list of available operators, review the [Language reference](fpl-lang-ref.md#language-reference). 

## Quick start guide

Rules consist of [clauses](rules.md#clauses) and are defined by the **RETURN** and **WHEN** keywords. They adhere to the following basic structure: 

      RETURN *decision* 
      WHEN *condition is true*

The **RETURN** decision is executed only if the **WHEN** expression evaluates to *True*. 

### RETURN

Your clause must return a decision of *approve*, *reject*, *challenge*, or *review*. You can also include optional parameters to send more information about the decision. Here are some examples of **RETURN** statements.

      RETURN Reject()
      RETURN Reject(“email is on block list”)
      RETURN Reject(“email is on block list”, “do not escalate”)

For information on decision types and their parameters, see [Decision types](fpl-lang-ref.md#decision-types). 

### WHEN

A **WHEN** expression contains one or more Boolean expressions. You can create multiple Boolean expressions using the **AND (&&)** and **OR (||)** [joining operators](fpl-lang-ref.md#joining-operators). 

A Boolean expression is formed by checking and/or comparing two types of variables:

- The *payload values* of the fields included in an API request for a purchase.
- The *scores* generated from Fraud Protection’s AI models.

You can access [variables](fpl-lang-ref.md#variables) with the  *@variable* syntax. To specify the full path of a variable, use *@”object.variable”*. 

When you use variables in a Boolean expression, you can:

- Compare variables to other variables or constants. 

      WHEN @email == “kayla@contoso.com”
      WHEN @”user.firstName” == @”shippingAddress.firstName”
      WHEN @riskscore > 700 
      WHEN Geo.CountryCode(@ipAddress) == “US”

- Check if a variable is contained within a list.

      WHEN ContainsKey(“Safe List”, “Emails”, @email)

- Check the value of a key within a list.

      WHEN Lookup(“Email List”, “Emails”, @email, “Status”) == “Safe”
      WHEN Lookup(“Product cutoff list”, “Product”, @productName, “Score Cutoff”).toDouble() < @riskScore

- Evaluate a string.

       WHEN @phoneNumber.StartsWith(“1-“)
       WHEN @email.EndsWith(“@contoso.com”)

## Language reference 

This section contains a complete list of operators available in Fraud Protection, including:

-	[Joining operators](fpl-lang-ref.md#joining-operators)
-	[List operators](fpl-lang-ref.md#list-operators)
-	[Comparison operators](fpl-lang-ref.md#comparison-operators)
-	[Geo operators](fpl-lang-ref.md#geo-operators)
-	[String operators](fpl-lang-ref.md#string-operators)
-	[Math operators](fpl-lang-ref.md#math-operators)
-	[DateTime operators](fpl-lang-ref.md#datetime-operators)
-	[Type casting operators](fpl-lang-ref.md#)

### Keywords

| Syntax| Description     | Example|
|-------|-----------------|--------|
|**RETURN** |<p>Must be followed by a valid [Decision type](fpl-lang-ref.md#decision-types): *Approve*, *Reject*, *Challenge*, or *Review*.</p><p>The decision can also be followed by [Other](fpl-lang-ref.md#additional-return-types), which is used to pass key value pairs.|<p>RETURN Reject()</p><p>RETURN Reject(), Other(key=@username)|
|**WHEN** |Must evaluate to a Boolean value. |WHEN @riskscore > 400|


#### Decision types

| Syntax   | Description     | Example|
|-------|-----------------|--------|
|Approve   |<p>Approves the event.</p><p>Overloads:</p><p>Approve()</p><p>Approve(String *reason*)</p><p>Approve(String *reason*, String *supportMessage*)|Approve()</p><p>Approve("on safe list")</p><p>Approve ("on safe list", “do not escalate”)</p>|
|Reject    |<p>Rejects the event.</p><p>Overloads:</p><p>Reject()</p><p>Reject(String *reason*)</p><p>Reject(String *reason*, String *supportMessage*) |Reject()</p><p>Reject("embargo country")</p><p>Return Reject()</p><p>Reject("embargo country", “do not escalate”)</p> |
|Review    |<p>Marks the transaction for further review.</p><p>Overloads:</p><p>Review()</p><p>Review(String *reason*)</p><p>Review(String *reason*, String *supportMessage*)|Review()</p><p>Review("user on watch list")</p><p>Review("user on watch list", “do not escalate”)</p>|
|Challenge |<p>Marks the transaction for further verification using the specified challenge type.</p><p>Overloads:</p><p>Challenge(String *challengeType*)</p><p>Challenge(String *challengeType*, String *reason*)</p><p>Challenge(String *challengeType*, String *reason*, String *supportMessage*)|<p>Challenge ("SMS")</p><p>Challenge ("SMS”, “suspected bot")</p><p>Challenge ("SMS”, suspected bot", “do not escalate”) |


#### Additional RETURN types

| Syntax    | Description     | Example|
|-------|-----------------|--------|
|Other  |Can be used to pass key value pairs.|Other(key="test", email=@email, countryRegion=Geo.CountryRegion(@ipAddress))|


#### Variables

For information about how to use variables, see [Type inference of variables](fpl-lang-ref.md#type-inference-of-variables).

| Syntax    | Description     | Example|
|-------|-----------------|--------|
|@	|<p>Used to reference an AI score or a variable from the event payload.</p><p>If **city** exists in multiple places in the payload, then @city will return the first occurrence.</p><p>To avoid this, specify the full path. For example @”address.city”</p><p>The type of this variable is inferred by the context in which it is used. If the variable is not found in the event payload, the default value for the inferred type is returned – 0.0 for double, empty string for strings, etc. If not enough context is provided, it defaults to *String*.</p><p>For information about type inference, see [Type inference of variables](fpl-lang-ref.md#type-inference-of-variables).|@city<br>@"address.city"|
|@botScore    |<p>Fraud Protection’s AI models generate a bot score between 0 and 999 for each Account Protection event. A higher score indicates a higher probability that the event was initiated by a bot.</p><p>You can reference this score in [post-bot-scoring clauses](rules.md#post-bot-scoring-clauses) and [post-risk-scoring clauses](rules.md#post-risk-scoring-clauses) with @botScore</p>|@botScore|
|@riskScore	|<p>Fraud Protection's AI models generate a risk score between 0 and 999 for all Purchase and Account Protection events. A higher score indicates a higher risk.</p><p>You can reference this score in post-risk-scoring clauses with @riskScore.</p>	|@riskScore |


#### Joining operators

| Syntax| Description     | Example|
|-------|-----------------|--------|
|**AND ( && )**  |Logical **And** |<p>@botScore > 500 && @riskScore > 500</p><p>@botScore > 500 AND @riskScore > 500</p> |
|**OR ( \|\| )** |Logical **Or** |<p>(@isEmailUsername == false  \|\| @isEmailValidated == false</p><p>@isEmailUsername == false OR @isEmailValidated == false</p> |


#### List operators

For information about using lists in rules, see [Using lists in rules](fpl-lang-ref.md#use-lists-in-rules).

| Syntax| Description     | Example|
|-------|-----------------|--------|
|ContainsKey |<p>Checks if a key is contained within specified column in a pre-defined [list](lists.md).</p><p>ContainsKey(String *listName*, String *columnName*, String *key*)</p> |<p>ContainsKey("Email Support List", “Emails”, @email)</p><p>This checks if column “Emails” in list “Email Support List” contains the variable @email.</p> |
|Lookup      |<p>Looks up the value of a key in a list column and returns the value as a String.</p><p>If the key is not found, and *defaultValue* is not specified, “Unknown” is returned.</p><p>Overloads<br>Lookup(String *listName*, String *keyColumnName*, String *key*, String *valueColumnName*) </p><p>Lookup(String *listName*, String *keyColumnName*, String key, String valueColumnName, String defaultValue)</p> |<p>Lookup("Email Support List", “Emails”, @email, ”Status”)</p><p>This finds the variable @email in column “Emails” of list “Email Support List”, and returns its corresponding value in column “Status”.</p> |
|LookupClosest |<p>Looks up the value of a key in a list column. If the key is not found, it returns the value for the key that is alphabetically the closest to the one you are looking for.</p><p>Lookup(String *listName*, String *keyColumnName*, String *key*, String *valueColumnName*)</p>|<p>LookupClosest("IP Addresses", “IP”, @ipAddress, ”City”) ==  ”Seattle” </p><p>This finds the variable @ipAddress in column “IP” of list “IP Addresses” and returns its corresponding value in column “City”. If @ipAddress is not found in the list, it will return the value for the next closest IP address in the list.</p>|
|In            |<p>Checks if a key is contained within a comma-separated list of values</p><p>In(String *key*, String *list*).</p>  |In(@countryRegion, "US, MX, CA")|


#### Comparison operators

Fraud protection supports all standard C# [comparison](https://docs.microsoft.com/dotnet/csharp/language-reference/operators/comparison-operators) and [equality](https://docs.microsoft.com/dotnet/csharp/language-reference/operators/equality-operators) operations. This table includes some examples of methods which may be useful to you.

| Syntax| Description     | Example|
|-------|-----------------|--------|
|== |Checks for equality. |@"user.countryRegion" == @"shippingAddress.countryRegion" |
|!= |Checks for inequality.  |@"user.countryRegion" != @"shippingAddress.countryRegion" |
|> |Checks if the first value is greater than the second value. |@riskScore > 500 |
|< |Checks if the first value is less than the second value. |@riskScore < 500 |
|>= |Checks if the first value is greater than or equal to the second value. |@riskScore >= 500 |
|<= |Checks if the first value is less than or equal to the second value. |@riskScore <= 500 |


#### Geo operators

These operators convert an IP address to a geographical address.

| Syntax| Description     | Example|
|-------|-----------------|--------|
|Geo.RegionCode    |<p>Converts an IPv4 address to its US region code (the abbreviation of the name of the US state or territory).</p><p>For example, an IP address in Washington State will return "WA."</p>| Geo.RegionCode(@ipAddr)|
|Geo.Region    |<p>Converts an IPv4 address to its US region (the name of the US state or territory).</p><p>For example, an IP address in Washington State will return "Washington."</p>    |Geo.Region(@ipAddr)|
|Geo.CountryCode    |<p>Converts an IPv4 address to its country code.</p><p>For example, an IP address in Australia will return "AU."</p>| Geo.CountryCode(@ipAddr)|
|Geo.CountryRegion    |<p>Converts an IP address to a region name.</p><p>For example, an IP address in Australia will return “Australia”.</p>|Geo.CountryRegion(@ipAddress)|
|Geo.City    |<p>Converts an IPv4 address to a city name. </p><p>For example, an IP address in New York City will return "New York City".</p>|WGeo.City(@ipAddr)|
|Geo.PostalCode    |<p>Converts an IPv4 address to its postal code.</p><p>For example, an IP address in Seattle might return "98106."|Geo.PostalCode(@ipAddr)</p>|
|Geo.Isp    |<p>Converts an IPv4 address to the Internet Service Provider (ISP) that manages that IP. </p><p>For example, an IP address might return "Level 3 Communications." </p>  |Geo.Isp(@ipAddr)|
|Geo.MarketCode    |<p>Converts an IPv4 address to the market code of the IP. </p><p>For example, an IP address from Canada will return "NA" (North America).</p><p>     |Geo.MarketCode(@ipAddr)|


#### String operators

Fraud Protection supports all .NET standard [String operators](https://docs.microsoft.com/dotnet/api/system.string?view=netframework-4.8). This table includes some examples of methods which may be useful to you.

| Syntax| Description     | Example|
|-------|-----------------|--------|
|StartsWith |<p>Checks if a string ends with a given suffix.</p><p>StartsWith(String *prefix*)</p> |@phoneNumber.StartsWith("1-") |
|EndsWith   |<p>Checks if a string ends with a given prefix.</p><p>EndsWith(String *suffix*)</p> |@email.EndsWith("@contoso.com") |
|Contains   |<p>Checks if a string contains another string.</p><p>Contains(String *substring*)</p> |@productName.Contains("Xbox") |
|Exists     |<p>Checks if a variable exists in the event payload.</p><p>Exists(String *variable*)</p>|Exists(@email)| 

#### Math operators

Fraud Protection supports all.NET’s standard [Math methods](https://docs.microsoft.com/dotnet/api/system.math?view=netframework-4.8) and all [C# arithmetic operators](https://docs.microsoft.com/dotnet/csharp/language-reference/operators/arithmetic-operators). This table includes some examples of methods which may be useful to you.

| Syntax| Description     | Example|
|-------|-----------------|--------|
|Math.Min |<p>Computes the minimum of two values.</p><p>Math.Min(Double value1, Double value2)</p> |Math.Min(@riskScore,@botScore) |
|Math.Max |<p>Computes the maximum of two values.</p><p>Math.Max(Double value1, Double value2)</p> |Math.Max(@riskScore,@botScore) |


### DateTime operators

Fraud Protection supports all .NET’s standard [DateTime](https://docs.microsoft.com/dotnet/api/system.datetime?view=netframework-4.8) properties, methods, and operators. This table includes some examples of properties which may be useful to you.

| Syntax| Description     | Example|
|-------|-----------------|--------|
|UtcNow |Gets a DateTime object that is set to the current date and time on the computer, expressed as the Coordinated Universal Time.  |DateTime.UtcNow |
|Today  |An object that is set to today’s date with the time component set to 00:00:00. |DateTime.Today |
|Year   |Gets the year component of the Date represented by this instance. |@creationDate.Year |
|Date   |Gets a new object with the same date as this instance, and the time value. |@creationDate.Date |


### Type casting operators

For information about type inferencing, see [Type inference of variables](fpl-lang-ref.md#type-inference-of-variables). 

| Syntax| Description     | Example|
|-------|-----------------|--------|
|ToDateTime() |Converts a string to a DateTime object. |@creationDate.ToDateTime() |
|ToDouble()   |Converts a string to a Double. |@purchaseAmount.ToDouble() |
|ToInt32()    |Converts a string to an Int32. |@riskScore.ToInt32() |


## Use lists in rules 

You can create a rule with a previously created [list](lists.md) with the **ContainsKey** or **Lookup** operators.

### ContainsKey

To check if a one of your lists contains a specific value, use the **ContainsKey** operation. Specify the list name, the column, and the key you want to check.

For example, you can create a single-column list of risky email addresses, titled *Risky email* list:

|Email |
|--------------|
|Kayla@contoso.com |
|Jamie@bellowscollege.com |
|Marie@atatum.com |

You can then use the following syntax to reject all transactions from “risky” email addresses in this list.

     RETURN Reject(“risky email”) 
     WHEN ContainsKey(“Risky email list”, “Email”, @email) 

This clause checks if the *Email* column in the “Risky email* list contains *email*. If it does, the transaction is rejected.

### Lookup

You can use the **Lookup** operation to look up the value of a key in a list.

For example, you can create a list titled *Email* with a column for email addresses and a column to indicate their status.

|Email address|Status|
|--------------|--------------|
|Kayla@contoso.com |Risky|
|Jamie@bellowscollege.com|Risky|
|Marie@atatum.com|Risky|
|Camille@fabrikam.com|Safe|
|Miguel@proseware.com |Safe |
|Tyler@contoso.com |Safe |

You can then use the following syntax to reject all transactions from *Risky* email addresses in this list.

    RETURN Reject(“risky email”) 
    WHEN Lookup(“Email List”, “Email”, @email, “Status”) == “Risky”

This clause finds the key *@email* in the *Email* column in the *Email* list and checks if the value in the *Status* column is *Risky*. If it is, the transaction is rejected.

If the *@email* key is not found in the list, Fraud Protection returns  *Unknown*. 

You can also specify your own default value as the fifth parameter. For more information, see [list operators](fpl-lang-ref.md#list-operators).

**Lookup** always returns a String value. To convert this value to an **Int**, **Double**, or **DateTime** value, use a [type casting operator](fpl-lang-ref.md#type-casting-operators).

## Type inference of variables

Variable types are inferred by the context in which they are used. For example:

- In the expression **WHEN @isEmailValidated**, the variable is interpreted as a Boolean value.
- In the expression **@riskScore > 500**, the variable is interpreted as a **Double** value. 
- In the expression **@creationDate.Year < DateTime.UtcNow.Year**, the variable is interpreted as a **DateTime value**. 

If there is not enough context to infer the type of a variable, it's considered a String. For example, in the expression **@riskScore < @botScore**, both variables are interpreted as strings.

To specify the type of a non-String variable, use a [type casting operator](fpl-lang-ref.md#type-casting-operators). 


