---
author: zhuoche
description: This topic explains the rules and lists capability of Dynamics 365 Fraud Protection account protection.
ms.author: v-davido
ms.service: fraud-protection
ms.date: 02/11/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin


title: Account protection Scorecard
---

# Manage Account Protection Rules and Lists

## Rules
You can use lists and rules to help automate your account protection decisioning. Rules shape real-time decision making by accepting, rejecting, challenging, and reviewing account protection events based on the conditions and risk score thresholds that you select. The rules use lists of data that you create that are relevant to your business. These capabilities help you define the parameters that are right for your business to screen for risky account protection events. They also help you enforce various policies, such as geofencing. These capabilities are designed to help you manage the trade-offs that are inherent when you must prevent fraud. 

Common operations associated with a rule are:
- **New rule**: create a new rule.
- **Rename**: change the descriptive name of a rule.
- **Activate/deactivate**: determine if the rule is affecting assessment API. (link)
- **Delete**: remove a rule.
- **Move up/move down**: change the execution order of rule.

The common components of a rule are:
- **Condition**: Conditions can be used to group related rules together. The rules will only be executed if the condition evaluates to true. 
- **Clause**: Clauses are the components that return a decision based on certain conditions. Clauses are executed in sequential order. Some clauses are run prior to model execution, before any score has been generated. Some clauses are run after a score has been generated.
- **Payload**: shows a sample of what the payload for account protection API look like for a given event. 

Examples of a rule (code example is still in progress) 

Condition should start with 'WHEN'. It can accept any valid expression if its result is a boolean.

Sample condition:
```
WHEN Geo.CountryCode(@ip) == "BR"

WHEN @id == 100 

WHEN @count < 10 
```
  
Example clause: throw a challenge if bot score is between 400 to 900:

```
Return Challenge(type = “sms”, reason = “bot score”) 
WHEN @modelData < 900 AND @modelData > 400 
```
     
Example clause: approve all users whose IP is in a list:
```
Return Approve(reason = "") 
WHEN IN (@ip, "Dictionary://mylist?KeyValueField = IP)
```

## Lists 

You can upload any number of lists to suit your specific business needs. After these lists are uploaded, you can use these lists within your rules to achieve the business results that you need. To upload a list, select the **lists** menu under Account protection.

Each list that you upload comprises a collection of entities (a collection of data of one or more columns) that you have authored offline and want to screen for, such as high-risk countries. After you upload a list, you can give it a meaningful name and reference it in any rule.

An example of list usage will be decision based on whether payload data is in or not in a list.

Common operation associated with the list are:
- **New list**: upload a new file (.csv with headers) that has been created offline.
- **Download**: save a list as a file to local machine.
- **Edit**: update an existing list (by updating the list offline).

## Related topics: (link tbd) 
- Account protection overview 
- View Account protection schemas 
- Account protection scorecard 

## Reference:  
- Return statement 
```
Approve (reason) 
Reject (reason) 
Challenge (type, reason) 
Review (reason) 
```
- When: Must evaluate to a boolean 
- Logical operators 

```
AND (&&)
OR(||)
-
==
@
IN
```
- String Operators 

```
StartsWith
EndsWith
Contains
```
- Math Operators
```
Math.Min
Math.Max
Math.Average
```
- Geo Operators 
```
Geo.RegionCode
Geo.Region
Geo.CountryCode
Geo.Country
Geo.City
Geo.PostalCode
Geo.Isp
Geo.MarketCode
```
- How to use lists 
```
IN (@ip, "Dictionary://mylist?KeyValueField = IP)      
MAP (@currentIP, "Dictionary://mylist?KeyValueField = IP
```
