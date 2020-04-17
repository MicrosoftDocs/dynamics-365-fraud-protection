---
author: yvonnedeq
description: This topic is a language guide to DFP rules.
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

Fraud Protection rules are written in a rich and expressive language. This language contains many similarities to C# and SQL, and is designed to provide you with the power and flexability you need to customize your fraud strategy and enforce unique business policies. 

To get started, read the [Quick start guide](fpl-lang-ref.md#quick-start-guide). For a complete list of available operators, review the [Language reference](fpl-lang-ref.md#language-reference). 

## Quick start guide

Rules are made up of [clauses](rules.md#clauses) which are defined by the **RETURN** and **WHEN** keywords. They adhere to the following basic structure: 

      RETURN *decision* 
      WHEN *condition is true*

The **RETURN** decision is executed only if the **WHEN** expression evaluates to *True*. 

### RETURN

Your clause must return a decision of *Approve*, *Reject*, *Challenge*, or *Review*. You can also include optional parameters to send more information about the decision. Here are some examples of valid **RETURN** statements:

      RETURN Reject()
      RETURN Reject(“email is on block list”)
      RETURN Reject(“email is on block list”, “do not escalate”)

For information on how to use decision types and their parameters, see [Decision types](fpl-lang-ref.md#decision-types). 

### WHEN

A **WHEN** expression is made up of one or more Boolean expressions. You can string together multiple Boolean expressions using the [Joining operators](fpl-lang-ref.md#joining-operators), **AND (&&)** and **OR (||)**. 

A Boolean expression is formed by checking and/or comparing variables. There are two types of variables:

- Payload values
- Scores

You can access all variables with the syntax *@variable*. To specify the full path of a variable, you can write *@”object.variable”*. 

To use variables to form a Boolean expression, you can:

- Compare variables to other variables or constants. 

      WHEN @email == “kayla@contoso.com”
      WHEN @”user.firstName” == @”shippingAddress.firstName”
      WHEN @riskscore > 700 
      WHEN Geo.CountryCode(@ipAddress) == “US”

- Check if a variable is contained within a list.

      WHEN ContainsKey(“Safe List”, “Emails”, @email)

- Check the value of a key within a list.

      WHEN Lookup(“Email List”, “Emails”, @email, “Status”) == “Safe”
      WHEN Lookup(“Country List”, “Country”, @country, “Score Cutoff”) < @riskScore

- Evaluate a string.

       WHEN @phoneNumber.startsWith(“1-“)
       WHEN @email.endsWith(“@contoso.com”)

Review the [Language reference](fpl-lang-ref.md#language-reference) for a complete list of available operators, including:

-	[Joining operators](fpl-lang-ref.md#joining-operators)
-	[List operators](fpl-lang-ref.md#list-operators)
-	[Comparison operators](fpl-lang-ref.md#comparison-operators)
-	[Geo operators](fpl-lang-ref.md#geo-operators)
-	[String operators](fpl-lang-ref.md#string-operators)
-	[Math operators](fpl-lang-ref.md#math-operators)
-	[DateTime operators](fpl-lang-ref.md#datetime-operators)
-	[Type casting operators](fpl-lang-ref.md#)


## Language reference 

### Keywords

The Fraud Protection Language (FPL) includes two keywords that you must use in each clause.

| Syntax| Description     | Example|
|-------|-----------------|--------|
|**RETURN** |<p>Must be followed by a valid [Decision type](fpl-lang-ref.md#decision-types): Approve, Reject, Challenge, or Review.</p><p>The Decision can also be followed by [Other](fpl-lang-ref.md#additional-return-types), used to pass key value pairs.|<p>RETURN Reject()</p><p>RETURN Reject(), Other(key=@username)|
|**WHEN** |Must evaluate to a Boolean value. |WHEN @riskscore > 400|


#### Decision types

| Syntax   | Description     | Example|
|-------|-----------------|--------|
|Approve   |<p>Approves the event.</p><p>Overloads:<br>Approve()</p><p>Approve(String *reason*)</p><p>Approve(String *reason*, String *supportMessage*)|Approve()</p><p>Approve("on safe list")</p><p>Approve ("on safe list", “do not escalate”)</p>|
|Reject    |<p>Rejects the event.</p><p>Overloads:</p><p>Reject()</p><p>Reject(String *reason*)</p><p>Reject(String *reason*, String *supportMessage*) |Reject()</p><p>Reject("embargo country")</p><p>Return Reject()</p><p>Reject("embargo country", “do not escalate”)</p> |
|Review    |<p>Marks the transaction for further review.</p><p>Overloads:</p><p>Review()</p><p>Review(String *reason*)</p><p>Review(String *reason*, String *supportMessage*)|Review()</p><p>Review("user on watch list")</p><p>Review("user on watch list", “do not escalate”)</p>|
|Challenge |<p>Marks the transaction for further verification using the specified challenge type.</p><p>Overloads:</p><p>Challenge(String *challengeType*)</p><p>Challenge(String *challengeType*, String *reason*)</p><p>Challenge(String *challengeType*, String *reason*, String *supportMessage*)|<p>Challenge ("SMS")</p><p>Challenge ("SMS”, “suspected bot")</p><p>Challenge ("SMS”, suspected bot", “do not escalate”) |


#### Additional RETURN types

| Syntax    | Description     | Example|
|-------|-----------------|--------|
|Other  |Can be used to pass key value pairs.|Other(key="test", username=@email, countryRegion=Geo.CountryRegion(@ipAddress))|


#### Variables

For information on how these variables are typed, click [type inference](fpl-lang-ref.md#type-inference).

| Syntax    | Description     | Example|
|-------|-----------------|--------|
|@	|<p>Used to reference an AI score or a variable from the event payload.</p><p>If city exists in multiple places in the payload, then @city will return the first occurrence.</p><p>To avoid this, specify the full path. For example @”address.city”</p><p>If the variable isn’t found in the event payload, the default value for that type is returned – 0.0 for double, empty string for strings, etc.</p>|@city<br>@"address.city"|
|@botscore    |<p>Fraud Protection’s AI models generate a bot score between 0 and 999 for each Account Protection event, with a higher score indicating a higher probability that event was initiated by a bot.</p><p>You can reference this score in [post-bot-scoring clauses](rules.md#post-bot-scoring-clauses) and [post-risk-scoring clauses](rules.md#post-risk-scoring-clauses) with @botScore</p>|@botScore|
|@riskscore	|<p>Fraud Protection's AI models generate a risk score between 0 and 999 for all Purchase and Account Protection events, with a higher score indicating a higher risk.</p><p>You can reference this score in post-risk-scoring clauses with @riskScore.</p>	|@riskScore |


#### Joining operators

| Syntax| Description     | Example|
|-------|-----------------|--------|
|**AND ( && )**  |Logical **And** |<p>@botScore > 500 && @riskScore > 500</p><p>@botScore > 500 AND @riskScore > 500</p> |
|**OR ( \|\| )** |Logical **Or** |<p>(@isEmailUsername == false  \|\| @isEmailValidated == false</p><p>@isEmailUsername == false OR @isEmailValidated == false</p> |


#### List operators

For additional information about using lists in rules, click [Using lists in rules](fpl-lang-ref.md#using-lists-in-rules).

| Syntax| Description     | Example|
|-------|-----------------|--------|
|ContainsKey |<p>Checks if a key is contained within specified column of a pre-defined [list](lists.md).</p><p>ContainsKey(String *listName*, String *columnName*, String *key*)</p> |<p>ContainsKey("Email Support List", “Emails”, @email)</p><p>This checks if the variable @email is contained in column “Emails” of list “Email Support List” </p> |
|Lookup      |<p>Looks up the value of a key in a list column.</p><p>If the key is not found, and *defaultValue* is not specified, “Unknown” is returned.</p><p>Overloads<br>Lookup(String *listName*, String *keyColumnName*, String *key*, String *valueColumnName*) </p><p>Lookup(String *listName*, String *keyColumnName*, String key, String valueColumnName, String defaultValue)</p> |<p>Lookup("Email Support List", “Emails”, @email, ”Status”) ==  ”Block”</p><p>This finds the variable @email in column “Emails” of list “Email Support List”, and returns its corresponding value in column “Status”</p> |
|In          |Checks if a key is contained within a comma-separated list of values<br>In(String *key*, String *list*)  |In(@countryRegion, "US, MX, CA")|


#### Comparison operators

Fraud protection supports all standard C# comparison and equality operations. This table includes some examples of methods which may be useful to you.

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
|Geo.RegionCode    |<p>Converts an IPv4 address to its US region code (the abbreviation of the name of the US state or territory)</p><p>For example, an IP address in Washington State will return "WA."</p>| Geo.RegionCode(@ipAddr)|
|Geo.Region    |<p>Converts an IPv4 address to its US region (the name of the US state or territory).</p><p>For example, an IP address in Washington State will return "Washington."</p>    |Geo.Region(@ipAddr)|
|Geo.CountryCode    |<p>Converts an IPv4 address to its country code.</p><p>For example, an IP address in Australia will return "AU."</p>| Geo.CountryCode(@ipAddr)|
|Geo.CountryRegion    |<p>Converts an IP address to a region name.</p><p>For example, an IP address in Australia will return “Australia”.</p>|Geo.CountryRegion(@ipAddress)|
|Geo.City    |<p>Converts an IPv4 address to a city name. </p><p>For example, an IP address in New York City will return "New York City".</p>|WGeo.City(@ipAddr)|
|Geo.PostalCode    |<p>Converts an IPv4 address to its postal code.</p><p>For example, an IP address in Seattle might return  "98106."|Geo.PostalCode(@ipAddr)</p>|
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

Fraud Protection supports all.NET’s standard [Math methods](https://docs.microsoft.com/dotnet/api/system.math?view=netframework-4.8) as well as all [C# arithmetic operators](https://docs.microsoft.com/dotnet/csharp/language-reference/operators/arithmetic-operators). This table includes some examples of methods which may be useful to you.

| Syntax| Description     | Example|
|-------|-----------------|--------|
|Math.Min |<p>Computes the minimum of two values.</p><p>Math.Min(Double value1, Double value2)</p> |Math.Min(@riskScore,@botScore) |
|Math.Max |<p>Computes the maximum of two values.</p><p>Math.Max(Double value1, Double value2)</p> |Math.Max(@riskScore,@botScore) |


### DateTime operators

Fraud Protection supports all .NET’s standard [DateTime](https://docs.microsoft.com/dotnet/api/system.datetime?view=netframework-4.8) properties, methods, and operators. This table includes some examples of properties which may be useful to you.

| Syntax| Description     | Example|
|-------|-----------------|--------|
|UtcNow |Gets a DateTime object that is set to the current date and time on the computer, expressed as the Coordinated Universal Time.  |DateTime.UtcNow |
|Today  |An object that is set to today’s date with the time component set to 00:00:00. |DateTime.UtcNow |
|Year   |Gets the year component of the Date represented by this instance. |@creationDate.Year |
|Date   |A new object with the same date as this instance, and the time value. |@creationDate.Date |


### Type casting operators

For more information about type inferencing, click [Type inference](fpl-lang-ref.md#type-inference). 

| Syntax| Description     | Example|
|-------|-----------------|--------|
|ToDateTime() |Converts a string to a DateTime object. |@creationDate.ToDateTime() |
|ToDouble()   |Converts a string to a Double. |@purchaseAmount.ToDouble() |
|ToInt32()    |Converts a string to an Int32. |@riskScore.ToInt32() |


## Using lists in rules 

You can create a rule with a previously created [list](lists.md) using either the **ContainsKey** or **Lookup** operators.

### ContainsKey

To check if a specific value is contained in one of your lists, use the **ContainsKey** operation. Specify the list name, the column, and the key you want to check.

For example, if you have a single-column list of risky email addresses, titled *Risky email* list

|Email |
|--------------|
|Kayla@contoso.com |
|Jamie@bellowscollege.com |
|Marie@atatum.com |

You can reject all transactions from emails in this list using the following syntax:

     RETURN Reject(“risky email”) 
     WHEN ContainsKey(“Risky email list”, “Email”, @username) 

This clause  checks if the *Email* column in the *Risky email* list contains *@username*. If it does, the transaction is rejected.

### Lookup

To look up the value of a key in a list, use the **Lookup** operation.

For example, if you have list titled *Email* list with a column for emails, and a column to indicate the status of that email:

|Email address|Status|
|--------------|--------------|
|Kayla@contoso.com |Risky|
|Jamie@bellowscollege.com|Risky|
|Marie@atatum.com|Risky|
|Camille@fabrikam.com|Safe|
|Miguel@proseware.com |Safe |
|Tyler@contoso.com |Safe |

You can reject all transactions from emails in this list which are marked as risky using the below syntax:

    RETURN Reject(“risky email”) 
    WHEN Lookup(“Email List”, “Email”, @username, “Status”) == “Risky”

This clause finds the key *@username* in the *Email* column of the *Email* list and checks if the value in the *Status* column is *Risky*. If it is, the transaction is rejected.

If the key is not found in the list, by default, *Unknown* is returned. 

You can also specify your own default value as a fifth parameter. See [list operators](fpl-lang-ref.md#list-operators) for more information. 

## Type inference

The default type of variables extracted using the @ operator, as well as the variables extracted from lists using the Lookup operation, is *String*. The inferred type may change depending on the context. For example:

-	In the expression WHEN @isEmailValidated, @isEmailValidated is interpreted as a Boolean value.
-	In the expression @riskScore > 500, @riskScore is interpreted as a Double value. 
- In the expression @creationDate.Year < DateTime.UtcNow.Year, @creationDate is interpreted as a DateTime value. 

You can also specify the type of a variable by using a [type casting operator](fpl-lang-ref.md#type-casting-operators). 


