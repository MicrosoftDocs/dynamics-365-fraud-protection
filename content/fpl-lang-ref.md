---
author: josaw1
description: This article is a language reference guide for Microsoft Dynamics 365 Fraud Protection rules.
ms.author: josaw
ms.date: 09/26/2022
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Language reference guide

---

# Language reference guide

Microsoft Dynamics 365 has its own rich and expressive language to help you define and express your fraud strategy. This language has many similarities to C# and SQL, and is designed to give you the flexibility that you need to address fraud for your unique business scenarios.

You can use this language today to define rules and velocities. For more information, see [Manage rules](rules.md) and [Perform velocity checks](velocities.md).

This language reference guide includes the complete list of operators, functions, and keywords that make up the language:

- [Keywords](fpl-lang-ref.md#keywords)
- [Decision functions](fpl-lang-ref.md#decision-functions)
- [Observation functions](fpl-lang-ref.md#observation-functions)
- [Model functions](fpl-lang-ref.md#model-functions)
- [Referencing attributes and variables](fpl-lang-ref.md#referencing-attributes-and-variables)
- [Logical operators](fpl-lang-ref.md#logical-operators)
- [List functions](fpl-lang-ref.md#list-functions)
- [Comparison operators](fpl-lang-ref.md#comparison-operators)
- [Geo functions](fpl-lang-ref.md#geo-functions)
- [String functions](fpl-lang-ref.md#string-functions)
- [Math functions](fpl-lang-ref.md#math-functions)
- [Type casting operators](fpl-lang-ref.md#type-casting-operators)
- [DateTime functions](fpl-lang-ref.md#datetime-operators)
- [Aggregation functions](fpl-lang-ref.md#aggregation-functions)

The guide also covers additional articles. Here are some examples:

- [Defining your own variables](fpl-lang-ref.md#defining-your-own-variables)
- [Using lists in rules](fpl-lang-ref.md#using-lists-in-rules)

    - [ContainsKey](fpl-lang-ref.md#containskey)
    - [Lookup](fpl-lang-ref.md#lookup)

- [Using external calls and velocities](fpl-lang-ref.md#using-external-calls-and-velocities)
- [Type inference of attributes](fpl-lang-ref.md#type-inference-of-attributes)

## Keywords

| Keyword | Description | Example |
|---------|-------------|---------|
| RETURN  | <p>A **RETURN** statement terminates rule execution.</p><p>The statement must specify a valid [decision function](fpl-lang-ref.md#decision-functions): **Approve()**, **Reject()**, **Challenge()**, or **Review()**.</p><p>The statement can also specify one or more observation functions: **Output()** or **Trace()**</p> | <p>RETURN Reject()</p><p>RETURN Reject(), Output(key=@"user.email")</p><p>RETURN Reject(), Trace(ip=@"device.ipAddress")</p>|
| OBSERVE | An **OBSERVE** statement does not terminate rule execution.</p><p>When an **OBSERVE** clause is hit, it will be logged in the API response, however, clauses will continue to evaluate until a **RETURN** statement is reached.</p><p>An **OBSERVE** statement must be followed by an [observation function](fpl-lang-ref.md#observation-functions).</p> | OBSERVE Output()</p><p>OBSERVE Output(reason=”high score”)</p> |
| WHEN    | A **WHEN** statement specifies a Boolean condition. The rest of the block is then run only if the condition is evaluated to *true*. | WHEN @"riskscore" \> 400 |
| SELECT  | A **SELECT** statement is used in a velocity to specify an aggregation function. | SELECT Count() AS velocityName |
| AS      | An **AS** statement is used to create an alias for your velocity. This alias can then be referenced from rules. | SELECT Count() AS velocityName |
| FROM    | A **FROM** statement is used to specify an assessment to observe a velocity on. | FROM Purchase |
| GROUPBY | <p>A **GROUPBY** statement specifies a property or an expression. All events that are evaluated to the same value in the **GROUPBY** statement are combined to calculate the aggregation that is requested in the **SELECT** statement.</p><p>For example, to calculate an aggregation for each user, use **GROUPBY @"user.userId"**.</p> | GROUPBY @"user.userId" |
| LET     | <p>A **LET** statement is used to define a new variable. The scope of the variable is the rule or velocity set that it's defined in. Variable names should be prefixed with a dollar sign ($).</p><p>For more information, see [Defining your own variables](fpl-lang-ref.md#defining-your-own-variables).</p> | LET $fullName = @"user.firstName" + @"user.lastName" |

## Decision functions

Decision functions are used in rules to specify a decision.

| Decision type                     | Description | Example |
|-----------------------------------|-------------|---------|
| Approve()                         | <p>This type specifies a decision of *Approve*. It can include a reason for the approval and an additional supporting message.</p><p>Overloads:</p><ul><li>Approve(String *reason*)</li><li>Approve(String *reason*, String *supportMessage*)</li></ul> | <p>RETURN Approve()</p><p>RETURN Approve("on safe list")</p><p>RETURN Approve ("on safe list", "do not escalate")</p> |
| Reject()                          | <p>This type specifies a decision of *Reject*. It can include a reason for the rejection and an additional supporting message.</p><p>Overloads:</p><ul><li>Reject(String *reason*)</li><li>Reject(String *reason*, String *supportMessage*)</li></ul> | <p>RETURN Reject()</p><p>RETURN Reject("embargo country")</p><p>RETURN Reject("embargo country", "do not escalate")</p> |
| Review()                          | <p>This type specifies a decision of *Review*. It can include a reason for the review and an additional supporting message.</p><p>Overloads:</p><ul><li>Review(String *reason*)</li><li>Review(String *reason*, String *supportMessage*)</li></ul> | <p>RETURN Review()</p><p>RETURN Review("user on watch list")</p><p>RETURN Review("user on watch list", "do not escalate")</p> |
| Challenge(String *challengeType*) | <p>This type specifies a decision of *Challenge* and a challenge type. It can also include a reason for the challenge and an additional supporting message.</p><p>Overloads:</p><ul><li>Challenge(String *challengeType*, String *reason*)</li><li>Challenge(String *challengeType*, String *reason*, String *supportMessage*)</li></ul> | <p>RETURN Challenge ("SMS")</p><p>RETURN Challenge ("SMS", "suspected bot")</p><p>RETURN Challenge ("SMS", suspected bot", "do not escalate")</p> |

## Observation functions

Observation functions can be used to take data from the current context and write it somewhere else.

| Return type | Description | Example |
|-------------|-------------|---------|
| Output(k=v)  | This function can be used to pass key-value pairs into the API response. | Output(key="test", email=@"user.email", countryRegion=Geo.CountryRegion(@"device.ipAddress")) |
|Trace(k=v)   | This function can be used to trigger a Trace event and send key-value pairs to the FraudProtection.Trace.Rule [Event Tracing namespace](event-tracing.md#event-schemas). | Trace(key="Manual Review", ip=@"device.ipAddress") |

## Model functions

Model functions run the various fraud models and are useful when your assessment does not automatically run one or more fraud models. When model functions run, the following occurs. First, information about the model running during rule evaluation is output in the fraud assessment API call. Second, the rule will get access to the model result, including score, reasons, and more, that can be used for further rule processing and decision making.

| Model type     | Description | Example |
|--------------|-------------|---------|
|  Risk  |  Assesses the likelihood of a session being risky. | Model.Risk()  |
| Bot   |   Assesses the likelihood of a session being bot-initiated. Pass in a device context ID that has been sent to Fraud Protection’s device fingerprinting solution. | Model.Bot(@deviceContextId)   |



## Referencing attributes and variables
You can use the at sign (@) operator to reference an attribute from the current event.

| Variable     | Description | Example |
|--------------|-------------|---------|
| @            | <p>An at sign (@) is used to reference an attribute from the incoming event. The attribute might be sent as part of the request payload, or it might be generated by Microsoft Dynamics 365 Fraud Protection.</p><p>After the at sign (@), specify the full path of the attribute that you want to reference. Enclose the path in quotation marks (for example, *@"address.city"*).</p><p>If the referenced attribute isn't part of the event payload, the default value for that type is returned: 0.0 for doubles, an empty string for strings, and so on.</p><p>The type of the attribute is inferred from the context that it's used in. If not enough context is provided, the *String* type is used by default.</p><p>For information about type inference, see [Type inference of attributes](fpl-lang-ref.md#type-inference-of-attributes).</p> | <p>@"address.city"</p> |
| $            | A dollar sign ($) is used to reference a variable that has been defined in a **LET** statement. For more information, see [Defining your own variables](fpl-lang-ref.md#defining-your-own-variables). | $fullName |
| @"botScore"  | <p>For every Account Creation or Account Login event, Fraud Protection's AI models generate a bot score between 0 and 999. A higher score indicates a higher probability that the event was initiated by a bot.</p><p>You can use *@botScore* to reference this score in [post-bot-scoring clauses](rules.md#post-bot-scoring-clauses) and [post-risk-scoring clauses](rules.md#post-risk-scoring-clauses).</p> | @"botScore" |
| @"riskScore" | <p>For every Purchase or Account Protection event, Fraud Protection's AI models generate a risk score between 0 and 999. A higher score indicates a higher risk.</p><p>You can use *@riskScore* to reference this score in post-risk-scoring clauses.</p> | @"riskScore" |
| @a\[x\]      | <p>This variable is used to index array variables.</p><p>If the request payload for an assessment contains an array of items, you can access individual elements of the array by using the following syntax: *@"productList\[0\]"*.</p><p>To access an attribute of that element, use the following syntax: *@"productList\[0\].productId"*</p> | <p>@"productList\[0\].productId"</p><p>@"paymentInstrumentList\[3\].type"</p> |
| Exists       | <p>This operator checks whether a variable exists in the event payload.</p><p>Exists(*String variable*)</p> | Exists(@"user.email") |

## Logical operators

| Operator  | Description | Example |
|-----------|-------------|---------|
| and (&&)  | Logical **And** | <p>@"riskScore" > 500 && @"riskScore" \< 800</p><p>@"riskScore" \> 500 and @"riskScore" \< 800</p> |
| or (\|\|) | Logical **Or** | <p>@"email.isEmailUsername" == false \|\| @"email.isEmailValidated" == false</p><p>@"email.isEmailUsername" == false or @"email.isEmailValidated" == false</p> |
| not       | Logical negation | @"email.isEmailUsername" not(!) @"email.isEmailUsername" |

## List functions

Fraud Protection lets you upload custom lists and reference them in the language. 

For information about how to upload these lists, see [Manage lists](lists.md). For more information about how to use lists in rules, see the [Using lists in rules](fpl-lang-ref.md#using-lists-in-rules) section later in this article.

| Operator | Description | Example |
|----------|-------------|---------|
| ContainsKey(<br>String *listName*,<br>String *columnName*,<br>String *key*) | This operator checks whether a key is contained in the specified column in a Fraud Protection [list](lists.md). | <p>ContainsKey("Email Support List", "Emails", @"user.email")</p><p>This example checks whether the "Emails" column in the "Email Support List" list contains the *@"user.email"* variable.</p> |
| Lookup(<br>String *listName*,<br>String *keyColName*,<br>String *valueColName*) | <p>This operator looks up the value of a key in a Fraud Protection list. Both the name of the column that contains the key and the name of the column that contains the value must be specified.</p><p>The value will always be returned as a string.</p><p>If the key isn't found, and if the **defaultValue** parameter isn't specified, "Unknown" is returned.</p> | <p>Lookup("Email Support List", "Emails", @"user.email", "Status",0)</p><p>This example looks for the *@"user.email"* variable in the "Emails" column of the "Email Support List" list and returns the corresponding value in the "Status" column.</p><p>If the key isn't found in the list, Fraud Protection returns 0.</p> |
| LookupClosest(<br>String *listName*, String *keyColumnName*, String *key*,<br> String *valueColumnName*, String *defaultValue*)<br> | <p>This operator looks up the value of a key in a Fraud Protection list. If the key isn't found, the value of the key that is alphabetically closest to the key that you're looking for is returned.</p><p>Overloads:</p><ul><li>Lookup(String *listName*, String *keyColumnName*, String key, String valueColumnName, String defaultValue)</li></ul> | <p>LookupClosest("IP Addresses", "IP", @"device.ipAddress", "City") == "Seattle"</p><p>This example looks for the *@ipAddress* variable in the "IP" column of the "IP Addresses" list and returns the corresponding value in the "City" column. If *@ipAddress* isn't found in the list, the expression returns the value of the next closest IP address in the list.</p> |
| In | <p>This operator checks whether a key is contained in a comma-separated list of values.</p><p>In(String *key*, String *list*)</p> | In(@"user.countryRegion", "US, MX, CA") |

## Comparison operators

Fraud Protection supports all standard C# [comparison](/dotnet/csharp/language-reference/operators/comparison-operators) and [equality](/dotnet/csharp/language-reference/operators/equality-operators) operations. This table includes some examples of operators that you might find useful. If you apply these operators to strings, lexicographic comparisons will occur.

| Operator | Description | Example |
|----------|-------------|---------|
| ==       | This operator checks for equality. | @"user.countryRegion" == @"shippingAddress.countryRegion" |
| !=       | This operator checks for inequality. | @"user.countryRegion" != @"shippingAddress.countryRegion" |
| \>       | This operator checks whether the first value is greater than the second value. | @"riskScore" \> 500 |
| \<       | This operator checks whether the first value is less than the second value. | @"riskScore" \< 500 |
| \>=      | This operator checks whether the first value is greater than or equal to the second value. | @"riskScore" \>= 500 |
| \<=      | This operator checks whether the first value is less than or equal to the second value. | @"riskScore" \<= 500 |

## Geo functions

These functions convert an IP address to a geographical address.

| Operator                       | Description | Example |
|--------------------------------|-------------|---------|
| Geo.RegionCode(String *ip*)    | <p>This operator converts an IPv4 address to its US region code (that is, the abbreviation for the name of the US state or territory).</p><p>For example, for an IP address in Washington state, "WA" is returned.</p> | Geo.RegionCode(@"device.ipAddress") |
| Geo.Region(String *ip*)        | <p>This operator converts an IPv4 address to its US region (that is, the name of the US state or territory).</p><p>For example, for an IP address in Washington state, "Washington" is returned.</p> | Geo.Region(@"device.ipAddress") |
| Geo.CountryCode(String *ip*)   | <p>This operator converts an IPv4 address to its country/region code.</p><p>For example, for an IP address in Australia, "AU" is returned.</p> | Geo.CountryCode(@"device.ipAddress") |
| Geo.CountryRegion(String *ip*) | <p>This operator converts an IP address to a region name.</p><p>For example, for an IP address in Australia, "Australia" is returned.</p> | Geo.CountryRegion(@"device.ipAddress") |
| Geo.City(String *ip*)          | <p>This operator converts an IPv4 address to a city name.</p><p>For example, for an IP address in New York City, "New York City" is returned.</p> | WGeo.City(@"device.ipAddress") |
| Geo.MarketCode(String *ip*)    | <p>This operator converts an IPv4 address to the market code of the IP address.</p><p>For example, for an IP address from Canada, "NA" (North America) is returned.</p> | Geo.MarketCode(@"device.ipAddress") |

## String functions

Fraud Protection supports the standard C# [string class](/dotnet/api/system.string?view=netframework-4.8&preserve-view=true). This table includes some examples of functions and operators that you might find useful.

| Operator                    | Description | Example |
|-----------------------------|-------------|---------|
| StartsWith(String *prefix*) | <p>This operator checks whether a string begins with a specified prefix.</p><p>StartsWith(String *prefix*)</p> | @"user.phoneNumber".StartsWith("1-") |
| EndsWith(String *suffix*)   | <p>This operator checks whether a string ends with a specified suffix.</p><p>EndsWith(String *suffix*)</p> | @"user.email".EndsWith("@contoso.com") |
| Contains(String *suffix*)   | <p>This operator checks whether a string contains another string.</p><p>Contains(String *substring*)</p> | @"productList.productName".Contains("Xbox") |

## Math functions

Fraud Protection supports all standard C# [math methods](/dotnet/api/system.math?view=netframework-4.8&preserve-view=true) and [arithmetic operators](/dotnet/csharp/language-reference/operators/arithmetic-operators). This table includes some examples of methods that you might find useful.


| Operator                                   | Description | Example |
|--------------------------------------------|-------------|---------|
| Math.Min(Double *value1*, Double *value*2) | This operator computes the minimum of two values. | Math.Min(@"riskScore",@"botScore") |
| Math.Max(Double *value1*, Double *value*2) | This operator computes the maximum of two values. | Math.Max(@"riskScore",@"botScore") |


## DateTime operators

Fraud Protection supports the standard C# [DateTime](/dotnet/api/system.datetime?view=netframework-4.8&preserve-view=true) properties, methods, and operators. This table includes some examples of functions and properties that you might find useful.

| Operator                   | Description | Example |
|----------------------------|-------------|---------|
| DaysSince(DateTime *date*) | This operator returns an integer that represents the number of days that have passed between the specified *DateTime* value and the current date (expressed as Coordinated Universal Time \[UTC\]). | DaysSince(@"user.CreationDate") |
| UtcNow                     | This operator gets a DateTime object that is set to the current date and time on the computer, expressed as UTC. | DateTime.UtcNow |
| Today                      | This operator gets an object that is set to the current date, where the time component is set to 00:00:00. | DateTime.Today |
| Year                       | This operator gets the year component of the date that is represented by this instance. | @"user.creationDate".Year |
| Date                       | This operator gets a new object that has the same date as this instance, but where the time value is set to 00:00:00 (midnight). | @"user.creationDate".Date |

## Type casting operators

For information about type inferencing, see the [Type inference of attributes](fpl-lang-ref.md#type-inference-of-attributes) section later in this article.

| Operator     | Description | Example |
|--------------|-------------|---------|
| ToDateTime() | This operator converts a string to a *DateTime* object. | @"user.creationDate".ToDateTime() |
| ToDouble()   | This operator converts a string to a *Double* value. | @"productList.purchasePrice".ToDouble() |
| ToInt32()    | This operator converts a string to an *Int32* value. | @"riskScore".ToInt32() |

## Aggregation functions

| Function                    | Description | Example |
|-----------------------------|-------------|---------|
| Count()                     | This function returns the number of times that an event has occurred. | SELECT Count() AS numPurchases |
| DistinctCount(String *key*) | This function returns the number of distinct values for the specified property. If the specified property is null or empty for an incoming event, the event won't contribute to the aggregation. | SELECT DistinctCount(@"device.ipAddress") AS distinctIPs |
| Sum(Double *value*)         | This function returns the sum of values for a specified numeric property. | SELECT Sum(@"totalAmount") AS totalSpending |


## Defining your own variables

You can use the **LET** keyword to define a variable. That variable can then be referenced in other places in the rule. All variables should be prefixed by a dollar sign ($).


For example, you declare the following variable.

```FraudProtectionLanguage
LET $fullName = @"user.firstName" + @"user.lastName"
```

Variables that are declared in a **LET** statement can be used only within the scope of the rule or velocity set that the statement is defined in. 

For example, to reference the variable from the previous example, you can write the following statement.

```FraudProtectionLanguage
WHEN $fullName == "Kayla Goderich"
```

> [!NOTE]
> After a variable has been defined, it can't be updated with a new value.

## Using lists in rules

You can use the **ContainsKey** and **Lookup** operators to reference lists that you've uploaded to Fraud Protection. For more information about lists, see [Manage lists](lists.md).

### ContainsKey

To check whether one of your lists contains a specific value, use the **ContainsKey** operator. Specify the list name, the column, and the key that you want to check for.

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

For multi-column lists, you can use the **Lookup** operator to check the value of a column for a specific key.

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

You can also specify your own default value as the fifth parameter. For more information, see the [Logical operators](fpl-lang-ref.md#logical-operators) section earlier in this article.

The **Lookup** operator always returns a *String* value. To convert this value to an *Int*, *Double*, or *DateTime* value, use a [type casting operator](fpl-lang-ref.md#type-casting-operators).

## Using external calls and velocities

You can reference external calls and velocities by using the corresponding keyword. 

- To reference an external call in the language, type **External**, followed by the external call that you want to reference. For more information, see [Use an external call in rules](external-calls.md#use-an-external-call-in-rules).
- To reference a velocity in the language, type **Velocity**, followed by the individual velocity that you want to reference. For more information, see [Use a velocity in rules](velocities.md#use-a-velocity-in-rules).

## Type inference of attributes

Variable types are inferred from the context that they are used in. Here are some examples:

- In the expression **WHEN \@isEmailValidated**, the variable is interpreted as a *Boolean* value.
- In the expression **@"riskScore" \> 500**, the variable is interpreted as a *Double* value.
- In the expression **@"user.creationDate".Year \< DateTime.UtcNow.Year**, the variable is interpreted as a *DateTime* value.

If there isn't enough context to infer the type of a variable, it's considered a *String* value. For example, in the expression **@"riskScore" \< @"botScore"**, both variables are interpreted as strings.

To specify the type of a non-string variable, use a [type casting operator](fpl-lang-ref.md#type-casting-operators).

[!INCLUDE[footer-include](includes/footer-banner.md)]
