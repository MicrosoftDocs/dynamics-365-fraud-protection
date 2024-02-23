
# Functions
Microsoft Dynamics 365 Fraud Protection gives you the flexibility to create functions which are used to perform a specific task. Using functions, you can plug in groups of code that can be always run together and can be reused which can then be accessed from other places within DFP for decision making. For example, if we want to call an external service to fetch a value from it, that logic can be defined within a function and then this function can be invoked from other resources.

## Defining a Function: Quick start guide

Functions consist of input parameters and output properties. 

### Input Parameters 

Functions can define parametrs which can be passed to the function at the time of invocation. The input parameters are defined in the function defenition. The number of parameters passed into the function at invocation should exactly match the number of parameters defined for this function. Input parametrs are optional and the defined parameters can be used within the Output properties to return a value. For more information, see the [output properties](Functions.md#output-properties). 

Input parameters section has 3 parts

#### 1. Parameter Name
   A name with which the parameter can be referenced

#### 2. Data Type
   Every input parameter should have a type associated to it. Specifying the type converts the value of that parameter to the corresponding type. Currently functions support all the primitive types such as Boolean, DateTime, Double, Integer and String.

   | Data type | Sample value | 
|----------|---------------|
| Boolean | True | N/A |
| DateTime | Feb,22,2024 4:44PM |
| Double | 0.0 |
| Integet | 0 |
| String | "Hello" |

#### 3. Default Value
   Every parameter requires a default value which will be used during "Function Evaluation" or if there is an issue with the function invocation. 

   In the below sample, **_number1** and **_number2** are the 2 defined parameters with its corrsponding type and default value. Both these parameters should be passed to the function at the time of invocation. 
   ![image](https://github.com/MicrosoftDocs/dynamics-365-fraud-protection-pr/assets/116034304/9775bbfe-c31e-4b93-9f8c-17f2c7d8d9a9)


### Output Properties 
The return value of a function can be defined through output properties. The Output Properties section will have the FQL logic to return a value of the function. These properties can then be accessed from within other functions, rules, velocities, post decision action rules and routing rules by invoking the function. A function can have up to 30 output properties. 

Output Properties section has 4 parts

#### 1. Property Description
   A description of the property which will be helpful for the caller. Intellisense will be able to show the property description if it was defined. Also, the description is optional. 

#### 2. Data Type
   The data type of the value that is returned from this property. Specifying the type converts the retrun value to that corresponding type. Currently functions support all the primitive types such as Boolean, DateTime, Double, Integer and String.

When errors are encountered either before or after the evaluation of the output property i.e. if the output property is deleted or if the caller of the function calls it with a different parameter type than the expected type, the default value of the data type will be returned from the function as the result.

#### 3. Default Value

   The default value is very important as this value gets returned as the result of a function whenever an exception is encountered during the evaluation of the property. Some examples are division by 0 and Null Reference exceptions.

#### 4. Code Editor to Return a Value

   The code editor is used to return a value from the function. 

   In the sample below, The **MyFunction** function has 2 output properties **calculate_Sum** and **Call_WeatherService** defined with its corresponding description, data type and default value. The **Calculate_Sum** uses the input parameters to retrun a value and the **Call_weatherService** makes a call to an external service to return a value. To learn about invoking a function, see [Invoke functions from resources](Functions.md#invoke-functions-from-resources) and [Function inheritance ](Functions.md#function-inheritance) sections later in this docuemnt. 

   ![image](https://github.com/MicrosoftDocs/dynamics-365-fraud-protection-pr/assets/116034304/648f1bb4-948c-4fa4-a22b-a1c61c8aeac6)

   There are different ways to return an output value

   1. Input parameters defined within a function can be used to return values
   
      Example of output property returning an input parameter as the retrun value. For more information on how to define input parameters, see the [Input Parameters](functions.md#input-parameters) section earlier in this article.
   
       ```FraudProtectionLanguage
       RETURN _number1 + _number2
       ```
   1. Any attributes that are sent in the API request for the assessment, including custom data. You can access these attributes with the @ operator. For example, @"salesTax".
     
      Example of function using request attributes:
       ```FraudProtectionLanguage
       RETURN @"salesTax"
       ```
   2. The scores that are generated from Fraud Protection's artificial intelligence models. For example, @"riskscore".
      
      Example of function using riskscore:
       ```FraudProtectionLanguage
       LET $a = Model.Risk().Score
       RETURN 20
       ```
   3. Lists which you have uploaded to Fraud Protection. For more information on how to upload lists, see [Manage lists](lists.md).
      
      Example of function using list:
       ```FraudProtectionLanguage
       RETURN Lookup("Country_Score", "Country", "US", "ScoreCutOff")
       ```
   4. Velocities which you have defined in Fraud Protection. For more information, see [Perform velocity checks](velocities.md).
      
      Example of function using velocity:
       ```FraudProtectionLanguage
       RETURN Velocity.IPs_Per_User(@"deviceContext.ipAddress", 30s)
       ```
   5. External calls which you have created in Fraud Protection. For more information, see [External calls](external-calls.md).
   
      Example of function using External calls:
       ```FraudProtectionLanguage
       RETURN External.weather("Seattle").id
       ```
   6. External assessments which you have created in Fraud Protection. For more information, see [External Assessments](external-assessments.md).
      
      Example of a function invoking external assessment:
       ```FraudProtectionLanguage
       LET $result = Assessments.myAssessment.Evaluate($baseInput = @@)
       RETURN $result.ToStr()
       ```
   
   
   8. Access function within functions
      
      Example of a function invoking another function:
       ```FraudProtectionLanguage
       RETURN Functions.MyFunction(5,6).Calculat_Sum
       ```

## Create a function

1. In the [Fraud Protection portal](https://dfp.microsoft.com/), from the left navigation, select **Functions**, and then select **New Function**.

    Fraud Protection creates a draft function that is visible only to you (the creator). Note that all changes that you make to the draft are automatically saved.

2. To define a new function from scratch, see the [Define a Function](functions.md#define-a-function) section earlier in this article.

3. To publish the function, select **Publish**.
4. In the confirmation dialog box, you can change the name and description. When you're ready, select **Publish**.

> [!NOTE]
> After the function is published, the function is visible to all users. The function can then be invoked within other functions, rules, velocities, post-decision rules and routing rules. 

For information about how to use your functions within other resources like functions, rules, velocities, post decision action and routing rules see the [Invoke function from resources](Functions.md#invoke-function-from-resources) section later in this article.

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

When the evaluation pane is open, you can see the list of output properties with its result. This will help you to understand if you are returning the correct values for the functions. 

## Invoke functions from resources
The published functions can be invoked from resources such as rules, velocities, post-decision actions, and routing rules. All the output properties defined within a function can be accessed by invoking the function. The values can then be used for decision making. 

### Invoking functions from Rules 
Functions can be invoked from any rule (within any assessment) within the same environemnt or environments down the stack. To learn more about rules, see [Rules](rules.md).
```FraudProtectionLanguage
LET $sum = Functions.MyFunction(5,5).Calculate_Sum
RETURN Approve()
WHEN $sum > 5
```

### Invoking functions from Velocities 
Functions can be invoked from any velocity within the same environemnt or environemnts down the stack. To learn more about velocities, see [Perform velocity checks](velocities.md).
```FraudProtectionLanguage
SELECT DistinctCount(@"device.deviceContextId") AS Devices_Per_IP
FROM AccountLogin
WHEN Functions.MyFunction(5,5).Calculate_Sum > 5
GROUPBY @"device.ipAddress"
```

### Invoking functions from Post Decision Rules
Functions can be invoked from any post-decision action rule (within any assessment) within the same environemnt or environments down the stack. To learn more about post decision action rules, see [Post decision Action Rules](post-decision-action-rule.md).
```FraudProtectionLanguage
DO SetResponse()
WHEN Functions.MyFunction(2,3).Calculate_Sum == 5
```

### Invoking functions from Routing Rules 
Functions can be invoked from any routing rules within the same environemnt or environemnts down the stack. To learn more about routing rules, see [Case Management](case-management-overview.md).
```FraudProtectionLanguage
ROUTETO Queue("General Queue")
WHEN Functions.MyFunction(5,5).Calculate_Sum > 5
```

## Function inheritance 
Functions can be invoked within the same environment and from environments down the stack. The invocation syntax depends on where the function exists and from where it is invoked. The below are the different ways to invoke functions within a multi hierarchy set up. 

### Invoking the functions created within the same environment

The below example shows invoking function from a rule where both the rule and the function exists in the same environment
```FraudProtectionLanguage
LET $sum = Functions.MyFunction(2,3).Calculate_Sum
RETURN Approve()
WHEN $sum > 5
```
### Invoking the functions created within root environment
The below example shows invoking a function that is created in the root from a child environment
```FraudProtectionLanguage
LET $sum = Functions.root.MyFunction(2,3).Calculate_Sum
RETURN Approve()
WHEN $sum > 5
```
### Invoking the functions created within the parent environment

The below example shows invoking a function from the immediate parent environemnt.
```FraudProtectionLanguage
LET $sum = Functions.parent.MyFunction(2,3).Calculate_Sum
RETURN Approve()
WHEN $sum > 5
```

### Invoking the functions created within any environment above the stack

The below example shows invoking a function that is created in an environment above the stack and inherited from a rule within a lower environment
```FraudProtectionLanguage
LET $sum = Functions.environment["environmentid"].MyFunction(2,3).Calculate_Sum
RETURN Approve()
WHEN $sum > 5
```
## Function and resource limits

Microsoft Dynamics 365 has a limit on the numbers of functions that can be created per environment and the resources that can be referenced within a function. The below are the limits

  | Resource | Limit | 
|----------|---------------|
| Maximum number of functions that can be published within an environemnt | 30 |
| Maximum number of output properties that can exists within a function | 30 |
| Maximum number of velocilties that a function can reference | 15 |
| Maximum number of external calls that a function can reference |2 |
| Maximum number lists that a function can reference | 5 |
| Maximum number of unique external assessments that a function can reference | 2​ |
| Maximum number of functions that a rule can invoke | 10 |​
| Maximum number of functions that a routing rule can invoke | 10 |
| Maximum number of functions that a post decision action can invoke | 10 |
| Maximum number of resources that a velocity can invoke | 10 |





​



