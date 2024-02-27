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
> Functions can be created within any environment in the multi hierarchy stack. When a function references resources like velocities, external calls, lists and external assessments which are available in that environment, the lower environments which invoke this function will also inherit the resources that the function references. For example, if a function created in the root references an external call to return a value, the child environment that invokes these functions will be able to access the result of that external call as well. To learn how to inherit and invoke functions, see [Function Inheritance](Functions.md#function-inheritance) section later in this article.


## Create a function

1. In the [Fraud Protection portal](https://dfp.microsoft.com/), from the left navigation, select **Functions**, and then select **New Function**.

    Fraud Protection creates a draft function that is visible only to you (the creator). Note that all changes that you make to the draft are automatically saved.

2. To define a new function from scratch, see the [Defining a Function](Functions.md#defining-a-function) section earlier in this article.

3. To publish the function, select **Publish**.
4. In the confirmation dialog box, you can change the name and description. When you're ready, select **Publish**.

> [!NOTE]
> After the function is published, the function is visible to all users. The function can then be invoked within other functions, rules, velocities, post-decision rules and routing rules. 

For information about how to use your functions within other resources like functions, rules, velocities, post decision action and routing rules see the [Invoke functions from resources](Functions.md#invoke-functions-from-resources) section later in this article.

### Understand the sample pane

When you create or edit a function, the **Sample** pane appears on the right side of the page.

- Functions are not tied to any assessments. The sample payload is just a helping guide for users that shows all the event properties that can be referenced in your functions. Select the event type in the **Event** field at the top of the pane.
- The **payload sample** section contains an example of the properties that can be sent in the request API for the assessment.


## Manage your function

1. To edit an existing published function, select the function, and then select **Edit**.

    A draft of your published function is created and is visible only to you. All changes that you make to the draft are automatically saved.

    When you're ready to push your changes into production, select **Publish**. The previously published function is overwritten with your changes.

    To discard your draft, select **Discard**.

2. To delete an existing function, select the ellipsis (**...**), and then select **Delete**.

3. To update the name or description of a function, select the ellipsis (**...**), and then select **Rename**.

4. To search for a function, enter a keyword in the **Search** field. All function names and descriptions are searched, and the results are filtered accordingly.

## Evaluate a function

Before you publish your new function, you can use the "Function evaluation" pane to make sure that it returns the results that you expect.

- To open the function evaluation pane, select **Expand** in the lower right of the **Functions** tab.
- To close the pane, select **Collapse**.

When the evaluation pane is open, you can see the list of output properties with its result. The evaluation uses "default" values for input parameters and values from the sample payload section when determining what should be returned, and if any of those values is changed then the output would also change accordingly. This will help you to understand if you are returning the correct values for each output property. 

## Invoke functions from resources
The published functions can be invoked from resources such as rules, velocities, post-decision actions, and routing rules. All the output properties defined within a function can be accessed by invoking the function. The values can then be used for decision making. 

### Invoking functions from Rules 
Functions can be invoked from any rule (within any assessment) within the same environment and from child environments in the hierarchy below. To learn more about rules, see [Rules](rules.md).
```FraudProtectionLanguage
LET $sum = Functions.MyFunction(@"totalAmount", @"salesTax").Calculate_Sum
RETURN Approve()
WHEN $sum > 5
```

### Invoking functions from Velocities 
Functions can be invoked from any velocity within the same environment and from child environments in the hierarchy below. To learn more about velocities, see [Perform velocity checks](velocities.md).
```FraudProtectionLanguage
SELECT DistinctCount(@"device.deviceContextId") AS Devices_Per_IP
FROM AccountLogin
WHEN Functions.MyFunction(@"totalAmount", @"salesTax").Calculate_Sum > 5
GROUPBY @"device.ipAddress"
```

### Invoking functions from Post Decision Rules
Functions can be invoked from any post-decision action rule (within any assessment) within the same environment and from child environments in the hierarchy below. To learn more about post decision action rules, see [Post decision Action Rules](post-decision-action-rule.md).
```FraudProtectionLanguage
DO SetResponse()
WHEN Functions.MyFunction(@"totalAmount", @"salesTax").Calculate_Sum == 5
```

### Invoking functions from Routing Rules 
Functions can be invoked from any routing rules within the same environment and from child environments in the hierarchy below. To learn more about routing rules, see [Case Management](case-management-overview.md).
```FraudProtectionLanguage
ROUTETO Queue("General Queue")
WHEN Functions.MyFunction(@"purchase.request.totalAmount", @"purchase.request.salesTax").Calculate_Sum > 5
```

## Function inheritance 
Functions can be invoked within the same environment and from child environments in the hierarchy below. The invocation syntax depends on where the function exists and from where it is invoked. Below are the different ways to invoke functions within a multi hierarchy set up. 

> [!NOTE]
> If a function references resources such as velocities, lists, external calls and external assessments, those resources will also be inherited from child environments in the hierarchy below when the function gets invoked. 

### Invoking the functions created within the same environment

Below example shows invoking function from a rule where both the rule and the function exist in the same environment.
```FraudProtectionLanguage
LET $sum = Functions.MyFunction(@"totalAmount", @"salesTax").Calculate_Sum
RETURN Approve()
WHEN $sum > 5
```
### Invoking the functions created within root environment
The below example shows invoking a function that is created in the root from a child environment.
```FraudProtectionLanguage
LET $sum = Functions.root.MyFunction(@"totalAmount", @"salesTax").Calculate_Sum
RETURN Approve()
WHEN $sum > 5
```
### Invoking the functions created within the parent environment

The below example shows invoking a function from the immediate parent environment.
```FraudProtectionLanguage
LET $sum = Functions.parent.MyFunction(@"totalAmount", @"salesTax").Calculate_Sum
RETURN Approve()
WHEN $sum > 5
```

### Invoking the functions created within any environment above the stack

The example below shows invoking a function that is created in an environment above the stack and inherited from a rule within a lower environment.
```FraudProtectionLanguage
LET $sum = Functions.environment["environmentid"].MyFunction(@"totalAmount", @"salesTax").Calculate_Sum
RETURN Approve()
WHEN $sum > 5
```
## Function and resource limits

Fraud Protection has a limit on the numbers of functions that can be created per environment and the resources that can be referenced within a function. The below are the limits.

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





​



