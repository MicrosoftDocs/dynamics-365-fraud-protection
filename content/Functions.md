
# Functions



## Defining a Function: Quick start guide

Functions consist of Input parameters and output properties. 

### Input Parameters 

Functions can define inputs which camn be passed at the time of invocation. The input is defined using parameters which are called "Input Parameters" are defined in the function defenition.Each input parameter that the user defines has 3 parts

#### Parameter Name
#### Data Type
#### Default Value

### Output Proprties 

#### Property Description
#### Data Type
#### Default Value
#### Code Editor to Return a Value

```FraudProtectionLanguage
RETURN <Value>
```
The RETURN statement is used to return a value from the function. 
Any of the below can be accessed within Code Editor to return a value
-	Any attributes that are sent in the API request for the assessment, including custom data. You can access these attributes with the @ operator. For example, @"user.userId".
  
  Example of function using request attributes:
  
  ```FraudProtectionLanguage
  RETURN @"salesTax"
  ```
-	The scores that are generated from Fraud Protection's artificial intelligence models. For example, @"riskscore".
  Example of function using riskscore:

  ```FraudProtectionLanguage
  LET $a = Model.Risk().Score
  RETURN 20
  ```
-	Lists which you have uploaded to Fraud Protection. For more information on how to upload lists, see [Manage lists](lists.md). 
  Example of function using list:
  ```FraudProtectionLanguage
  RETURN Lookup("Country_Score", "Country", "US", "ScoreCutOff")
  ```
-	Velocities which you have defined in Fraud Protection. For more information, see [Perform velocity checks](velocities.md).
  Example of function using velocity:

  ```FraudProtectionLanguage
  RETURN Velocity.IPs_Per_User(@"deviceContext.ipAddress",30s)
  ```
-	External calls which you have created in Fraud Protection. For more information, see [External calls](external-calls.md).

  Example of function using External calls:
  ```FraudProtectionLanguage
  RETURN External.weather("Seattle").id
  ```

- External assessments which you have created in Fraud Protection. For more information, see [External Assessments](external-assessments.md). 
  Example of function using External Assessments:
- Please refer to the [Language reference guide](fpl-lang-ref.md) for list of all functions available within DFP. Decision functions , Action functions and Observation functions are not allowed within functions. Everything from Model functions until Global variable functions can be used within Functions. 
  Example of function using Model Functions:
-Access function within functions
  Example of function invoking other Functions:

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

## Function inheritance 

## Invoke a Function from resources

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



