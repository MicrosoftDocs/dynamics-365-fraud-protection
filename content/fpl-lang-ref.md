---
author: josaw1
description: This article is a language reference guide for Microsoft Dynamics 365 Fraud Protection rules.
ms.author: josaw
ms.date: 01/22/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Language reference guide

---

# Language reference guide

Microsoft Dynamics 365 has its own rich and expressive language to help you define and express your fraud strategy. This language has many similarities to C# and SQL, and is designed to give you the flexibility that you need to address fraud for your unique business scenarios.

You can use this language today to define rules and velocities. For more information, see [Manage rules](rules.md) and [Perform velocity checks](velocities.md).

This language reference guide includes the complete list of operators, functions, and statements that make up the language:

- [Statements](fpl-lang-ref.md#statements)
- [Decision functions](fpl-lang-ref.md#decision-functions)
- [Action functions](fpl-lang-ref.md#action-functions)
- [Observation functions](fpl-lang-ref.md#observation-functions)
- [Model functions](fpl-lang-ref.md#model-functions)
- [Gibberish detection functions](fpl-lang-ref.md#gibberish-detection-functions)
- [Device attribute functions](fpl-lang-ref.md#device-attribute-functions)
- [Referencing attributes and variables](fpl-lang-ref.md#referencing-attributes-and-variables)
- [Logical operators](fpl-lang-ref.md#logical-operators)
- [List functions](fpl-lang-ref.md#list-functions)
- [Comparison operators](fpl-lang-ref.md#comparison-operators)
- [BIN Lookup functions](fpl-lang-ref.md#bin-lookup-functions)
- [Geo functions](fpl-lang-ref.md#geo-functions)
- [String functions](fpl-lang-ref.md#string-functions)
- [Math functions](fpl-lang-ref.md#math-functions)
- [Type casting operators](fpl-lang-ref.md#type-casting-operators)
- [DateTime functions](fpl-lang-ref.md#datetime-operators)
- [Aggregation functions](fpl-lang-ref.md#aggregation-functions)
- [Global Variables functions](fpl-lang-ref.md#global-variables-functions)

The guide also covers other articles. Here are some examples:

- [Defining your own variables](fpl-lang-ref.md#defining-your-own-variables)
- [Using lists in rules](fpl-lang-ref.md#using-lists-in-rules)

    - [ContainsKey](fpl-lang-ref.md#containskey)
    - [Lookup](fpl-lang-ref.md#lookup)

- [Using external calls, external assessments and velocities](#external)
- [Type inference of attributes](fpl-lang-ref.md#type-inference-of-attributes)
- [JSON Arrays and Objects](#arrays-objects)

## Statements

| Statement syntax | Description | Example |
|---------|-------------|-------------|
| LET <i>\<VariableName\></i> = <i>\<Expression\></i> | <p>A **LET** statement is used to define a new variable. The scope of the variable is the rule or velocity set it's defined in. Variable names should be prefixed with a dollar sign ($).</p><p>For more information, see [Defining your own variables](fpl-lang-ref.md#defining-your-own-variables).</p><p>Any number of **LET** statements can be used in the Condition section and the clauses of all rule types and velocity sets.</p> | LET $fullName = @"user.firstName" + @"user.lastName" |
| <p>OBSERVE</p><p>OBSERVE \<<i>ObservationFunction</i>\>(\<<i>KeyValuePairs</i>\>)<br>[ WHEN \<<i>BooleanExpression</i>\></p> ]| <p>An **OBSERVE** statement doesn't terminate rule execution with a decision. It merely logs key-value pairs to either the API response or trace logs. Subsequent rules and rule clauses continues to run until a **RETURN** statement is reached.</p><p>An **OBSERVE** statement must be followed by one or more [observation functions](fpl-lang-ref.md#observation-functions).</p><p>If a **WHEN** clause is present and is evaluated to **False**, the **OBSERVE** statement isn't logged.</p><p>A maximum of one can be used for each clause in the following rules:</p><ul><li>Purchase rules</li><li>Custom Assessment rules</li><li>Account Protection rules</li><ul> | <p>OBSERVE Output(reason="high score")</p><p>OBSERVE TRACE(ip=@"device.ipAddress") WHEN @"riskscore" \> 400 | 
| RETURN \<<i>DecisionFunction</i>\><br>[ ,\<<i>ObservationFunction</i>\>(\<<i>KeyValuePairs</i>\>) ]<br>[ WHEN \<<i>BooleanExpression</i>\> ] | <p>A **RETURN** statement terminates rule execution with a decision.</p><p>The statement must specify a valid [decision function](fpl-lang-ref.md#decision-functions): **Approve()**, **Reject()**, **Challenge()**, or **Review()**.</p><p>The statement can also specify one or more [observation functions](fpl-lang-ref.md#observation-functions): **Output()** or **Trace()**</p><p>Finally, the statement can include a **WHEN** clause to specify the condition under which it should do any of the preceding.</p><p>A maximum of one can be used per clause in the following rules:</p><ul><li>Purchase rules</li><li>Custom Assessment rules</li><li>Account Protection rules</li><ul> | <p>RETURN Review()<br>WHEN IsWatch("Device Support List", @"deviceAttributes.deviceId") \|\|<br>IsWatch("Payment Support List", @"paymentInstrumentList.merchantPaymentInstrumentId")</p><p>RETURN Reject(), Trace(ip=@"device.ipAddress") WHEN @"riskscore" \> 400</p> |
| ROUTETO QUEUE <i>\<QueueName\></i><br>[ WHEN \<<i>BooleanExpression</i>\> ] | <p>The **ROUTETO** command is used in routing rules to direct matching assessments to [case management queues](case-management-administrator.md).</p><p>The optional **WHEN** clause can be used to describe the conditions under which the command should perform the routing.</p><p>A maximum of one can be used per clause in routing rules.</p> | ROUTETO Queue("High Value Queue")<br>WHEN @"purchase.request.totalAmount" \> 500 | 
| SELECT <i>\<AggregationFunction\></i><br>AS <i>\<VelocityName\></i><br>FROM <i>\<AssesmentType\></i><br>GROUPBY <i>\<GroupExpression\></i><br>[ WHEN <i>\<BooleanExpression\></i> ] | <p>A **SELECT** statement is used in velocity sets to define a [velocity](velocities.md). It must specify an [aggregation function](fpl-lang-ref.md#aggregation-functions).</p><p>The required **AS** clause is used to create an alias for your velocity. This alias can then be referenced from rules.</p><p>The required **FROM** clause is used to specify the assessment type to observe a velocity on. Valid values are **Purchase**, **AccountLogin**, **AccountCreation**, **Chargeback**, **BankEvent**, and **CustomAssessment**.</p><p>The required **GROUPBY** clause specifies a property or an expression. All events that are evaluated to the same value in the **GROUPBY** statement are combined to calculate the aggregation requested in the **SELECT** statement.</p><p>For example, to calculate an aggregation for each user, use **GROUPBY @"user.userId"**.</p><p>The optional **WHEN** clause specifies a Boolean expression that determines whether the assessment that's being processed should be included in the velocity that's being defined.</p><p>A maximum of one can be used per clause in velocity sets.</p>| <p>SELECT Count() AS _Purchase_Rejections_Per_Email<br>FROM Purchase<br>WHEN @"ruleEvaluation.decision" == "Reject"<br>GROUPBY @"user.email"</p><p>SELECT DistinctCount(@"purchaseId")<br>AS _BankDeclines_Per_Device<br>FROM BankEvent<br>WHEN @"status" == "DECLINED"<br>GROUPBY @"purchase.deviceContext.externalDeviceId"</p> |
| WHEN \<<i>BooleanExpression</i>\> | <p>The **WHEN** statement is like the **WHEN** clauses on the other statements, but it stands alone in the Condition section of rules and velocity sets. It specifies a Boolean condition that determines whether the whole rule, velocity set, or routing rule should run.</p><p>A maximum of one can be used in the Condition section of all rule types and velocity sets.</p> | WHEN @"riskscore" \> 400 |
|DO \<<i>Action function</i>\>|A **DO** statement is used to perform some action at the end of rule execution. This statement can only be used in Post-decision actions, and followed by an Action function|DO SetResponse(name = @”firstname” + @”lastname”)|

## Decision functions

Decision functions are used in rules to specify a decision.

| Decision type                     | Description | Example |
|-----------------------------------|-------------|---------|
| Approve()                         | <p>This type specifies a decision of *Approve*. It can include a reason for the approval and another supporting message.</p><p>Overloads:</p><ul><li>Approve(String *reason*)</li><li>Approve(String *reason*, String *supportMessage*)</li></ul> | <p>RETURN Approve()</p><p>RETURN Approve("on safe list")</p><p>RETURN Approve ("on safe list", "do not escalate")</p> |
| Reject()                          | <p>This type specifies a decision of *Reject*. It can include a reason for the rejection and another supporting message.</p><p>Overloads:</p><ul><li>Reject(String *reason*)</li><li>Reject(String *reason*, String *supportMessage*)</li></ul> | <p>RETURN Reject()</p><p>RETURN Reject("embargo country")</p><p>RETURN Reject("embargo country", "do not escalate")</p> |
| Review()                          | <p>This type specifies a decision of *Review*. It can include a reason for the review and another supporting message.</p><p>Overloads:</p><ul><li>Review(String *reason*)</li><li>Review(String *reason*, String *supportMessage*)</li></ul> | <p>RETURN Review()</p><p>RETURN Review("user on watch list")</p><p>RETURN Review("user on watch list", "do not escalate")</p> |
| Challenge(String *challengeType*) | <p>This type specifies a decision of *Challenge* and a challenge type. It can also include a reason for the challenge and another supporting message.</p><p>Overloads:</p><ul><li>Challenge(String *challengeType*, String *reason*)</li><li>Challenge(String *challengeType*, String *reason*, String *supportMessage*)</li></ul> | <p>RETURN Challenge ("SMS")</p><p>RETURN Challenge ("SMS", "suspected bot")</p><p>RETURN Challenge ("SMS", suspected bot", "do not escalate")</p> |

## Action functions

Action functions are used to specify the action to be taken in a Post-decision action rule

| Action type | Description | Example |
|-------------|-------------|---------|
|SetResponse(String sectionName, k=v)|<p>This function can be used to pass key-value pairs to the “CustomProperties” section of API response. You can specify a subsection sectionName for the key values pair to go into. </p><p>Overloads:</p>•&nbsp;&nbsp;&nbsp;SetResponse(k=v)|<p>SetResponse(“Scores”, bot = Model.Bot(@deviceContextId), risk=Model.Risk())</p><p>SetResponse(test=”123”)</p>|
 

## Observation functions

Observation functions can be used to take data from the current context and write it somewhere else.

| Return type | Description | Example |
|-------------|-------------|---------|
| Output(k=v)  | This function can be used to pass key-value pairs into the API response. | Output(key="test", email=@"user.email", countryRegion=Geo.CountryRegion(@"device.ipAddress")) |
|Trace(k=v)   | This function can be used to trigger a Trace event and send key-value pairs to the FraudProtection.Trace.Rule [Event Tracing namespace](event-tracing.md#event-schemas). | Trace(key="Manual Review", ip=@"device.ipAddress") |

## Model functions

Model functions run the various fraud models and are useful when your assessment does not automatically run one or more fraud models. When model functions run, information about the model running during rule evaluation is output in the fraud assessment API call. Then, the rule gets access to the model result, including score, reasons, and more, that can be used for further rule processing and decision making.

| Model type     | Description | Example |
|--------------|-------------|---------|
|  Risk  |  Assesses the likelihood of a session being risky. | Model.Risk()  |
| Bot   |   Assesses the likelihood of a session being bot-initiated. Pass in a device context ID that was sent to Fraud Protection’s device fingerprinting solution. | Model.Bot(@deviceContextId)   |

## Gibberish detection functions
These functions help prevent fraud by quicky and efficiently detecting whether key user-input fields (such as names and addresses) contain gibberish. 

| Function     | Description | Example |
|--------------|-------------|---------|
| GetPattern(String).maxConsonants |  Maximum number of contiguous consonants in a string that are not separated by a vowel. For example maxConsonants for the string “01gggyturah” is 5.   |  GetPattern(@"user.email").maxConsonants |
| GetPattern(String).gibberScore  |  ML based score between 0 and 1; 0 means most likely to be gibberish and 1 means least likely to be gibberish.  | GetPattern(@"user.email").gibberScore  |


> [!NOTE]
> Gibberish detection model is based on the frequency of two consecutive alphanumeric characters in publicly available english documents. It is assumed that the more frequently two consecutive alphanumeric characters appear in public documents, less likely that they are gibberish. The model should provide reasonable scores for english texts, and can be used to detect if the names or addresses contains gibberish. However, the model might not be suitable for abbreviations, such as short form for states (AZ, TX, etc.) and it also can't be used to validate names or addresses. Lastly, the model has not been tested for non-English texts.


## Device attribute functions

| Operator     | Description | Example |
|--------------|-------------|---------|
|  Device.GetAttributes(String _sessionId_)  | Returns selected device attributes from device fingerprinting. The selected device attributes are curated by Fraud Protection and are a set of attributes commonly used in rules. | Device.GetAttributes(@"deviceContext.deviceContextId).attribute_name  |
| Device.GetFullAttributes(String _sessionId_)   | Returns a full set of device attributes from device fingerprinting. Use this function only when needed to access the full set of device attributes. To view the full set of device attributes, see [Set up device fingerprinting](device-fingerprinting.md). | Device.GetFullAttributes(@"deviceFingerprinting.id").attribute_name   |

## Referencing attributes and variables
You can use the at sign (@) operator to reference an attribute from the current event.

| Variable     | Description | Example |
|--------------|-------------|---------|
| @            | <p>An at sign (@) is used to reference an attribute from the incoming event. The attribute might be sent as part of the request payload, or it might be generated by Microsoft Dynamics 365 Fraud Protection.</p><p>After the at sign (@), specify the full path of the attribute that you want to reference. Enclose the path in quotation marks (for example, *@"address.city"*).</p><p>If the referenced attribute isn't part of the event payload, the default value for that type is returned: 0.0 for doubles, an empty string for strings, and so on.</p><p>The type of the attribute is inferred from the context it's used in. If not enough context is provided, the *String* type is used by default.</p><p>For information about type inference, see [Type inference of attributes](fpl-lang-ref.md#type-inference-of-attributes).</p> | <p>@"address.city"</p> |
| $            | A dollar sign ($) is used to reference a variable that has been defined in a **LET** statement. For more information, see [Defining your own variables](fpl-lang-ref.md#defining-your-own-variables). | $fullName |
| @"botScore"  | <p>For every Account Creation or Account Login event, Fraud Protection's AI models generate a bot score between 0 and 999. A higher score indicates a higher probability that the event was initiated by a bot.</p><p>You can use *@botScore* to reference this score in [post-bot-scoring clauses](rules.md#post-bot-scoring-clauses) and [post-risk-scoring clauses](rules.md#post-risk-scoring-clauses).</p> | @"botScore" |
| @"riskScore" | <p>For every Purchase or Account Protection event, Fraud Protection's AI models generate a risk score between 0 and 999. A higher score indicates a higher risk.</p><p>You can use *@riskScore* to reference this score in post-risk-scoring clauses.</p> | @"riskScore" |
| @a[x\]      | <p>This variable is used to index array variables.</p><p>If the request payload for an assessment contains an array of items, you can access individual elements of the array by using the following syntax: *@"productList\[0\]"*.</p><p>To access an attribute of that element, use the following syntax: *@"productList\[0\].productId"*</p> | <p>@"productList\[0\].productId"</p><p>@"paymentInstrumentList\[3\].type"</p> |
| Exists       | <p>This operator checks whether a variable exists in the event payload.</p><p>Exists(*String variable*)</p> | Exists(@"user.email") |
|Response.Decision()|This function references the decision for the current assessment being evaluated.| Response.Decision() == “Approve”|
|Request.CorrelationId()|This function references the unique Correlation ID of the event being evaluated. You can use this function to access the Correlation ID of an event in the rules experience and pass it to an external call as a parameter or a header.| External.MyExternalCall(Request.CorrelationId())|
|.GetDiagnostics()|This function can be used to discover important diagnostic and debug information from an external call or an external assessment response. For an external call, the Diagnostics object contains the Request payload, Endpoint, HttpStatus code, Error message, and Latency. Endpoint isn't available in the Diagnostic object for an external assessment response. Any of these fields can be used in the rules once the Diagnostics object has been created by using its corresponding extension method, “.GetDiagnostics()”|<p>LET $extResponse = External. myCall(@"device.ipAddress")</p><p>LET $extResponseDiagnostics = $extResponse.GetDiagnostics()</p><p>OBSERVE Output(Diagnostics = $extResponseDiagnostics )</p><p>WHEN $extResponseDiagnostics. HttpStatusCode != 200|


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
| Lookup(<br>String *listName*,<br>String *keyColName*,<br>String *valueColName*) | <p>This operator looks up the value of a key in a Fraud Protection list. Both the name of the column that contains the key and the name of the column that contains the value must be specified.</p><p>The value is always returned as a string.</p><p>If the key isn't found, and if the **defaultValue** parameter isn't specified, "Unknown" is returned.</p> | <p>Lookup("Email Support List", "Emails", @"user.email", "Status",0)</p><p>This example looks for the *@"user.email"* variable in the "Emails" column of the "Email Support List" list and returns the corresponding value in the "Status" column.</p><p>If the key isn't found in the list, Fraud Protection returns 0.</p> |
| LookupClosest(<br>String *listName*, String *keyColumnName*, String *key*,<br> String *valueColumnName*, String *defaultValue*)<br> | <p>This operator looks up the value of a key in a Fraud Protection list. If the key isn't found, the value of the key that is alphabetically closest to the key that you're looking for is returned.</p><p>Overloads:</p><ul><li>Lookup(String *listName*, String *keyColumnName*, String key, String valueColumnName, String defaultValue)</li></ul> | <p>LookupClosest("IP Addresses", "IP", @"device.ipAddress", "City") == "Seattle"</p><p>This example looks for the *@ipAddress* variable in the "IP" column of the "IP Addresses" list and returns the corresponding value in the "City" column. If *@ipAddress* isn't found in the list, the expression returns the value of the next closest IP address in the list.</p> |
| In | <p>This operator checks whether a key is contained in a comma-separated list of values.</p><p>In(String *key*, String *list*)</p> | In(@"user.countryRegion", "US, MX, CA") |

## Comparison operators

Fraud Protection supports all standard C# [comparison](/dotnet/csharp/language-reference/operators/comparison-operators) and [equality](/dotnet/csharp/language-reference/operators/equality-operators) operations. This table includes some examples of operators that you might find useful. If you apply these operators to strings, lexicographic comparisons occur.

| Operator | Description | Example |
|----------|-------------|---------|
| ==       | This operator checks for equality. | @"user.countryRegion" == @"shippingAddress.countryRegion" |
| !=       | This operator checks for inequality. | @"user.countryRegion" != @"shippingAddress.countryRegion" |
| \>       | This operator checks whether the first value is greater than the second value. | @"riskScore" \> 500 |
| \<       | This operator checks whether the first value is less than the second value. | @"riskScore" \< 500 |
| \>=      | This operator checks whether the first value is greater than or equal to the second value. | @"riskScore" \>= 500 |
| \<=      | This operator checks whether the first value is less than or equal to the second value. | @"riskScore" \<= 500 |

## BIN Lookup functions
BIN Lookup functions provide payment card account information (for example, card network, card type, card country code) based on bank identification number (BIN). Data for BIN Lookup is sourced from leading third-party BIN data providers and then curated by Microsoft Fraud Protection.

| Operator                       | Description | Example |
|--------------------------------|-------------|---------|
|BIN.Lookup(String *BIN*).cardNetwork|<p> This function looks up BIN and returns card's network (for example, Visa, Mastercard).|BIN.Lookup(@"card.bin").cardNetwork|
|BIN.Lookup(String *BIN*).cardType|<p> This operator looks up BIN and returns card type (for example, Debit, Credit).|BIN.Lookup(@"card.bin").cardType|
|BIN.Lookup(String *BIN*).issuer|<p> This operator looks up BIN and returns issuing organization.|BIN.Lookup(@"card.bin").issuer|
|BIN.Lookup(String *BIN*).countryCode|<p> This operator looks up BIN and returns ISO two-letter country code of the card.|BIN.Lookup(@"card.bin").countryCode|
|BIN.Lookup(String *BIN*).error|<p> This operator looks up BIN and returns an error message if the BIN could not be found.|BIN.Lookup(@"card.bin").error|

## Geo functions

Geo functions provide resolution by converting an IP address to a geographical address. Geo functions can be invoked in rules only by using IPs that are part of transaction payload or collected by Fraud Protection by using Device Fingerprinting. Geo functions can't be invoked for arbitrary IP values.

| Operator                       | Description | Example |
|--------------------------------|-------------|---------|
| Geo.RegionCode(String *ip*)    | <p>This operator converts an IPv4 address to its US region code (that is, the abbreviation for the name of the US state or territory).</p><p>For example, for an IP address in Washington state, "WA" is returned.</p> | Geo.RegionCode(@"device.ipAddress") |
| Geo.Region(String *ip*)        | <p>This operator converts an IPv4 address to its US region (that is, the name of the US state or territory).</p><p>For example, for an IP address in Washington state, "Washington" is returned.</p> | Geo.Region(@"device.ipAddress") |
| Geo.CountryCode(String *ip*)   | <p>This operator converts an IPv4 address to its country/region code.</p><p>For example, for an IP address in Australia, "AU" is returned.</p> | Geo.CountryCode(@"device.ipAddress") |
| Geo.CountryRegion(String *ip*) | <p>This operator converts an IP address to a region name.</p><p>For example, for an IP address in Australia, "Australia" is returned.</p> | Geo.CountryRegion(@"device.ipAddress") |
| Geo.City(String *ip*)          | <p>This operator converts an IPv4 address to a city name.</p><p>For example, for an IP address in New York City, "New York City" is returned.</p> | Geo.City(@"device.ipAddress") |
| Geo.MarketCode(String *ip*)    | <p>This operator converts an IPv4 address to the market code of the IP address.</p><p>For example, for an IP address from Canada, "NA" (North America) is returned.</p> | Geo.MarketCode(@"device.ipAddress") |

## String functions

Fraud Protection supports the standard C# [string class](/dotnet/api/system.string?view=netframework-4.8&preserve-view=true). This table includes some examples of functions and operators that you might find useful.

| Operator                    | Description | Example |
|-----------------------------|-------------|---------|
| Contains(String *substring*)   | <p>This operator checks whether a string contains another string.</p><p>Contains(String *substring*)</p> | @"productList`.productName".Contains("Xbox") |
| ContainsOnly(*CharSet*) | <p> This operator checks whether a string contains only the charsets provided.</p><p>ContainsOnly(Charset1 Charset2 ...etc.)</p>|@"zipcode".ContainsOnly(CharSet.Numeric)|
| ContainsAll(*CharSet*) |<p> This operator checks whether a string contains all the charsets provided.</p><p>ContainsAll(Charset1 Charset2 ...etc.)</p>|@ “zipcode”.ContainsAll(CharSet.Numeric\|CharSet.Hypen)|
| ContainsAny(*CharSet*)|<p> This operator checks whether a string contains any of the charsets provided.</p><p>ContainsAll(Charset1 Charset2 ...etc.)</p>|@”zipcode”.ContainsAny(CharSet.Numeric\|CharSet.Hypen)|
| StartsWith(String *prefix*) | <p>This operator checks whether a string begins with a specified prefix.</p><p>StartsWith(String *prefix*)</p> | @"user.phoneNumber".StartsWith("1-") |
| EndsWith(String *suffix*)   | <p>This operator checks whether a string ends with a specified suffix.</p><p>EndsWith(String *suffix*)</p> | @"user.email".EndsWith("@contoso.com") |
| IsNumeric()  | <p>This operator checks whether a string is a numeric value.</p><p>(String).IsNumeric()</p> | @"user.email".IsNumeric() |
| Length  | <p>This operator returns the number of characters in the string.  | @"user.username".Length |
| Convert.ToDateTime(@"user.creationDate").ToString("yyyy-MM-dd HH:mm:ss")  | <p>This operator converts the string to datetime and converts datetime to a string using the given format.| Convert.ToDateTime(@"user.creationDate").ToString("yyyy-MM-dd") |

### Using CharSet in ContainsOnly, ContainsAll, and ContainsAny

The following character types can be used in ContainsOnly, ContainsAll, and ContainsAny.

| Character Type | Description |
|----------------|-------------|
| Alphabetic | a-z, A-Z |
| Apostrophe |	' |
| Asperand	| @ |
| Backslash |	\ |
| Comma	| , |
| Hypen	| - |
| Numeric	| 0-9 |
| Period	| . |
| Slash	| / |
| Underscore |	_ |
| WhiteSpace |	Single space |

## Math functions

Fraud Protection supports all standard C# [math methods](/dotnet/api/system.math?view=netframework-4.8&preserve-view=true) and [arithmetic operators](/dotnet/csharp/language-reference/operators/arithmetic-operators). This table includes some examples of methods that you might find useful.


| Operator                                   | Description | Example |
|--------------------------------------------|-------------|---------|
| Math.Min(Double *value1*, Double *value*2) | This operator computes the minimum of two values. | Math.Min(@"riskScore",@"botScore") |
| Math.Max(Double *value1*, Double *value*2) | This operator computes the maximum of two values. | Math.Max(@"riskScore",@"botScore") |
| RandomInt(Integer *min*, Integer *max*) | This operator returns a random integer in the range provided, including the minimum value and excluding the maximum value. | RandomInt(0, 100) |


## DateTime operators

Fraud Protection supports the standard C# [DateTime](/dotnet/api/system.datetime?view=netframework-4.8&preserve-view=true) properties, methods, and operators. This table includes some examples of functions and properties that you might find useful.

| Operator                   | Description | Example |
|----------------------------|-------------|---------|
| DaysSince(DateTime *date*) | This operator returns an integer that represents the number of days that passed between the specified *DateTime* value and the current date (expressed as Coordinated Universal Time \[UTC\]). | DaysSince(@"user.CreationDate") |
| UtcNow                     | This operator gets a DateTime object that is set to the current date and time on the computer, expressed as UTC. | DateTime.UtcNow |
| Today                      | This operator gets an object that is set to the current date, where the time component is set to 00:00:00. | DateTime.Today |
| Year                       | This operator gets the year component of the date represented by this instance. | @"user.creationDate".Year |
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
| Count()                     | This function returns the number of times that an event occurred. | SELECT Count() AS numPurchases |
| DistinctCount(String *key*) | This function returns the number of distinct values for the specified property. If the specified property is null or empty for an incoming event, the event won't contribute to the aggregation. | SELECT DistinctCount(@"device.ipAddress") AS distinctIPs |
| Sum(Double *value*)         | This function returns the sum of values for a specified numeric property. | SELECT Sum(@"totalAmount") AS totalSpending |

## Global Variables functions

Global Variables functions can be used to set and get global variables within rules, velocities, routing rules, and post-decision action rules. The variables that are set can be accessed from within the same environment or from environments down the stack. For example, if you set global variables in a rule within the root environment, the variables can be accessed within the rules from the same environment or from their children. Also, global variables are specific to an assessment. A variable set within one assessment can't be accessed from another assessment. 

| Operator | Description | Example |
|-------------|-------------|---------|
| SetVariables(k=v)  | This function can be used to set key-value pairs, i.e., set values to variables. | Do SetVariables(key= 123, email=@"user.email") |
| GetVariable("k")   | This function can be used to access the variables that are already set. In cases where we access variables that is never set, a default value will be returned.| <p>GetVariable("key").AsInt()</p><p>GetVariable("email").AsString()<p>GetVariable("key").AsDouble()</p><p>GetVariable("key").AsBool()</p><p>GetVariable("key").AsDateTime()<p>GetVariable("key").AsJsonObject()</p><p>GetVariable("key").AsJsonArray()</p> |

## Defining your own variables

You can use the **LET** keyword to define a variable. That variable can then be referenced in other places in the rule. Prefix all variables by a dollar sign ($).


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
> After a variable is defined, it can't be updated with a new value.

## Using lists in rules

You can use the **ContainsKey** and **Lookup** operators to reference lists that you uploaded to Fraud Protection. For more information about lists, see [Manage lists](lists.md).

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

## <a name='external'></a> Using external calls, external assessments and velocities

- To reference an external call, type **External**, followed by the external call that you want to reference. For more information, see [Use an external call in rules](external-calls.md#use-an-external-call-in-rules).
- To reference an external assessment, type **Assessments**, followed by the external assessment that you want to reference. For more information, see [Use an external assessment in rules](external-assessments.md).
- To reference a velocity, type **Velocity**, followed by the velocity that you want to reference. For more information, see [Use a velocity in rules](velocities.md#use-a-velocity-in-rules).

## Type inference of attributes

Variable types are inferred from the context that they are used in. Here are some examples:

- In the expression **WHEN \@isEmailValidated**, the variable is interpreted as a *Boolean* value.
- In the expression **@"riskScore" \> 500**, the variable is interpreted as a *Double* value.
- In the expression **@"user.creationDate".Year \< DateTime.UtcNow.Year**, the variable is interpreted as a *DateTime* value.

If there isn't enough context to infer the type of a variable, it's considered a *String* value. For example, in the expression **@"riskScore" \< @"botScore"**, both variables are interpreted as strings.

To specify the type of a non-string variable, use a [type casting operator](fpl-lang-ref.md#type-casting-operators).

[!INCLUDE[footer-include](includes/footer-banner.md)]

## <a name='arrays-objects'></a> JSON Arrays and Objects
FQL has support for the construction of complex structured objects as local variables, which may be passed through to the external call or external assessment in JSON form. As with all other locals in FQL, arrays and objects are immutable once created.

### JSON arrays

Arrays are created by enclosing expressions in a pair of brackets:
```FraudProtectionLanguage
LET $arr1 = [ "hello", "world" ]
LET $arr2 = [
  "this is also an array",
  78.4,
  $arr1,
  @"user.email",
  External.MyExtcall()
]
```

### JSON objects

Objects are created with braces:
```FraudProtectionLanguage
LET $obj1 = { isObject: true }
LET $obj2 = {
  numberField: 7,
  fieldIs: "string",
  internalObj: $obj1,
  inline: {
    innerInnerField: "hello"
  }
}
```

### FQL functions for JSON Arrays & Objects

| Syntax | Description | Example |
|---------|-------------|-------------|
|**Array.GetValue** (TargetArray **.AsJsonArray**(), matchKey, matchValue, lookupKey)|<p>With this function, you can access the first array element that matches a condition.</p><p><i>Returns a value</i></p>|**Array.GetValue**(@@"payloadProperty"**.AsJsonArray**(), matchKey, matchValue, lookupKey)|
|**Array.GetValues**(TargetArray **.AsJsonArray**(), matchKey, matchValue)|<p>With this function, you can access a set of array elements that match a condition.</p><p><i>Returns an array</i></p>|**Array.GetValues**(@@"payloadProperty"**.AsJsonArray**(), matchKey, matchValue)|

Here are some more detailed examples of how to use the above syntax based on different array sources: 

| Array Source | Array.GetValue  | Array.GetValues  |
|---------|-------------|-------------|
|External assessments |<p>LET $a = Assessments.myAssessment.evaluate()</p><p>LET $sample = Array.GetValue($a.ruleEvaluations.AsJsonArray(), "rule", "Sample Payload Generation", "clauseNames")</p><p>RETURN Approve()</p><p>WHEN $sample[0].AsString() == "TestData"</p>|<p>LET $a = Assessments.myAssessment.evaluate()</p><p>LET $sample = Array.GetValues($a.ruleEvaluations.AsJsonArray(), "rule", "Sample Payload Generation")</p><p>RETURN Approve()</p><p>WHEN $sample[0].clauseNames[0].AsString() == "TestData"</p>|
|Payload|<p><i>Payload sample: {"group":[{"item1": "a", "item2": "a1"}, {"item1": "b", "item2": "b1"}]}</i></p></p>LET $sample = Array.GetValue(@@"group".AsJsonArray(), "item1", "a", "item2")</p><p>RETURN Approve()WHEN $sample.AsString() == "a1"</p>|<p><i>Payload sample: { "group":[{"item1": "a", "item2": "a1"}, {"item1": "b", "item2": "b1"}]}</i></p><p>LET $sample = Array.GetValues(@@"group".AsJsonArray(), "item1", "a")</p><p>RETURN Approve()</p><p>WHEN $sample[0].item2.AsString() == "a1"|
|Global variables|<p><i>Using same payload sample as above</i></p><p>Do SetVariables(Var=@@"group")</p><p>LET $group = GetVariable("Var").AsJsonObject()</p><p>LET $value = Array.GetValue($group, "item1", "a", "item2")</p><p>RETURN Approve()</p><p>WHEN $value.AsString() == "a1"</p>|<p><i>Using same payload sample as above</i></p><p>Do SetVariables(Var=@@"group")</p><p>LET $group = GetVariable("Var").AsJsonObject()</p><p>LET $arr = Array.GetValues($group.AsJsonArray(), "item1", "a")</p><p>RETURN Approve()</p>|
|External call|<p><i>External call (**myCall**) response: {"group":[{"item1": "a", "item2": "a1"}, {"item1": "b", "item2": "b1"}]}</i></p><p>LET $x = External.myCall().AsJsonObject()</p><p>LET $value = Array.GetValue($x.group[0].AsJsonObject(), "item1", "a", "item2")</p><p>RETURN Approve()</p><p>WHEN $value.AsString() == "a1"</p>|<p><i>External call (**myCall**) response: {"group":[{"item1": "a", "item2": "a1"}, {"item1": "b", "item2": "b1"}]}</i></p><p>LET $x = External.myCall().AsJsonObject()</p><p>LET $arr = Array.GetValues($x.group[0].AsJsonObject(), "item1", "a")</p><p>RETURN Approve()WHEN $arr[0].item2.AsString() == "a1"</p>|

> [!NOTE]
> Arrays can NOT be used as a key (Group by) in velocities

### Type casting for JSON Arrays and Objects

  - Following .As\<Type\>() are supported from the JsonObject:
    -	AsString()
    -	AsInt()
    -	AsDouble()
    -	AsDateTime()
    -	AsBool()
    -	AsJsonArray()
    -	AsJsonObject()

  - When you use array helper methods, .GetValue or .GetValues, you need to type cast using **.As<i>\<Type\></i>**().
    Example:
    ```FraudProtectionLanguage
    LET $arr = {myArr:[{item1: "red", number: 45}, {item1: "blue", number: 56}, {item1: "green", number: 33}]}
    LET $sample = Array.GetValues($arr.myArr.AsJsonArray(), "item1", "blue")
    ```

  - Once have converted to Array/Object explicitly, you may need to use **.As<i>\<Type\></i>**() to cast to a specific data type. 
    Example:
    ```FraudProtectionLanguage
    RETURN Approve()
    WHEN $sample[0].number.AsInt() == 56
    ```

  - When you use @@, it implicitly type casts the data to a JSON object. If you then want to convert the JSON Object to a different data type, you will need to use **.As<i>\<Type\></i>**(). 
    Example:
    ```FraudProtectionLanguage
    LET $sample = @@”user.addresses”.AsJsonArray()
    ```
  
  - When you want to output in a certain format, you will need to use **.As<i>\<Type\></i>**(). 
    Example:
    ```FraudProtectionLanguage
    LET $sample = @@”user.addresses”
    Output(abc = $sample.AsJsonArray())
    ```

> [!NOTE]
> Type casting best practices:
>   - Always type cast at the end of the .Chain
>    >     Example:
>    >     LET $sample = External.myCall().data[0].Item1[0].AsJsonArray()
>    >                                  -OR-
>    >     LET $sample = @@”accommodations[0].rooms”.AsJsonArray()
>    - When unsure, always explicitly type cast using .As\<Type\>()

