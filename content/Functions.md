
# Functions



## Defining a Function: Quick start guide

Functions consist of Input parameters and output properties. 

### Input Parameters 

Functions can define parametrs which can be passed to the function at the time of invocation. The input parameters are defined in the function defenition. The number of parameters passed into the function at invocation should exactly match the number of parameters defined for this function. Input parametrs are optional and the defined parameters can be used within the Output properties to return a value. For more information, see the [Output Properties](output-properties.md). 

Input parameter have 3 parts

#### Parameter Name
A name with which the parameter can be referenced

#### Data Type
Each parameter should have a type associated to it. Specifying the type converts the value of that parameter to the corresponding type. Currently functions support all the primitive data types such as integer, string, docuble, boolean and dateTime

#### Default Value
Each parameters requires a default value which will be used during "Function Evaluation" or if there is an issue with the function invocation. 

![image](https://github.com/MicrosoftDocs/dynamics-365-fraud-protection-pr/assets/116034304/9775bbfe-c31e-4b93-9f8c-17f2c7d8d9a9)


### Output Proprties 

#### Property Description
A description of the property which will be helpful for the caller. Intellisense will be able to show the property description if it was defined. Also, the description is optional. 

#### Data Type
The data type of the value that is returned from this property. Specifying the type converts the retrun value of that corresponding type. Currently we can return all the primitive data types such as integer, string, docuble, boolean and dateTime

#### Default Value
#### Code Editor to Return a Value

![image](https://github.com/MicrosoftDocs/dynamics-365-fraud-protection-pr/assets/116034304/fb128994-5f05-4af4-9b34-575fe5e813bb)

```FraudProtectionLanguage
RETURN <Value>
```
The RETURN statement is used to return a value from the function. 
Any of the below can be accessed within Code Editor to return a value

1. Input parameters defined within a function can be used to return values

   Example of output property returning an input parameter as the retrun value. For more information on how to define input parameters, see the [Input Parameters](functions.md#input-parameters) section earlier in this article.

    ```FraudProtectionLanguage
    RETURN _number1 + _number2
    ```
1. Any attributes that are sent in the API request for the assessment, including custom data. You can access these attributes with the @ operator. For example, @"salesTax"".
  
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
    RETURN Velocity.IPs_Per_User(@"deviceContext.ipAddress",30s)
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

1. In the [Fraud Protection portal](https://dfp.microsoft.com/), in the left navigation, select **Functions**, and then select **New Function**.

    Fraud Protection creates a draft function that is visible only to you (the creator). Note that all changes that you make to the draft are automatically saved.

2. To define a new function from scratch, see the [Define a Function](functions.md#define-a-function) section earlier in this article.

3. To publish the function, select **Publish**.
4. In the confirmation dialog box, you can change the name and description. When you're ready, select **Publish**.

> [!NOTE]
> After the function is published, the function is visible to all users. The function can then be invoked within other functions, rules, velocities, post decision rules and routing rules. 

For information about how to use your functions within other resources like functions, rules, velocities, popst decision action and routing rules see the [Invoke a Function from resources](Functions.md#invoke-a-function-from-resources) section later in this article.

### Understand the Sample pane

When you create or edit a function, the **Sample** pane appears on the right side of the page.

- Functions are not tied on assessments. The sample payload is just a helping guide for users that shows all the event properties that can be referenced in your functions. Select the event type in the **Event** field at the top of the pane.
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

## Invoking Functions from resources
Functions which are created can be invoked from resources such as rules, velocities, post decision actions and routing rules. All the output properties defined within a function can be accessed by invoking the function. The values can then be used for decision making. 
### Invoke functions from Rules 

```FraudProtectionLanguage
LET $sum = Functions.MyFunction(5,5).Calculate_Sum
RETURN Approve()
WHEN $sum > 5
```

### Invoke functions from Velocities 

```FraudProtectionLanguage
SELECT DistinctCount(@"device.deviceContextId") AS Devices_Per_IP
FROM AccountLogin
WHEN Functions.MyFunction(5,5).Calculate_Sum > 5
GROUPBY @"device.ipAddress"
```

### Invoke functions from Post Decision Rules

```FraudProtectionLanguage
DO SetResponse()
WHEN Functions.MyFunction(2,3).Calculate_Sum == 5
```

### Invoke functions from Routing Rules 

```FraudProtectionLanguage
ROUTETO Queue("General Queue")
WHEN Functions.MyFunction(5,5).Calculate_Sum > 5
```

## Function inheritance 
Functions can be invoked within the same environemnt and from environments down the stack. The invocation syntax depends on where the function exists and from where it is invoked. The below are the different ways to invoke functions within a multi hierarchy set up. 

### Invoking the functions created within the same environment

The below example shows invoking function from a rule where both the rule and the function exists ins the same environment
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

The below example shows invoking a function from the immediate parent environemnt. Here parent means the environment immediate environment above you
```FraudProtectionLanguage
LET $sum = Functions.parent.MyFunction(2,3).Calculate_Sum
RETURN Approve()
WHEN $sum > 5
```

### Invoking the functions created within any environment above the stack

The below example shows invoking a function that is created an environment above the stack and inherited from any rule within a lower environment
```FraudProtectionLanguage
LET $sum = Functions.environment["environmentid"].MyFunction(2,3).Calculate_Sum
RETURN Approve()
WHEN $sum > 5
```
## Function and resource limits



