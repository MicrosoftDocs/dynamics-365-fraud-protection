---
author: v-davido
description: This topic outlines the requred schema for the loss prevention API.
ms.author: v-davido
ms.service: fraud-protection
ms.date: 01/14/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin

title: View loss prevention schema
---

# View loss prevention schema

This topic outlines the schema for the loss prevention API.

Note the following formatting guidelines throughout:

- The files are in CSV UTF-8 (comma delimited) format (\*.csv).
- The maximum file size is 10 gigabytes (GB).
- The **DateTime** columns are in ISO 8601 format. For example, **DateTime.UtcNow.ToString("o")** might have the result **"2019-03-14T20:18:11.254Z"**.
- The decimal precision is two decimal places.
- The following characters are escaped in all columns: commas, new line characters, and multiline characters.

## Transaction Staging

| Attribute | Type | Description |
| --- | --- | --- |
| AMOUNTPOSTEDTOACCOUNT | numeric | Amount posted to account for GL posting. |
| BATCHID | bigint | Not sure. May be deprecated. |
| COSTAMOUNT | numeric | Cost for items. |
| CREATEDOFFLINE | int | Was created offline w/o db connection. |
| COSTAMOUNT | numeric | Cost for items. |



## table test

| AMOUNTPOSTE+A2:C54DTOACCOUNT    | [numeric](32 6) NOT NULL  | Amount posted to account for GL posting                                                                                                                      |
|---------------------------------|---------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| BATCHID                         | [bigint] NOT NULL         | Not sure. May be deprecated                                                                                                                                  |
| CHANNELREFERENCEID              | [nvarchar](50) NOT NULL   | Deprecated?                                                                                                                                                  |
| COMMENT_                        | [nvarchar](60) NOT NULL   | Txn level comment                                                                                                                                            |
| COSTAMOUNT                      | [numeric](32 6) NOT NULL  | Cost for items                                                                                                                                               |
| CREATEDOFFLINE                  | [int] NOT NULL            | Was created offline without channel db connection?                                                                                                           |
| CURRENCY                        | [nvarchar](3) NOT NULL    | Currency                                                                                                                                                     |
| CUSTOMERACCOUNT                 | [nvarchar](38) NOT NULL   | Account number                                                                                                                                               |
| CUSTOMERDISCOUNTAMOUNT          | [numeric](32 6) NOT NULL  | Discount mapped to customer, automatic for that customer                                                                                                     |
| DATAAREAID                      | [nvarchar](4) NOT NULL    |                                                                                                                                                              |
| DEFINITIONGROUP                 | [nvarchar](60) NOT NULL   |                                                                                                                                                              |
| DELIVERYMODE                    | [nvarchar](10) NOT NULL   | Mode of delivery if not cash and carry                                                                                                                       |
| DISCOUNTAMOUNT                  | [numeric](32 6) NOT NULL  | Discount amount                                                                                                                                              |
| DISCOUNTAMOUNTWITHOUTTAX        | [numeric](32 6) NOT NULL  | Discount amount without tax                                                                                                                                  |
| EXCHANGERATE                    | [numeric](32 16) NOT NULL | Exchange rate if paying with non-store currency                                                                                                              |
| EXECUTIONID                     | [nvarchar](90) NOT NULL   |                                                                                                                                                              |
| GROSSAMOUNT                     | [numeric](32 6) NOT NULL  | Total due before discounts(?)                                                                                                                                |
| INCOMEEXPENSEAMOUNT             | [numeric](32 6) NOT NULL  | If transaction is drawer related(add/remove money and not an actual transaction)                                                                             |
| INFOCODEDISCOUNTGROUP           | [nvarchar](10) NOT NULL   | If discount is applied and info code is prompted to request why                                                                                              |
| INVOICEID                       | [nvarchar](20) NOT NULL   | Related to payments on customer accounts, invoice they are making a payment against                                                                          |
| ISSELECTED                      | [int] NOT NULL            |                                                                                                                                                              |
| ITEMSPOSTED                     | [int] NOT NULL            | Delivery address effectivity- date when address becomes invalid                                                                                              |
| LOGISTICPOSTALADDRESSVALIDTO    | [datetime] NOT NULL       | ID for customer address. They may have multiple                                                                                                              |
| LOGISTICSLOCATIONID             | [nvarchar](30) NOT NULL   | Delivery address effectivity- date when address valid                                                                                                        |
| LOGISTICSPOSTALADDRESSVALIDFROM | [datetime] NOT NULL       | City                                                                                                                                                         |
| LOGISTICSPOSTALCITY             | [nvarchar](60) NOT NULL   | County                                                                                                                                                       |
| LOGISTICSPOSTALCOUNTY           | [nvarchar](10) NOT NULL   | State                                                                                                                                                        |
| LOGISTICSPOSTALSTATE            | [nvarchar](10) NOT NULL   | Street                                                                                                                                                       |
| LOGISTICSPOSTALSTREET           | [nvarchar](250) NOT NULL  | Zip                                                                                                                                                          |
| LOGISTICSPOSTALZIPCODE          | [nvarchar](10) NOT NULL   | Loyalty card number                                                                                                                                          |
| LOYALTYCARDID                   | [nvarchar](30) NOT NULL   | Amount after taxes and discounts                                                                                                                             |
| NETAMOUNT                       | [numeric](32 6) NOT NULL  | price before discounts                                                                                                                                       |
| NETPRICE                        | [numeric](32 6) NOT NULL  | # of lines on the transaction                                                                                                                                |
| OPERATINGUNITNUMBER             | [nvarchar](30) NOT NULL   |                                                                                                                                                              |
| PARTITION                       | [nvarchar](20) NOT NULL   |                                                                                                                                                              |
| PAYMENTAMOUNT                   | [numeric](32 6) NOT NULL  | Payment amount                                                                                                                                               |
| POSTASSHIPMENT                  | [int] NOT NULL            | ?                                                                                                                                                            |
| REFUNDRECEIPTID                 | [nvarchar](18) NOT NULL   | if refund, receipt id for original transaction                                                                                                               |
| RETAILNCREXPORTED               | [int] NOT NULL            |                                                                                                                                                              |
| RRECEIPTID                      | [nvarchar](18) NOT NULL   | Receipt number, different from transaction number                                                                                                            |
| SALEISRETURNSALE                | [int] NOT NULL            | If sale is return                                                                                                                                            |
| SALESINVOICEAMOUNT              | [numeric](32 6) NOT NULL  | Amount for sales invoice if  customer is picking up a few items from an order                                                                                |
| SALESORDERAMOUNT                | [numeric](32 6) NOT NULL  | total amount for customer orders(which are different from cash and carry because they have shipping details)                                                 |
| SALESORDERID                    | [nvarchar](20) NOT NULL   | Order number(for those with shipping details                                                                                                                 |
| SALESPAYMENTDIFFERENCE          | [numeric](32 6) NOT NULL  | ?                                                                                                                                                            |
| SHIFT                           | [nvarchar](10) NOT NULL   | Shift is a set of transactions throughout the day for which cash and sales activity is calculated. Useful for determining how much cash should be in the til |
| SHIPPINGDATEREQUESTED           | [datetime] NOT NULL       | Date when goods on customer order should be shipped                                                                                                          |
| SITEID                          | [nvarchar](10) NOT NULL   | Typically used for retail  stores to organize by region such as "Northwest US stores"                                                                        |
| STAFF                           | [nvarchar](25) NOT NULL   | POS user ID                                                                                                                                                  |
| SYNCSTARTDATETIME               | [datetime] NOT NULL       |                                                                                                                                                              |
| TAXCALCULATIONTYPE              | [int] NOT NULL            | If tax is based on Store, Customer, Destination                                                                                                              |
| TERMINAL                        | [nvarchar](10) NOT NULL   |                                                                                                                                                              |
| TOACCOUNT                       | [int] NOT NULL            | How much is being charged to customer's account                                                                                                              |
| TOTALDISCOUNTAMOUNT             | [numeric](32 6) NOT NULL  | Amount of discount applied to transaction total                                                                                                              |
| TOTALMANUALDISCOUNTAMOUNT       | [numeric](32 6) NOT NULL  | If manually applied vs automatic total discount                                                                                                              |
| TOTALMANUALDISCOUNTPERCENTAGE   | [numeric](32 6) NOT NULL  | Percentage of manually applied total discount                                                                                                                |
| TRANSACTIONDATE                 | [datetime] NOT NULL       | Date                                                                                                                                                         |
| TRANSACTIONNUMBER               | [nvarchar](44) NOT NULL   | Transaction ID                                                                                                                                               |
| TRANSACTIONSTATUS               | [int] NOT NULL            | Typically "posted"                                                                                                                                           |
| TRANSACTIONTIME                 | [int] NOT NULL            | Time                                                                                                                                                         |
| TRANSACTIONTYPE                 | [int] NOT NULL            | Cash and carry vs order                                                                                                                                      |
| TRANSFERSTATUS                  | [int] NOT NULL            |                                                                                                                                                              |
| WAREHOUSE                       | [nvarchar](10) NOT NULL   | Maps to Store 1:1                                                                                                                                            |





## end table test

## Transaction Sales Line Staging

| Attribute | Type | Description |
| --- | --- | --- |
| trackingId | string | The identifier of the Signup event. |

## Transaction Payment Line Staging

| Attribute | Type | Description |
| --- | --- | --- |
| trackingId | string | The identifier of the Signup event. |

## Payment Method

| Attribute | Type | Description |
| --- | --- | --- |
| trackingId | string | The identifier of the Signup event. |

## Transaction Staging

| Attribute | Type | Description |
| --- | --- | --- |
| trackingId | string | The identifier of the Signup event. |


