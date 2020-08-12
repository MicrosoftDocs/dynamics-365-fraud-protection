---
author: yvonnedeq
description: This topic is a language guide for Microsoft Dynamics 365 Fraud Protection rules.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 08/12/2020
ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Rules language guide 

---
# Rules language guide

## Overview

Microsoft Dynamics 365 Fraud Protection [rules](rules.md) are written in a rich and expressive language. This language has many similarities to C# and SQL, and is designed to give you the power and flexibility that you need to customize your fraud strategy and enforce unique business policies.

To get started, read the [Quick start guide](fpl-lang-ref.md#quick-start-guide) that follows. For a complete list of available operators, see the [Language reference](fpl-lang-ref.md#language-reference) later in this topic.

## Quick start guide

Rules consist of [clauses](rules.md#clauses), and are defined by the **RETURN** and **WHEN** keywords. They have the following basic structure.

```ruleslanguage
RETURN *decision* 
WHEN *condition is true*
```

The **RETURN** decision is run only if the **WHEN** expression is evaluated to *True*.

### RETURN

Your clause must return a decision of *Approve*, *Reject*, *Challenge*, or *Review*. You can also include optional parameters to send more information about the decision. Here are some examples of **RETURN** statements.

```ruleslanguage
RETURN Reject()
RETURN Reject("email is on block list")
RETURN Reject("email is on block list", "do not escalate")
```

For information about decision types and their parameters, see the [Decision types](fpl-lang-ref.md#decision-types) section later in this topic.

In addition to a decision type, you can also return additional functions, such as Other or Trace. For more information, see [Additional return types](fpl-lang-ref.md#additional-return-types) section later in this topic.

### WHEN

A **WHEN** expression contains one or more Boolean expressions. You can create multiple Boolean expressions by using the **AND (&&)** and **OR (||)** [joining operators](fpl-lang-ref.md#joining-operators).

A Boolean expression is formed by checking and/or comparing two types of variables:

- The *payload values* of the fields that are included in an application programming interface (API) request for a purchase.
- The *scores* that are generated from Fraud Protection's artificial intelligence (AI) models.

You can access [variables](fpl-lang-ref.md#variables) using the following syntax: *@"object.field"*. For example, *@"user.firstName"*.

When you use variables in a Boolean expression, you can perform the following tasks:

- Compare variables to other variables, or to constants.

```ruleslanguage
WHEN @"user.email" == "kayla@contoso.com"
WHEN @"user.firstName" == @"shippingAddress.firstName"
WHEN @"riskscore" > 700 
WHEN Geo.CountryCode(@"device.ipAddress") == "US"
```

- Check whether a variable is contained in a list.

```ruleslanguage
WHEN ContainsKey("Safe List", "Emails", @"user.email")
```

- Check the value of a key in a list.

```ruleslanguage
WHEN Lookup("Email List", "Emails", @"user.email", "Status") == "Safe"
WHEN Lookup("Product cutoff list", "Product", @"productList.productName", "Score Cutoff").toDouble() < @"riskScore"
```

- Evaluate a string.

```ruleslanguage
WHEN @"phone.phoneNumber".StartsWith("1-")
WHEN @"user.email".EndsWith("@contoso.com")
```

## Language reference

This section contains a complete list of operators that are available in Fraud Protection. These operators are grouped into the following types:

- [Joining operators](fpl-lang-ref.md#joining-operators)
- [List operators](fpl-lang-ref.md#list-operators)
- [Comparison operators](fpl-lang-ref.md#comparison-operators)
- [Geo operators](fpl-lang-ref.md#geo-operators)
- [String operators](fpl-lang-ref.md#string-operators)
- [Math operators](fpl-lang-ref.md#math-operators)
- [DateTime operators](fpl-lang-ref.md#datetime-operators)
- [Type casting operators](fpl-lang-ref.md#)

### Keywords

| Keyword | Description | Example |
|--------|-------------|---------|
| RETURN | <p>This keyword must be followed by a valid [decision type](fpl-lang-ref.md#decision-types): *Approve*, *Reject*, *Challenge*, or *Review*.</p><p>The decision can be followed by the [Other](fpl-lang-ref.md#additional-return-types) type, which is used to pass key/value pairs.</p> | <p>RETURN Reject()</p><p>RETURN Reject(), Other(key=@"user.email")</p> |
| WHEN   | The expression must be able to be evaluated to a *Boolean* value. | WHEN @"riskscore" \> 400 |

#### Decision types

| Decision type    | Description | Example |
|-----------|-------------|---------|
| Approve   | <p>This decision type approves the event.</p><p>Overloads:</p><ul><li>Approve()</li><li>Approve(String *reason*)</li><li>Approve(String *reason*, String *supportMessage*)</li></ul> | <p>Approve()</p><p>Approve("on safe list")</p><p>Approve ("on safe list", "do not escalate")</p> |
| Reject    | <p>This decision type rejects the event.</p><p>Overloads:</p><ul><li>Reject()</li><li>Reject(String *reason*)</li><li>Reject(String *reason*, String *supportMessage*)</li></ul> | <p>Reject()</p><p>Reject("embargo country")</p><p>Return Reject()</p><p>Reject("embargo country", "do not escalate")</p> |
| Review    | <p>This decision type marks the transaction for further review.</p><p>Overloads:</p><ul><li>Review()</li><li>Review(String *reason*)</li><li>Review(String *reason*, String *supportMessage*)</li></ul> | <p>Review()</p><p>Review("user on watch list")</p><p>Review("user on watch list", "do not escalate")</p> |
| Challenge | <p>This decision type marks the transaction for further verification by using the specified challenge type.</p><p>Overloads:</p><ul><li>Challenge(String *challengeType*)</li><li>Challenge(String *challengeType*, String *reason*)</li><li>Challenge(String *challengeType*, String *reason*, String *supportMessage*)</li></ul> | <p>Challenge ("SMS")</p><p>Challenge ("SMS", "suspected bot")</p><p>Challenge ("SMS", suspected bot", "do not escalate")</p> |

#### Additional return types

| Return type | Description | Example |
|--------|-------------|---------|
| Other  | This type can be used to pass key/value pairs. | Other(key="test", email=@"user.email", countryRegion=Geo.CountryRegion(@"device.ipAddress")) |
|Trace   |Can be used to trigger a Trace event, and send key value pairs to the FraudProtection.Trace.Rule [Event Tracing namespace](event-tracing.md#event-schemas). |Trace(key=”Manual Review”, ip=@”device.ipAddress”) |

#### Variables

For information about how to use variables, see the [Type inference of variables](fpl-lang-ref.md#type-inference-of-variables) section later in this topic.

| Variable          | Description | Example |
|-----------------|-------------|---------|
| @               | <p>Used to reference a variable from the event payload.</p><p>After the @, specify the full path of the variable you would like to reference, surrounded by quotes. For example, @”address.city”.</p><p>If the variable referenced is not part of the event payload, the default value for that type is returned – 0.0 for double, empty string for strings, etc.</p><p>The type of the variable is inferred by the context in which it is used. If not enough context is provided, the type defaults to String.</p><p>For information about type inference, see [Type inference of variables](fpl-lang-ref.md#type-inference-of-variables).</p>| <p>@"address.city"</p> |
| @"botScore"       | <p>For every Account Protection event, Fraud Protection's AI models generate a bot score between 0 and 999. A higher score indicates a higher probability that the event was initiated by a bot.</p><p>You can use *@botScore* to reference this score in [post-bot-scoring clauses](rules.md#post-bot-scoring-clauses) and [post-risk-scoring clauses](rules.md#post-risk-scoring-clauses).</p> | @"botScore" |
| @"riskScore"      | <p>For every Purchase and Account Protection event, Fraud Protection's AI models generate a risk score between 0 and 999. A higher score indicates a higher risk.</p><p>You can use *@riskScore* to reference this score in post-risk-scoring clauses.</p> | @"riskScore" |
|@a[x]    |<p>Used to index array variables. </p><p>If the request payload for an assessment contains an array of items, you can access individual elements of the array using the following syntax: @"productList[0]". </p><p>To access an attribute of that element: @"productList[0].productId"</p>    |<p>@"productList[0].productId" </p><p>@"paymentInstrumentList[3].type"</p>


#### Joining operators

| Operator    | Description | Example |
|-----------|-------------|---------|
| AND (&&)  | Logical **And** | <p>@"botScore" \> 500 && @"riskScore" \> 500</p><p>@"botScore" \> 500 AND @"riskScore" \> 500</p> |
| OR (\|\|) | Logical **Or** | <p>@"email.isEmailUsername" == false \|\| @"email.isEmailValidated" == false</p><p>@"email.isEmailUsername" == false OR @"email.isEmailValidated" == false</p> |

#### List operators

For information about how to use lists in rules, see the [Using lists in rules](fpl-lang-ref.md#using-lists-in-rules) section later in this topic.

| Operator        | Description | Example |
|---------------|-------------|---------|
| ContainsKey   | <p>This operator checks whether a key is contained in the specified column in a predefined [list](lists.md).</p><p>ContainsKey(String *listName*, String *columnName*, String *key*)</p> | <p>ContainsKey("Email Support List", "Emails", @"user.email")</p><p>This example checks whether the "Emails" column in the "Email Support List" list contains the *@"user.email"* variable.</p> |
| Lookup        | <p>This operator looks up the value of a key in a list column and returns the value as a *String* value.</p><p>If the key isn't found, and *defaultValue* isn't specified, "Unknown" is returned.</p><p>Overloads:</p><ul><li>Lookup(String *listName*, String *keyColumnName*, String *key*, String *valueColumnName*)</li><li>Lookup(String *listName*, String *keyColumnName*, String key, String valueColumnName, String defaultValue)</li></ul> | <p>Lookup("Email Support List", "Emails", @"user.email", "Status")</p><p>This example looks for the *@"user.email"* variable in the "Emails" column of the "Email Support List" list and returns the corresponding value in the "Status" column.</p> |
| LookupClosest | <p>This operator looks up the value of a key in a list column. If the key isn't found, it returns the value of the key that is alphabetically closest to the key that you're looking for.</p><p>Lookup(String *listName*, String *keyColumnName*, String *key*, String *valueColumnName*)</p> | <p>LookupClosest("IP Addresses", "IP", @"device.ipAddress", "City") == "Seattle"</p><p>This example looks for the *@ipAddress* variable in the "IP" column of the "IP Addresses" list and returns the corresponding value in the "City" column. If *@ipAddress* isn't found in the list, the expression returns the value of the next closest IP address in the list.</p> |
| In            | <p>This operator checks whether a key is contained in a comma-separated list of values.</p><p>In(String *key*, String *list*)</p> | In(@"user.countryRegion", "US, MX, CA") |

#### Comparison operators

Fraud Protection supports all standard C# [comparison](https://docs.microsoft.com/dotnet/csharp/language-reference/operators/comparison-operators) and [equality](https://docs.microsoft.com/dotnet/csharp/language-reference/operators/equality-operators) operations. Applying these operators to Strings will result in lexicographic comparisons. This table includes some examples of operators which may be useful to you.

| Operator | Description | Example |
|--------|-------------|---------|
| ==     | This operator checks for equality. | @"user.countryRegion" == @"shippingAddress.countryRegion" |
| !=     | This operator checks for inequality. | @"user.countryRegion" != @"shippingAddress.countryRegion" |
| \>     | This operator checks whether the first value is greater than the second value. | @"riskScore" \> 500 |
| \<     | This operator checks whether the first value is less than the second value. | @"riskScore" \< 500 |
| \>=    | This operator checks whether the first value is greater than or equal to the second value. | @"riskScore" \>= 500 |
| \<=    | This operator checks whether the first value is less than or equal to the second value. | @"riskScore" \<= 500 |

#### Geo operators

These operators convert an IP address to a geographical address.

| Operator            | Description | Example |
|-------------------|-------------|---------|
| Geo.RegionCode    | <p>This operator converts an IPv4 address to its US region code (that is, the abbreviation for the name of the US state or territory).</p><p>For example, for an IP address in Washington state, "WA" is returned.</p> | Geo.RegionCode(@"device.ipAddress") |
| Geo.Region        | <p>This operator converts an IPv4 address to its US region (that is, the name of the US state or territory).</p><p>For example, for an IP address in Washington state, "Washington" is returned.</p> | Geo.Region(@"device.ipAddress") |
| Geo.CountryCode   | <p>This operator converts an IPv4 address to its country/region code.</p><p>For example, for an IP address in Australia, "AU" is returned.</p> | Geo.CountryCode(@"device.ipAddress") |
| Geo.CountryRegion | <p>This operator converts an IP address to a region name.</p><p>For example, for an IP address in Australia, "Australia" is returned.</p> | Geo.CountryRegion(@"device.ipAddress") |
| Geo.City          | <p>This operator converts an IPv4 address to a city name.</p><p>For example, for an IP address in New York City, "New York City" is returned.</p> | WGeo.City(@"device.ipAddress") |
| Geo.MarketCode    | <p>This operator converts an IPv4 address to the market code of the IP address.</p><p>For example, for an IP address from Canada, "NA" (North America) is returned.</p> | Geo.MarketCode(@"device.ipAddress") |

#### String operators

Fraud Protection supports all standard .NET [string operators](https://docs.microsoft.com/dotnet/api/system.string?view=netframework-4.8). This table includes some examples of methods that you might find useful.

| Operator     | Description | Example |
|------------|-------------|---------|
| StartsWith | <p>This operator checks whether a string begins with a specified prefix.</p><p>StartsWith(String *prefix*)</p> | @"user.phoneNumber".StartsWith("1-") |
| EndsWith   | <p>This operator checks whether a string ends with a specified suffix.</p><p>EndsWith(String *suffix*)</p> | @"user.email".EndsWith("@contoso.com") |
| Contains   | <p>This operator checks whether a string contains another string.</p><p>Contains(String *substring*)</p> | @"productList.productName".Contains("Xbox") |
| Exists     | <p>This operator checks whether a variable exists in the event payload.</p><p>Exists(String *variable*)</p> | Exists(@"user.email") |

#### Math operators

Fraud Protection supports all standard .NET [math methods](https://docs.microsoft.com/dotnet/api/system.math?view=netframework-4.8) and all C# [arithmetic operators](https://docs.microsoft.com/dotnet/csharp/language-reference/operators/arithmetic-operators). This table includes some examples of methods that you might find useful.

| Operator   | Description | Example |
|----------|-------------|---------|
| Math.Min | <p>This operator computes the minimum of two values.</p><p>Math.Min(Double value1, Double value2)</p> | Math.Min(@"riskScore",@"botScore") |
| Math.Max | <p>This operator computes the maximum of two values.</p><p>Math.Max(Double value1, Double value2)</p> | Math.Max(@"riskScore",@"botScore") |

### DateTime operators

Fraud Protection supports all standard .NET [DateTime](https://docs.microsoft.com/dotnet/api/system.datetime?view=netframework-4.8) properties, methods, and operators. This table includes some examples of properties that you might find useful.

| Operator | Description | Example |
|--------|-------------|---------|
|DaysSince	|<p>Returns an int representing the number of days that have passed between today (in UTC time) and the given DateTime value. </p><p>DaysSince(DateTime date)</p>	|DaysSince(@"user.CreationDate")|
| UtcNow | This operator gets a DateTime object that is set to the current date and time on the computer, expressed as Coordinated Universal Time (UTC). | DateTime.UtcNow |
| Today  | This operator gets an object that is set to the current date, where the time component is set to 00:00:00. | DateTime.Today |
| Year   | This operator gets the year component of the date that is represented by this instance. | @"user.creationDate".Year |
| Date   | This operator gets a new object that has the same date as this instance, and the time value. | @"user.creationDate".Date |

### Type casting operators

For information about type inferencing, see the [Type inference of variables](fpl-lang-ref.md#type-inference-of-variables) section.

| Operator       | Description | Example |
|--------------|-------------|---------|
| ToDateTime() | This operator converts a string to a *DateTime* object. | @"user.creationDate".ToDateTime() |
| ToDouble()   | This operator converts a string to a *Double* value. | @"productList.purchasePrice".ToDouble() |
| ToInt32()    | This operator converts a string to an *Int32* value. | @"riskScore".ToInt32() |

## Using lists in rules

You can use the **ContainsKey** and **Lookup** operators to create a rule with a previously created [list](lists.md).

### ContainsKey

To check whether a one of your lists contains a specific value, use the **ContainsKey** operator. Specify the list name, the column, and the key that you want to check.

For example, you create a single-column list of risky email addresses and name it *Risky email list*.

| Email                      |
|----------------------------|
| `Kayla@contoso.com`        |
| `Jamie@bellowscollege.com` |
| `Marie@atatum.com`         |

You can then use the following syntax to reject all transactions from the risky email addresses in this list.

```ruleslanguage
RETURN Reject("risky email") 
WHEN ContainsKey("Risky email list", "Email", @"user.email") 
```

This clause checks whether the "Email" column in the "Risky email list" list contains the *@email* key. If it does, the transaction is rejected.

### Lookup

You can use the **Lookup** operator to look up the value of a key in a list.

For example, you create a list that has one column for email addresses and another column that indicates the status of those email addresses. You name this list *Email List*.

| Email                      | Status |
|----------------------------|--------|
| `Kayla@contoso.com`        | Risky  |
| `Jamie@bellowscollege.com` | Risky  |
| `Marie@atatum.com`         | Risky  |
| `Camille@fabrikam.com`     | Safe   |
| `Miguel@proseware.com`     | Safe   |
| `Tyler@contoso.com`        | Safe   |

You can then use the following syntax to reject all transactions from the email addresses in this list that have a status of *Risky*.

```ruleslanguage
RETURN Reject("risky email") 
WHEN Lookup("Email List", "Email", @"user.email", "Status") == "Risky"
```

This clause looks for the *@"user.email"* key in the "Email" column in the "Email List" list and checks whether the value in the "Status" column is *Risky*. If it is, the transaction is rejected.

If the *@"user.email"* key isn't found in the list, Fraud Protection returns "Unknown."

You can also specify your own default value as the fifth parameter. For more information, see the [List operators](fpl-lang-ref.md#list-operators) section earlier in this topic.

The **Lookup** operator always returns a *String* value. To convert this value to an *Int*, *Double*, or *DateTime* value, use a [type casting operator](fpl-lang-ref.md#type-casting-operators).

## Type inference of variables

Variable types are inferred from the context that they are used in. Here are some examples:

- In the expression **WHEN \@isEmailValidated**, the variable is interpreted as a *Boolean* value.
- In the expression **@"riskScore" \> 500**, the variable is interpreted as a *Double* value.
- In the expression **@"user.creationDate".Year \< DateTime.UtcNow.Year**, the variable is interpreted as a *DateTime* value.

If there isn't enough context to infer the type of a variable, it's considered a *String* value. For example, in the expression **@"riskScore" \< @"botScore"**, both variables are interpreted as strings.

To specify the type of a non-string variable, use a [type casting operator](fpl-lang-ref.md#type-casting-operators).
