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



## table test -- start

## TransactionStaging

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

## TransactionSalesLineStaging

| Attribute                       | Type                      | Description                                                                                        |
|---------------------------------|---------------------------|----------------------------------------------------------------------------------------------------|
| BARCODE                         | [nvarchar](80) NOT NULL   | Bar code that was scanned                                                                          |
| CASHDISCOUNTAMOUNT              | [numeric](32 6) NOT NULL  | Amount of cash disount, if applicable                                                              |
| CATEGORYHIERARCHYNAME           | [nvarchar](128) NOT NULL  | Categrory hierarchy used to organize products                                                      |
| CATEGORYNAME                    | [nvarchar](254) NOT NULL  | Name of the product category                                                                       |
| CHANNELLISTINGID                | [nvarchar](50) NOT NULL   | ?                                                                                                  |
| COSTAMOUNT                      | [numeric](32 6) NOT NULL  | Product cost                                                                                       |
| CURRENCY                        | [nvarchar](3) NOT NULL    | Currency paid?                                                                                     |
| CUSTOMERACCOUNT                 | [nvarchar](38) NOT NULL   | Customer account number                                                                            |
| CUSTOMERDISCOUNT                | [numeric](32 6) NOT NULL  | Customer discount                                                                                  |
| CUSTOMERINVOICEDISCOUNTAMOUNT   | [numeric](32 6) NOT NULL  | ?                                                                                                  |
| DATAAREAID                      | [nvarchar](4) NOT NULL    |                                                                                                    |
| DEFINITIONGROUP                 | [nvarchar](60) NOT NULL   |                                                                                                    |
| DISCOUNTAMOUNTFORPRINTING       | [numeric](32 6) NOT NULL  | ?                                                                                                  |
| DISCOUNTAMOUNTWITHOUTTAX        | [numeric](32 6) NOT NULL  |                                                                                                    |
| ELECTRONICDELIVERYEMAIL         | [nvarchar](80) NOT NULL   | Email address                                                                                      |
| EXECUTIONID                     | [nvarchar](90) NOT NULL   |                                                                                                    |
| GIFTCARD                        | [int] NOT NULL            | Gift card number                                                                                   |
| INVENTORYSTATUS                 | [int] NOT NULL            | ?                                                                                                  |
| ISLINEDISCOUNTED                | [int] NOT NULL            | Is the txn line discounted                                                                         |
| ISLINKEDPRODUCTNOTORIGINAL      | [int] NOT NULL            | If linked item was changed                                                                         |
| ISORIGINALOFLINKEDPRODUCTLIST   | [int] NOT NULL            | ?                                                                                                  |
| ISPRICECHANGE                   | [int] NOT NULL            | If price was changed manually                                                                      |
| ISRETURNNOSALE                  | [int] NOT NULL            | ?                                                                                                  |
| ISSCALEPRODUCT                  | [int] NOT NULL            | Is the connected scale used to get Qty                                                             |
| ISSELECTED                      | [int] NOT NULL            |                                                                                                    |
| ISWEIGHTMANUALLYENTERED         | [int] NOT NULL            | If scale is not connected, cashier can enter weight manually                                       |
| ISWEIGHTPRODUCT                 | [int] NOT NULL            | Same as scale product?                                                                             |
| ITEMCOLOR                       | [nvarchar](25) NOT NULL   | Color                                                                                              |
| ITEMCONFIGID                    | [nvarchar](50) NOT NULL   | Configuration ID for kits                                                                          |
| ITEMID                          | [nvarchar](20) NOT NULL   | Product ID                                                                                         |
| ITEMRELATION                    | [nvarchar](20) NOT NULL   | ?                                                                                                  |
| ITEMSALESTAXGROUP               | [nvarchar](10) NOT NULL   | Effective sales tax group for the item                                                             |
| ITEMSIZE                        | [nvarchar](10) NOT NULL   | Size                                                                                               |
| ITEMSTYLE                       | [nvarchar](10) NOT NULL   | Style, like color and size is another product dimension                                            |
| KEYBOARDPRODUCTENTRY            | [int] NOT NULL            | If product ID was keyed in                                                                         |
| LINEDISCOUNT                    | [numeric](32 6) NOT NULL  | Discount on line                                                                                   |
| LINEMANUALDISCOUNTAMOUNT        | [numeric](32 6) NOT NULL  | If discount was manually entered, the amount                                                       |
| LINEMANUALDISCOUNTPERCENTAGE    | [numeric](32 6) NOT NULL  | If manual percentage discount was applied, the percentage                                          |
| LINENUMBER                      | [numeric](32 16) NOT NULL | Line number on the transaction                                                                     |
| LINEPERCENTAGEDISCOUNT          | [numeric](32 6) NOT NULL  | Automatic percentage discount amount                                                               |
| LOGISTICLOCATIONID              | [nvarchar](30) NOT NULL   | ?                                                                                                  |
| LOGISTICSPOSTALADDRESSVALIDFROM | [datetime] NOT NULL       | ?                                                                                                  |
| LOTID                           | [nvarchar](20) NOT NULL   | Not used                                                                                           |
| MODEOFDELIVERY                  | [nvarchar](10) NOT NULL   | Method of delivery to the customer                                                                 |
| NETAMOUNT                       | [numeric](32 6) NOT NULL  | Net amount for transaction                                                                         |
| NETAMOUNTINCLUSIVETAX           | [numeric](32 6) NOT NULL  | Net amount with tax included                                                                       |
| NETPRICE                        | [numeric](32 6) NOT NULL  | Net price for the line before discounts                                                            |
| OFFERNUMBER                     | [nvarchar](40) NOT NULL   | ?                                                                                                  |
| OPERATINGUNITNUMBER             | [nvarchar](30) NOT NULL   | Part of the reference data that comprises a store                                                  |
| ORIGINALITEMSALESTAXGROUP       | [nvarchar](10) NOT NULL   | If tax is overridden, tracks what the original tax amt was.                                        |
| ORIGINALPRICE                   | [numeric](32 6) NOT NULL  | Product price without sale pricing applied                                                         |
| ORIGINALSALESTAXGROUP           | [nvarchar](10) NOT NULL   | Original sales tax group for the transaction                                                       |
| PARTITION                       | [nvarchar](20) NOT NULL   |                                                                                                    |
| PERIODICDISCOUNTAMOUNT          | [numeric](32 6) NOT NULL  | Discount amount for periodic discount(kind of like happy hour)                                     |
| PERIODICDISCOUNTGROUP           | [nvarchar](10) NOT NULL   | Periodic discount group                                                                            |
| PERIODICDISCOUNTPERCENTAGE      | [numeric](32 6) NOT NULL  | Periodic discount percentage                                                                       |
| PRICE                           | [numeric](32 6) NOT NULL  | Price (I believe with discounts)                                                                   |
| PRICEGROUPS                     | [nvarchar](10) NOT NULL   | Price group that products and customers belong to.                                                 |
| PRICEINBARCODE                  | [int] NOT NULL            | If price embedded bar code was scanned                                                             |
| PRODUCTSCANNED                  | [int] NOT NULL            | If the product was scanned                                                                         |
| QUANTITY                        | [numeric](32 6) NOT NULL  | Quantity                                                                                           |
| REASONCODEDISCOUNT              | [numeric](32 6) NOT NULL  | If a discount was applied, reason codes can be configured to prompt the cashier to select a reason |
| RECEIPTNUMBER                   | [nvarchar](18) NOT NULL   | Receipt number                                                                                     |
| REQUESTEDRECEIPTDATE            | [datetime] NOT NULL       | For customer orders, date that the customer requests arrival/pickup                                |
| REQUESTEDSHIPDATE               | [datetime] NOT NULL       | Requested date for order to ship                                                                   |
| RETAILEMAILADDRESSCONTENT       | [nvarchar](400) NOT NULL  | email address for receipt                                                                          |
| RETURNLINENUMBER                | [numeric](32 16) NOT NULL | Line number from original transaction when returning from journal                                  |
| RETURNOPERATINGUNITNUMBER       | [nvarchar](30) NOT NULL   | Store where the return is being processed                                                          |
| RETURNQUANTITY                  | [numeric](32 6) NOT NULL  | Quantity being returned.                                                                           |
| RETURNTERMINAL                  | [nvarchar](10) NOT NULL   | Terminal where txn is being returned.                                                              |
| RETURNTRANSACTIONNUMBER         | [nvarchar](44) NOT NULL   | Original transaction number when returning from receipt/journal                                    |
| RFIDTAGID                       | [nvarchar](24) NOT NULL   |                                                                                                    |
| SALESTAXAMOUNT                  | [numeric](32 6) NOT NULL  | Amt of sales tax applied to the transaction                                                        |
| SALESTAXGROUP                   | [nvarchar](10) NOT NULL   | Effective sales tax group for the transaction                                                      |
| SECTIONNUMBER                   | [nvarchar](10) NOT NULL   | ?                                                                                                  |
| SERIALNUMBER                    | [nvarchar](20) NOT NULL   | Serial number for the product                                                                      |
| SHELFNUMBER                     | [nvarchar](10) NOT NULL   | Shelf number where the product is kept(not really used).                                           |
| SITEID                          | [nvarchar](10) NOT NULL   | Category to which store belongs (i.e. Pacific Northwest stores)                                    |
| SKIPREPORTS                     | [int] NOT NULL            |                                                                                                    |
| STANDARDNETPRICE                | [numeric](32 6) NOT NULL  | Like original price?                                                                               |
| SYNCSTARTDATETIME               | [datetime] NOT NULL       |                                                                                                    |
| TERMINAL                        | [nvarchar](10) NOT NULL   |                                                                                                    |
| TOTALDISCOUNT                   | [numeric](32 6) NOT NULL  | Amount of discount applied to order total.                                                         |
| TOTALDISCOUNTINFOCODELINENUM    | [numeric](32 16) NOT NULL | If prompted for info code when applying total discount, reason code is saved here                  |
| TOTALDISCOUNTPERCENTAGE         | [numeric](32 6) NOT NULL  | Discount percent applied to transaction total, if total discount by percent is used                |
| TRANSACTIONCODE                 | [int] NOT NULL            | ?                                                                                                  |
| TRANSACTIONNUMBER               | [nvarchar](44) NOT NULL   | Transaction number                                                                                 |
| TRANSACTIONSTATUS               | [int] NOT NULL            | Posted indicates that the statement has been completed(amounts have hit the GL in the back office) |
| TRANSFERSTATUS                  | [int] NOT NULL            |                                                                                                    |
| UNIT                            | [nvarchar](10) NOT NULL   | Ea., Pcs, Gallons etc.                                                                             |
| UNITPRICE                       | [numeric](32 6) NOT NULL  | Price per unit                                                                                     |
| UNITQUANTITY                    | [numeric](32 6) NOT NULL  | Quantity of unit sold (not sure how this is different from unit)                                   |
| VARIANTNUMBER                   | [nvarchar](10) NOT NULL   | ID for unit combination of color, size and style                                                   |
| WAREHOUSE                       | [nvarchar](10) NOT NULL   | Reference data for store. Indicates physical location of the goods.                                |
## PaymentLineStaging

| Attribute                        | Type                      | Description                                                     |
|----------------------------------|---------------------------|-----------------------------------------------------------------|
| ACCOUNTNUMBER                    | [nvarchar](30) NOT NULL   | Customer's account nubmer if named customer is on transaction   |
| AMOUNTINACCOUNTINGCURRENCY       | [numeric](32 6) NOT NULL  | Amount due for line                                             |
| AMOUNTINTENDEREDCURRENCY         | [numeric](32 6) NOT NULL  | amount tendered in currency (different if not store's currency) |
| AMOUNTTENDERED                   | [numeric](32 6) NOT NULL  | Amount paid(?)                                                  |
| AMOUNTTENDEREDADJUSTMENT         | [numeric](32 6) NOT NULL  |                                                                 |
| CARDNUMBER                       | [nvarchar](30) NOT NULL   | Truncated card no.                                              |
| CARDTYPEID                       | [nvarchar](10) NOT NULL   | Card name (AMEX, VISA, ETC)                                     |
| CREDITVOUCHERID                  | [nvarchar](30) NOT NULL   | If paid by voucher, the voucher number                          |
| CURRENCYCODE                     | [nvarchar](3) NOT NULL    | Currency paid                                                   |
| DATAAREAID                       | [nvarchar](4) NOT NULL    |                                                                 |
| DEFINITIONGROUP                  | [nvarchar](60) NOT NULL   |                                                                 |
| EXCHANGERATEINACCOUNTINGCURRENCY | [numeric](32 16) NOT NULL | Exchange rate                                                   |
| EXCHANGERATEINTENDEREDCURRENCY   | [numeric](32 16) NOT NULL | Exchange rate                                                   |
| EXECUTIONID                      | [nvarchar](90) NOT NULL   |                                                                 |
| GIFTCARDID                       | [nvarchar](30) NOT NULL   | Gift card number                                                |
| ISCHANGELINE                     | [int] NOT NULL            | If payment is due back to customer due to overpayment           |
| ISPREPAYMENT                     | [int] NOT NULL            | Is a deposit                                                    |
| ISSELECTED                       | [int] NOT NULL            |                                                                 |
| LINENUMBER                       | [numeric](32 16) NOT NULL | Payment line number                                             |
| LOYALTYCARDID                    | [nvarchar](30) NOT NULL   | If paying with loyalty points, the card number provided         |
| OPERATINGUNITNUMBER              | [nvarchar](30) NOT NULL   | Operating unit unique to store                                  |
| PARTITION                        | [nvarchar](20) NOT NULL   |                                                                 |
| QUANTITY                         | [numeric](32 6) NOT NULL  | ?                                                               |
| RECEIPTID                        | [nvarchar](18) NOT NULL   | Receipt ID. Different from Trasaction ID.                       |
| STAFF                            | [nvarchar](25) NOT NULL   | User ID                                                         |
| SYNCSTARTDATETIME                | [datetime] NOT NULL       |                                                                 |
| TENDERTYPE                       | [nvarchar](10) NOT NULL   | Type of tender paid                                             |
| TERMINAL                         | [nvarchar](10) NOT NULL   |                                                                 |
| TRANSACTIONNUMBER                | [nvarchar](44) NOT NULL   | Transaction number                                              |
| TRANSACTIONSTATUS                | [int] NOT NULL            | Status of payment line                                          |
| TRANSFERSTATUS                   | [int] NOT NULL            |                                                                 |
| VOIDSTATUS                       | [int] NOT NULL            | If a tender line was voided prior to tendering the transaction  |


## PaymentMethod

| Attribute           | Type                    | Description |
|---------------------|-------------------------|---------------------------------------------------------------|
| DEFAULTFUNCTION     | [int] NOT NULL          | TBD                                                           |
| NAME                | [nvarchar](60) NOT NULL | TBD                                                           |
| PAYMENTMETHODNUMBER | [nvarchar](10) NOT NULL | TBD                                                           |





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


