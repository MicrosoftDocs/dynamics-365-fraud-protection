---
author: josaw1
description: This article provides an overview of how to create functions in Fraud Protection.
ms.author: josaw
ms.date: 02/27/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Create functions

---

# Create functions
Dynamics 365 Fraud Protection gives you the flexibility to create functions that you can use to perform a specific task. For example, you can use functions to combine groups of code that must be executed together. Or you can use functions to reuse code, where you write the code once and access it from other places, making the code easier to maintain. In that example, if you want to call an external service to fetch a value from it, the logic can be defined within a function, and the function can be invoked from other resources.

## Define a function

Functions consist of input parameters and output properties. 

### Input parameters 

Functions can define parameters to be passed to the function at the time of invocation. Input parameters are defined in the function definition. The number of parameters passed into the function at invocation should exactly match the number of parameters defined for the function. The defined parameters can be used within the output properties to return a value. For more information, see [Output properties](Functions.md#output-properties). Defining input parameters is optional. 

Input parameters consist of the following three parts.

- **Parameter name**: A name with which the parameter can be referenced.
- **Data Type**: Every input parameter should have a data type associated to it. The data type that you specify converts the value of the parameter to the corresponding type. Functions support the data types listed in the following table.

  | Data type | Sample value | 
  |----------|---------------|
  | Boolean | True |
  | DateTime | Feb,22,2024 4:44PM |
  | Double | 10.0 |
  | Integer | 10 |
  | String | "Hello" |

- **Default Value**: A default value is required for every parameter. The defaukt value is used during "Function Evaluation," or if there is an issue with the function invocation. 


### Output properties 
You can define the return value of a function by using output properties. Output properties use the "Fraud Query Language (FQL)" logic to return a value of the function. The output properties can then be accessed from within other functions, rules, velocities, post-decision action rules, and routing rules when the function is invoked. A function can have up to 30 output properties. For more information on FQL and how to use it, see [Language reference guide](fpl-lang-ref.md).

Output properties consist of the following four parts.

- **Property description**: A description of the property. The description is optional. 
- **Data type**: The data type of the value that is returned from the property. Functions support all the primitive data types, such as boolean, datetime, double, integer, and string. Whenever a breaking change is made to the output property of a function that's referenced in other resources, the default value of the original output property "data type" is used as a fallback to proceed with the resource execution. We recommend that you update your resources after breaking changes.
- **Default value**: The default value is returned as the result of a function when an exception is encountered during the evaluation of the property. For example, division by 0, and Null Reference exceptions.
- **Code editor to return a value**: The code editor is used to return a value from the function. The following are ways to return an output value.

   1. Input parameters defined within a function can be used to return values.

      Example of an output property returning an input parameter as the return value. For more information on how to define input parameters, see the [Input Parameters](Functions.md#input-parameters) section earlier in this article.

  ```FraudProtectionLanguage
  RETURN _number1 + _number2
  ```

   2. Both the request and response attributes (including custom data) of an assessment that contains the rule that invokes the function. You can access these attributes with the *@* operator. For example, @"salesTax".
      
      Example of function using request attributes:
      
  ```FraudProtectionLanguage
  RETURN @"salesTax"
  ```

   3. The Fraud Protection enrichment data. For example, Geo.CountryCode().

      Example of function using riskscore:

  ```FraudProtectionLanguage
  RETURN Geo.CountryCode(@"deviceContext.ipAddress")
  ```

   4. Lists that you upload to Fraud Protection. For more information on how to upload lists, see [Manage lists](lists.md).

      Example of function using list:

  ```FraudProtectionLanguage
  RETURN Lookup("Country_Score", "Country", "US", "ScoreCutOff")
  ```

   5. Velocities that are defined in Fraud Protection. For more information, see [Perform velocity checks](velocities.md).

      Example of function using velocity:

  ```FraudProtectionLanguage
  RETURN Velocity.IPs_Per_User(@"deviceContext.ipAddress", 30s)
  ```

   6. External calls that were created in Fraud Protection. For more information, see [External calls](external-calls.md).

      Example of function using external calls:
      
  ```FraudProtectionLanguage
  RETURN External.weather("Seattle").id
  ```
   7. External assessments that were created in Fraud Protection. For more information, see [External Assessments](external-assessments.md).

      Example of a function invoking external assessment:

  ```FraudProtectionLanguage
  LET $result = Assessments.myAssessment.Evaluate($baseInput = @@)
  RETURN $result.ToStr()
  ```

   8. Access function within functions.

      Example of a function invoking another function:

  ```FraudProtectionLanguage
  RETURN Functions.MyFunction(@"totalAmount", @"salesTax").Calculate_Sum
  ```
       
> [!NOTE]
> You can create functions in any environment in the multi-hierarchy stack. When a function references resources such as velocities, external calls, lists, and external assessments that are available in the environment, the lower environments that invoke the function also inherit the resources that the function references. For example, if you create a function in the root that references an external call to return a value, the child environment that invokes the function can also access the result of that external call. For more information on how to inherit and invoke functions, refer to the [Function Inheritance](Functions.md#function-inheritance) section later in this article.


## Publish a function

1. In the [Fraud Protection portal](https://dfp.microsoft.com/), select **Functions** in the navigation bar, and then select **New Function**. Fraud Protection creates a draft function that's displayed only to you (the creator of the function). All changes that you make to the draft are automatically saved.

2. To define a new function from scratch, refer to the [Defining a Function](Functions.md#defining-a-function) section earlier in this article.

3. To publish the function, select **Publish**.
  
4. In the confirmation dialog box, you can change the name and description. Select **Publish**.

> [!NOTE]
> After you publish the function, it's visible to all users. The function can then be invoked within other functions, rules, velocities, post-decision rules, and routing rules. 

For information about how to use functions in other resources such as functions, rules, velocities, post decision actions, and routing rules, refer to the [Invoke functions from resources](Functions.md#invoke-functions-from-resources) section later in this article.

### The Sample pane

When you create or edit a function, the **Sample** pane appears on the side of the page.

- Functions aren't tied to any assessments. The sample payload is presented as a helpful guide for users that shows all the event properties that can be referenced in your functions. Select the event type in the **Event** field at the top of the pane.
  
- The **payload sample** section contains an example of the properties that can be sent in the request API for the assessment.


## Manage a function

1. To edit a previously published function, select the function and then select **Edit**. A draft of the published function is created and is available only to you. All of the changes that you make to the draft are automatically saved. To push your changes into production, select **Publish**. The previously published function is overwritten with your changes. To discard your draft, select **Discard**.

2. To delete an existing function, select the ellipsis (**...**), and then select **Delete**.

3. To update the name or description of a function, select the ellipsis (**...**), and then select **Rename**.

4. To search for a function, enter a keyword in the **Search** field. All of the function names and descriptions are searched, and the results are filtered according to the search keywords.

## Evaluate a function

Before you publish a function, you can use the **Function evaluation** pane to make sure that it returns the results that you expect.

- To open the function evaluation pane, select **Expand** in the **Functions** tab.
- To close the pane, select **Collapse**.

When the evaluation pane is open, the list of output properties is displayed with its result. The evaluation uses default values for input parameters and values from the sample payload section when determining what should be returned. If any of those values is changed, the output is also changed. That way, you can make sure that the correct values for each output property are returned. 

## Invoke functions from resources
The published functions can be invoked from resources such as rules, velocities, post-decision actions, and routing rules. All of the output properties defined within a function can be accessed by invoking the function. The values can then be used for decision-making. 

### Rules 
Functions can be invoked from any rule (within any assessment) in the same environment and from child environments in the hierarchy below. For more information about rules, see [Rules](rules.md).

```FraudProtectionLanguage
LET $sum = Functions.MyFunction(@"totalAmount", @"salesTax").Calculate_Sum
RETURN Approve()
WHEN $sum > 5
```

### Velocities 
Functions can be invoked from any velocity in the same environment and from child environments in the hierarchy below. For more information about velocities, see [Perform velocity checks](velocities.md).

```FraudProtectionLanguage
SELECT DistinctCount(@"device.deviceContextId") AS Devices_Per_IP
FROM AccountLogin
WHEN Functions.MyFunction(@"totalAmount", @"salesTax").Calculate_Sum > 5
GROUPBY @"device.ipAddress"
```

### Post-decision rules
Functions can be invoked from any post-decision action rule (within any assessment) in the same environment and from child environments in the hierarchy below. For more information about post-decision action rules, see [Post decision Action Rules](post-decision-action-rule.md).

```FraudProtectionLanguage
DO SetResponse()
WHEN Functions.MyFunction(@"totalAmount", @"salesTax").Calculate_Sum == 5
```

### Routing rules 
Functions can be invoked from any routing rules in the same environment and from child environments in the hierarchy below. For more information about routing rules, see [Case Management](case-management-overview.md).

```FraudProtectionLanguage
ROUTETO Queue("General Queue")
WHEN Functions.MyFunction(@"purchase.request.totalAmount", @"purchase.request.salesTax").Calculate_Sum > 5
```

## Function inheritance 
Functions can be invoked in the same environment and from child environments in the hierarchy below. The invocation syntax depends on where the function exists and where it is invoked from. Below are the different ways to invoke functions within a multi-hierarchy set up. 

> [!NOTE]
> If a function references resources such as velocities, lists, external calls, and external assessments, the resources are also inherited from child environments in the hierarchy below when the function gets invoked. 

### Invoke functions created within the same environment

The example below invokes a function from a rule where both the rule and the function exist in the same environment.

```FraudProtectionLanguage
LET $sum = Functions.MyFunction(@"totalAmount", @"salesTax").Calculate_Sum
RETURN Approve()
WHEN $sum > 5
```

### Invoke functions created within root environment

The example below invokes a function created in the root from a child environment.

```FraudProtectionLanguage
LET $sum = Functions.root.MyFunction(@"totalAmount", @"salesTax").Calculate_Sum
RETURN Approve()
WHEN $sum > 5
```

### Invoke the functions created within the parent environment

The example below invokes a function from the immediate parent environment.

```FraudProtectionLanguage
LET $sum = Functions.parent.MyFunction(@"totalAmount", @"salesTax").Calculate_Sum
RETURN Approve()
WHEN $sum > 5
```

### Invoke functions created within any environment above the stack

The example below invokes a function created in an environment above the stack and inherited from a rule within a lower environment.

```FraudProtectionLanguage
LET $sum = Functions.environment["environmentid"].MyFunction(@"totalAmount", @"salesTax").Calculate_Sum
RETURN Approve()
WHEN $sum > 5
```

## Function and resource limits

Fraud Protection has a limit on the number of functions that can be created per environment and the number of resources that can be referenced within a function. 

| Resource | Limit | 
|----------|---------------|
| Maximum number of functions that can be published within an environment | 30 |
| Maximum number of output properties that can exist within a function | 30 |
| Maximum number of unique velocities that a function can reference | 15 |
| Maximum number of external calls that a function can reference |2 |
| Maximum number unique list lookups that a function can reference | 5 |
| Maximum number of unique external assessments that a function can reference | 2​ |
| Maximum number of functions that a rule-set can invoke | 10 |​
| Maximum number of functions that a routing rule can invoke | 10 |
| Maximum number of functions that a post decision action can invoke | 10 |
| Maximum number of resources that a velocity can invoke | 10 |

