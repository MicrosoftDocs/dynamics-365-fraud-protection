---
author: yvonnedeq
description: This topic is a language reference guide  for Microsoft Dynamics 365 Fraud Protection rules.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 03/24/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Language reference guide

---

# Language reference guide

## Overview

Microsoft Dynamics 365 has its own rich and expressive language to help you define and express your fraud strategy. This language has many similarities to C# and SQL, and is designed to give you the flexibility that you need to address fraud for your unique business scenarios.

You can use this language today to define rules and velocities. To learn more, see [Manage rules](rules.md) and [Perform velocity checks](velocities.md).

This language reference guide includes the complete list of operators, functions, and keywords that make up the language:

-	Keywords
-	Decision functions
-	Observation functions
-	Referencing attributes
-	Logical operators
-	Comparison operators
-	Type casting operators
-	Geo functions
-	String functions 
-	Math functions
-	DateTime functions
-	Aggregation functions

The guide also covers additional topics such as: 

- [Defining your own variables](fpl-lang-ref.md#defining-your-own-variables)
-	[Using lists](fpl-lang-ref.md#using-lists-in-rules)
-	[Using external calls and velocities](pl-lang-ref.md#using-external-calls-and-velocities)
-	Type inheritance of properties

## Language reference

### Keywords

| Keyword | Description | Example |
|--------|-------------|---------|
| RETURN | <p>A RETURN statement will terminate rule execution. </p><p>The statement must specify a valid decision function Approve(), Reject(), Challenge(), or Review().</p><p>The statement may also specify one or more observation functions:  Other() or Trace()</p>| <p>RETURN Reject()</p><p>RETURN Reject(), Other(key=@"user.email")</p><p>RETURN Reject(), Other(key=@"user.email"),Trace(ip=@"device.ipAddress")</p> |
| WHEN   | The WHEN statement specifies a *Boolean* condition. This serves to make the rest of the block execute only when the condition evaluates to true. | WHEN @"riskscore" \> 400 |
| SELECT   | Used in a velocity to specify an aggregation function. | SELECT Count() AS velocityName |
| AS       | Used to create an alias for your velocity, which will be referenceable from rules. | SELECT Count() AS velocityName |
| FROM     | Used to select on assessment on which to observe a velocity.  | FROM Purchase  |
| GROUPBY  | <p>A GROUPBY statement specifies a property or an expression. All events events evaluated to the same value in the GROUPBY are combined to calculate the requested aggregation in the SELECT statement. </p><p>For example if you wanted to calculate an aggregation for each user, you would GROUPBY @”user.userId” </p> | GROUPBY @”user.userId”  |
| LET      | <p>Used to define a new variable. The scope of the variable is the rule or velocity set in which it is defined in. Variable names should be prefixed with $.</p><p>For more information, see [Defining your own variables](fpl-lang-ref.md#defining-your-own-variables). </p>  | LET $fullName = @”user.firstName” + @”user.lastName”  |

#### Decision functions

Decision functions are used in rules to specify a decision.  

| Decision type    | Description | Example |
|-----------|-------------|---------|
| Approve()   | <p>Specifies a decision of Approve. Can include a reason for the approval, as well as an additional supporting message.</p><p>Overloads:</p><ul><li>Approve(String *reason*)</li><li>Approve(String *reason*, String *supportMessage*)</li></ul> | <p>RETURN Approve()</p><p>RETURN Approve("on safe list")</p><p>RETURN Approve ("on safe list", "do not escalate")</p> |
| Reject()    | <p>Specifies a decision of Reject. Can include a reason for the rejection, as well as an additional supporting message.</p><p>Overloads:</p><ul><li>Reject(String *reason*)</li><li>Reject(String *reason*, String *supportMessage*)</li></ul> | <p>RETURN Reject()</p><p>RETURN Reject("embargo country")</p><p>RETURN Reject("embargo country", "do not escalate")</p> |
| Review()    | <p>Specifies a decision of Review. Can include a reason for the review, as well as an additional supporting message.</p><p>Overloads:</p><ul><li>Review(String *reason*)</li><li>Review(String *reason*, String *supportMessage*)</li></ul> | <p>RETURN Review()</p><p>RETURN Review("user on watch list")</p><p>RETURN Review("user on watch list", "do not escalate")</p> |
| Challenge(String *challengeType*) | <p>Specifies a decision of Challenge, as well as a challenge type. Can also include a reason for the challenge, as well as an additional supporting message.</p><p>Overloads:</p><ul><li>Challenge(String *challengeType*, String *reason*)</li><li>Challenge(String *challengeType*, String *reason*, String *supportMessage*)</li></ul> | <p>RETURN Challenge ("SMS")</p><p>RETURN Challenge ("SMS", "suspected bot")</p><p>RETURN Challenge ("SMS", suspected bot", "do not escalate")</p> |

#### Observation functions

Observation functions can be used to take data from the current context, and write it elsewhere.  

| Return type | Description | Example |
|--------|-------------|---------|
| Other(k=v)  | Can be used to pass key/value pairs into the API response. | Other(key="test", email=@"user.email", countryRegion=Geo.CountryRegion(@"device.ipAddress")) |
|Trace(k=v)   |Can be used to trigger a Trace event, and send key value pairs to the FraudProtection.Trace.Rule [Event Tracing namespace](event-tracing.md#event-schemas). |Trace(key="Manual Review", ip=@"device.ipAddress") |

#### Referencing attributes and variables

You can use the @ operator to reference an attribute from the current event.

| Variable          | Description | Example |
|-----------------|-------------|---------|
| @               | <p>Used to reference an attribute from the incoming event. The attribute may be sent as part of the request payload or may be generated by Fraud Protection.</p><p>After the @, specify the full path of the variable you would like to reference, surrounded by quotes. For example, @"address.city".</p><p>If the variable referenced is not part of the event payload, the default value for that type is returned – 0.0 for double, empty string for strings, etc.</p><p>The type of the variable is inferred by the context in which it is used. If not enough context is provided, the type defaults to String.</p><p>For information about type inference, see [Type inference of variables](fpl-lang-ref.md#type-inference-of-variables).</p>| <p>@"address.city"</p> |
| $                 | Used to reference a variable which has been defined in a LET statement. For more information, see [Defining your own variables](fpl-lang-ref.md#defining-your-own-variables). | $fullName  |
| @"botScore"       | <p>For every Account Creation or Account Login event, Fraud Protection's AI models generate a bot score between 0 and 999. A higher score indicates a higher probability that the event was initiated by a bot.</p><p>You can use *@botScore* to reference this score in [post-bot-scoring clauses](rules.md#post-bot-scoring-clauses) and [post-risk-scoring clauses](rules.md#post-risk-scoring-clauses).</p> | @"botScore" |
| @"riskScore"      | <p>For every Purchase and Account Protection event, Fraud Protection's AI models generate a risk score between 0 and 999. A higher score indicates a higher risk.</p><p>You can use *@riskScore* to reference this score in post-risk-scoring clauses.</p> | @"riskScore" |
|@a[x]    |<p>Used to index array variables. </p><p>If the request payload for an assessment contains an array of items, you can access individual elements of the array using the following syntax: @"productList[0]". </p><p>To access an attribute of that element: @"productList[0].productId"</p>    |<p>@"productList[0].productId" </p><p>@"paymentInstrumentList[3].type"</p>
| Exists            | <p>This operator checks whether a variable exists in the event payload.</p><p>Exists(*String variable*)</p>    | Exists(@"user.email")  |

#### Logical operators

| Operator    | Description | Example |
|-----------|-------------|---------|
| and (&&)  | Logical **And** | <p> @"riskScore" > 500 && @"riskScore" < 800 </p><p> @"riskScore" > 500 and @"riskScore" < 800 </p> |
| or (\|\|) | Logical **Or** | <p>@"email.isEmailUsername" == false \|\| @"email.isEmailValidated" == false</p><p>@"email.isEmailUsername" == false or @"email.isEmailValidated" == false</p> |
| not       | Logical negation  | <p> !@”email.isEmailUsername” </p><p> not @”email.isEmailUsername” </p>  |

#### List functions

Fraud Protection allows you to upload custom lists and reference them in the language. 

For information about how to upload these lists, see [Manage lists](lists.md). For additional information on how  how to use lists in rules, see the [Using lists in rules](fpl-lang-ref.md#using-lists-in-rules) section later in this topic.

| Operator        | Description | Example |
|---------------|-------------|---------|
| <p>ContainsKey(<p>  String *listName*, </p><p>  String *columnName*, </p><p>  String *key*) </p>   | Checks whether a key is contained in the specified column in a Fraud Protection [list](lists.md). | <p>ContainsKey("Email Support List", "Emails", @"user.email")</p><p>This example checks whether the "Emails" column in the "Email Support List" list contains the *@"user.email"* variable.</p> |
| <p>Lookup(<p>  String *listName*, </p><p>  String *keyColName*, </p><p>  String *valueColName *) </p>    |<p>Looks up the value of a key in a Fraud Protection list. The column name containing the key as well as the column name containing the value must be specified. </p><p>The value will always be returned as a *String*.  </p><p>If the key isn't found, and defaultValue parameter isn't specified, "Unknown" is returned. </p><p>Overloads:</p><ul><li>Lookup(String *listName*, String *keyColumnName*, String key, String valueColumnName, String defaultValue)</li></ul> | <p>Lookup("Email Support List", "Emails", @"user.email", "Status",0)</p><p>This example looks for the *@"user.email"* variable in the "Emails" column of the "Email Support List" list and returns the corresponding value in the "Status" column.</p><p>If the key is not found in the list, Fraud Protection will return 0.</p> |
| <p>LookupClosest(</p><p>String*listName*, String *keyColumnName*, </p><p>String *key*, String *valueColumnName*) | Looks up the value of a key in a Fraud Protection list. If the key isn't found, it returns the value of the key that is alphabetically closest to the key that you're looking for. | <p>LookupClosest("IP Addresses", "IP", @"device.ipAddress", "City") == "Seattle"</p><p>This example looks for the *@ipAddress* variable in the "IP" column of the "IP Addresses" list and returns the corresponding value in the "City" column. If *@ipAddress* isn't found in the list, the expression returns the value of the next closest IP address in the list.</p> |
| In            | <p>This operator checks whether a key is contained in a comma-separated list of values.</p><p>In(String *key*, String *list*)</p> | In(@"user.countryRegion", "US, MX, CA") |

#### Comparison operators

Fraud Protection supports all standard C# [comparison](https://docs.microsoft.com/dotnet/csharp/language-reference/operators/comparison-operators) and [equality](https://docs.microsoft.com/dotnet/csharp/language-reference/operators/equality-operators) operations. This table includes some examples of operators which may be useful to you. Applying these operators to Strings will result in lexicographic comparisons..

| Operator | Description | Example |
|--------|-------------|---------|
| ==     | This operator checks for equality. | @"user.countryRegion" == @"shippingAddress.countryRegion" |
| !=     | This operator checks for inequality. | @"user.countryRegion" != @"shippingAddress.countryRegion" |
| \>     | This operator checks whether the first value is greater than the second value. | @"riskScore" \> 500 |
| \<     | This operator checks whether the first value is less than the second value. | @"riskScore" \< 500 |
| \>=    | This operator checks whether the first value is greater than or equal to the second value. | @"riskScore" \>= 500 |
| \<=    | This operator checks whether the first value is less than or equal to the second value. | @"riskScore" \<= 500 |

#### Geo functions

These functions convert an IP address to a geographical address.

| Operator            | Description | Example |
|-------------------|-------------|---------|
| Geo.RegionCode(String *ip*)    | <p>This operator converts an IPv4 address to its US region code (that is, the abbreviation for the name of the US state or territory).</p><p>For example, for an IP address in Washington state, "WA" is returned.</p> | Geo.RegionCode(@"device.ipAddress") |
| Geo.Region(String *ip*)        | <p>This operator converts an IPv4 address to its US region (that is, the name of the US state or territory).</p><p>For example, for an IP address in Washington state, "Washington" is returned.</p> | Geo.Region(@"device.ipAddress") |
| Geo.CountryCode(String *ip*)   | <p>This operator converts an IPv4 address to its country/region code.</p><p>For example, for an IP address in Australia, "AU" is returned.</p> | Geo.CountryCode(@"device.ipAddress") |
| Geo.CountryRegion(String *ip*) | <p>This operator converts an IP address to a region name.</p><p>For example, for an IP address in Australia, "Australia" is returned.</p> | Geo.CountryRegion(@"device.ipAddress") |
| Geo.City(String *ip*)          | <p>This operator converts an IPv4 address to a city name.</p><p>For example, for an IP address in New York City, "New York City" is returned.</p> | WGeo.City(@"device.ipAddress") |
| Geo.MarketCode(String *ip*)    | <p>This operator converts an IPv4 address to the market code of the IP address.</p><p>For example, for an IP address from Canada, "NA" (North America) is returned.</p> | Geo.MarketCode(@"device.ipAddress") |

#### String functions

Fraud Protection supports the standard C# [string class](https://docs.microsoft.com/dotnet/api/system.string?view=netframework-4.8&preserve-view=true). This table includes some examples of methods that you might find useful.

| Operator     | Description | Example |
|------------|-------------|---------|
| StartsWith(String *prefix*) | <p>This operator checks whether a string begins with a specified prefix.</p><p>StartsWith(String *prefix*)</p> | @"user.phoneNumber".StartsWith("1-") |
| EndsWith(String *suffix*)   | <p>This operator checks whether a string ends with a specified suffix.</p><p>EndsWith(String *suffix*)</p> | @"user.email".EndsWith("@contoso.com") |
| Contains(String *suffix*)   | <p>This operator checks whether a string contains another string.</p><p>Contains(String *substring*)</p> | @"productList.productName".Contains("Xbox") |

#### Math functions

Fraud Protection supports all standard C# [math methods](https://docs.microsoft.com/dotnet/api/system.math?view=netframework-4.8&preserve-view=true) and [arithmetic operators](https://docs.microsoft.com/dotnet/csharp/language-reference/operators/arithmetic-operators). This table includes some examples of methods that you might find useful.

| Operator   | Description | Example |
|----------|-------------|---------|
| Math.Min(Double *value1*, Double *value*2) | his operator computes the minimum of two values. | Math.Min(@"riskScore",@"botScore") |
| Math.Max(Double *value1*, Double *value*2) | This operator computes the maximum of two values. | Math.Max(@"riskScore",@"botScore") |

### DateTime operators

Fraud Protection supports the standard C# [DateTime](https://docs.microsoft.com/dotnet/api/system.datetime?view=netframework-4.8&preserve-view=true) properties, methods, and operators. This table includes some examples of functions and properties that you might find useful.

| Operator | Description | Example |
|--------|-------------|---------|
|DaysSince(DateTime *date*)	|Returns an int representing the number of days that have passed between today (in UTC time) and the given DateTime value. 	|DaysSince(@"user.CreationDate")|
| UtcNow | This operator gets a DateTime object that is set to the current date and time on the computer, expressed as Coordinated Universal Time (UTC). | DateTime.UtcNow |
| Today  | This operator gets an object that is set to the current date, where the time component is set to 00:00:00. | DateTime.Today |
| Year   | This operator gets the year component of the date that is represented by this instance. | @"user.creationDate".Year |
| Date   | This operator gets a new object that has the same date as this instance, and the time value set to midnight. | @"user.creationDate".Date |

### Type casting operators

For information about type inferencing, see the [Type inference of variables](fpl-lang-ref.md#type-inference-of-variables) section.

| Operator       | Description | Example |
|--------------|-------------|---------|
| ToDateTime() | This operator converts a string to a *DateTime* object. | @"user.creationDate".ToDateTime() |
| ToDouble()   | This operator converts a string to a *Double* value. | @"productList.purchasePrice".ToDouble() |
| ToInt32()    | This operator converts a string to an *Int32* value. | @"riskScore".ToInt32() |

### Aggregation functions

| Function     | Description | Example |
|--------------|-------------|---------|
| Count()                         | Returns the number of times an event has occured.    | SELECT Count() AS numPurchases |
| DistinctCount(String *key*)()   | Returns the number of distinct values for the specified property. If the specified property is null or empty for an incoming event, the event will not contribute to the aggregation. | SELECT DistinctCount(@”device.ipAddress”) AS distinctIPs |
| Sum(Double *value*)             | Returns the sum of values for a specified numeric property.  | SELECT Sum(@”totalAmount”) AS totalSpending |

## Defining your own variables

You can use the LET keyword to define a variable, which can then be referenced elsewhere in the rule. All variables should be prefixed by $.

For example, you could declare the following variable:

LET $fullName = @”user.firstName” + @”user.lastName”

Variables declared in a LET statement can be used only within the scope of the rule or velocity set it is defined in. 

To reference the variable above, you could write the following:

WHEN $fullName == “Kayla Goderich”

> [!NOTE]
> Once a variable has been defined, it cannot be updated with a new value.

## Using lists in rules

You can use the **ContainsKey** and **Lookup** operators to reference lists which you have uploaded to Fraud Protection. For more information about lists, see [Manage lists](lists.md).

### ContainsKey

To check whether a one of your lists contains a specific value, use the **ContainsKey** operator. Specify the list name, the column, and the key that you want to check for.

For example, you upload a single-column list of risky email addresses and name it *Risky email list*.

| Email                      |
|----------------------------|
| `Kayla@contoso.com`        |
| `Jamie@bellowscollege.com` |
| `Marie@atatum.com`         |

You can then use the following syntax to reject all transactions from the risky email addresses in this list.

```FraudProtectionLanguage
RETURN Reject("risky email") 
WHEN ContainsKey("Risky email list", "Email", @"user.email") 
```

This clause checks whether the "Email" column in the "Risky email list" list contains the *@email* key. If it does, the transaction is rejected.

### Lookup

For multi-column lists, You can use the **Lookup** operator to check the value of column for a specific key.

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

```FraudProtectionLanguage
RETURN Reject("risky email") 
WHEN Lookup("Email List", "Email", @"user.email", "Status") == "Risky"
```

This clause looks for the *@"user.email"* key in the "Email" column in the "Email List" list and checks whether the value in the "Status" column is *Risky*. If it is, the transaction is rejected.

If the *@"user.email"* key isn't found in the list, Fraud Protection returns "Unknown."

You can also specify your own default value as the fifth parameter. For more information, see the [List operators](fpl-lang-ref.md#list-operators) section earlier in this topic.

The **Lookup** operator always returns a *String* value. To convert this value to an *Int*, *Double*, or *DateTime* value, use a [type casting operator](fpl-lang-ref.md#type-casting-operators).

## Using external calls and velocities

You can reference external calls and velocities by using the corresponding keyword. 

To reference an external call in the language, type “External.” followed by the external call you’d like to reference. For more information, see [Use an external call with rules](external-calls.md#use-an-external-call-with-rules).

To reference a velocity in the language, type “Velocity.” followed by the individual velocity you’d like to reference. For more information, see [Use a velocity in rules](velocities.md#use-a-velocity-in-rules).



## Type inference of variables

Variable types are inferred from the context that they are used in. Here are some examples:

- In the expression **WHEN \@isEmailValidated**, the variable is interpreted as a *Boolean* value.
- In the expression **@"riskScore" \> 500**, the variable is interpreted as a *Double* value.
- In the expression **@"user.creationDate".Year \< DateTime.UtcNow.Year**, the variable is interpreted as a *DateTime* value.

If there isn't enough context to infer the type of a variable, it's considered a *String* value. For example, in the expression **@"riskScore" \< @"botScore"**, both variables are interpreted as strings.

To specify the type of a non-string variable, use a [type casting operator](fpl-lang-ref.md#type-casting-operators).


[!INCLUDE[footer-include](includes/footer-banner.md)]
