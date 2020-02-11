---
author: veganesa
description: This topic outlines the requred schema for the loss prevention feature.
ms.author: veganesa
ms.service: fraud-protection
ms.date: 02/11/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin

title: View loss prevention schema
---

# View loss prevention schema

This topic outlines the schemas used to define the data used in generating models and determining risk assessments. 

Note the following formatting guidelines throughout:

- The files are in CSV UTF-8 (comma delimited) format (\*.csv).
- The maximum file size is 10 gigabytes (GB).
- The **DateTime** columns are in ISO 8601 format. For example, **DateTime.UtcNow.ToString("o")** might have the result **"2019-03-14T20:18:11.254Z"**.
- The decimal precision is two decimal places.
- The following characters are escaped in all columns: commas, new line characters, and multiline characters.


## Transactions

| Field name           | Data type     | Description |
|---------------------|----------|-------------|
| AMOUNTPOSTEDTOACCOUNT    | numeric (32 6)  | Amount posted to account for GL posting                                                                                                                      |
| BATCHID                         | bigint         | Idenitifier for Batch or Shift                                                                                                                               |
| CHANNELREFERENCEID        | nvarchar (50)           | This field is not required                                                                                                                              |
| COMMENT                       | nvarchar (60)   | Transaction level comment                                                                                                                                            |
| COSTAMOUNT                      | numeric (32 6) NOT NULL  | Cost for items                                                                                                                                               |
| CREATEDOFFLINE                  | int            | Was created offline without channel db connection?                                                                                                           |
| CURRENCY                        | nvarchar (3)    | Currency                                                                                                                                                     |
| CUSTOMERACCOUNT                 | nvarchar (38) NOT NULL   | Account number                                                                                                                                               |
| CUSTOMERDISCOUNTAMOUNT          | numeric (32 6)  | Discount mapped to customer, automatic for that customer                                                                                                     |
| DATAAREAID                      | nvarchar (4) NOT NULL    | Identification legal entity in Finance & Operations                                                                                                                                                             |
| DEFINITIONGROUP                 | nvarchar (60)   | Fields added by the synchronization engine (DIFX) in Finance & Operations. They define the export sequence.                                                                                                                                                             |
| DELIVERYMODE                    | nvarchar (10)   | Mode of delivery if not cash and carry                                                                                                                       |
| DISCOUNTAMOUNT                  | numeric (32 6)  | Discount amount                                                                                                                                              |
| DISCOUNTAMOUNTWITHOUTTAX        | numeric (32 6)  | Discount amount without tax                                                                                                                                  |
| EXCHANGERATE                    | numeric (32 16) | Exchange rate if paying with non-store currency                                                                                                              |
| EXECUTIONID                     | nvarchar (90)   | Fields added by the synchronization engine (DIFX) in Finance & Operations. They define the export sequence.                                                                                                                                                             |
| GROSSAMOUNT                     | numeric (32 6)  | Total due before discounts(?)                                                                                                                                |
| INCOMEEXPENSEAMOUNT             | numeric (32 6)  | If transaction is drawer related(add/remove money and not an actual transaction)                                                                             |
| INFOCODEDISCOUNTGROUP           | nvarchar (10)   | If discount is applied and info code is prompted to request why                                                                                              |
| INVOICEID                       | nvarchar (20)   | Related to payments on customer accounts, invoice they are making a payment against                                                                          |
| ISSELECTED                      | int            | Fields added by the synchronization engine (DIFX) in Finance & Operations. They define the export sequence.                                                                                                                                                             |
| ITEMSPOSTED                     | int            | Delivery address effectivity- date when address becomes invalid                                                                                              |
| LOGISTICPOSTALADDRESSVALIDTO    | datetime       | ID for customer address. They may have multiple                                                                                                              |
| LOGISTICSLOCATIONID             | nvarchar (30)   | Delivery address effectivity- date when address valid                                                                                                        |
| LOGISTICSPOSTALADDRESSVALIDFROM | datetime       | City                                                                                                                                                         |
| LOGISTICSPOSTALCITY             | nvarchar (60)   | County                                                                                                                                                       |
| LOGISTICSPOSTALCOUNTY           | nvarchar (10)   | State                                                                                                                                                        |
| LOGISTICSPOSTALSTATE            | nvarchar (10)   | Street                                                                                                                                                       |
| LOGISTICSPOSTALSTREET           | nvarchar (250)  | Zip                                                                                                                                                          |
| LOGISTICSPOSTALZIPCODE          | nvarchar (10)   | Loyalty card number                                                                                                                                          |
| LOYALTYCARDID                   | nvarchar (30)   | Amount after taxes and discounts                                                                                                                             |
| NETAMOUNT                       | numeric (32 6 NOT NULL  | price before discounts                                                                                                                                       |
| NETPRICE                        | numeric (32 6)  | Number of lines on the transaction                                                                                                                                |
| OPERATINGUNITNUMBER             | nvarchar (30) NOT NULL   | Business Unit that the store maps to                                                                                                                                                      |
| PARTITION                       | nvarchar (nvarchar 20) NOT NULL   | An identification of a data partition in Finance & Operations specific to D365                                                                                                                                                            |
| PAYMENTAMOUNT                   | numeric (32 6)  | Payment amount                                                                                                                                               |
| POSTASSHIPMENT                  | int            | Indicates if this has a shipment associated                                                                                                                                                            |
| REFUNDRECEIPTID                 | nvarchar (18)   | if refund, receipt id for original transaction                                                                                                               |
| RETAILNCREXPORTED               | int            | In the beginning of our roll-out we were pushing transactions to an NCR BOS-system. This field is a flag for that.                                                                                                                                                              |
| RRECEIPTID                      | nvarchar (18)   | Receipt number, different from transaction number                                                                                                            |
| SALEISRETURNSALE                | int            | If sale is return                                                                                                                                            |
| SALESINVOICEAMOUNT              | numeric (32 6)  | Amount for sales invoice if  customer is picking up a few items from an order                                                                                |
| SALESORDERAMOUNT                | numeric (32 6)  | total amount for customer orders(which are different from cash and carry because they have shipping details)                                                 |
| SALESORDERID                    | nvarchar (20)   | Order number(for those with shipping details                                                                                                                 |
| SALESPAYMENTDIFFERENCE          | numeric (32 6)  | Difference amount after Payment made by customer                                                                                                                                                            |
| SHIFT                           | nvarchar (10)   | Shift is a set of transactions throughout the day for which cash and sales activity is calculated. Useful for determining how much cash should be in the til |
| SHIPPINGDATEREQUESTED           | datetime       | Date when goods on customer order should be shipped                                                                                                          |
| SITEID                          | nvarchar (10)   | Typically used for retail  stores to organize by region such as "Northwest US stores"                                                                        |
| STAFF                           | nvarchar (25)   | Point of sale (POS) user ID                                                                                                                                                  |
| SYNCSTARTDATETIME               | datetime NOT NULL       | Fields added to synchronization engine (DIXF) in Finance & Operations. They decline the export sequence.                                                                                                                                                              |
| TAXCALCULATIONTYPE              | int            | If tax is based on Store, Customer, Destination                                                                                                              |
| TERMINAL                        | nvarchar (10) NOT NULL   |  The identifier for point of sale (POS)                                                                                                                                                           |
| TOACCOUNT                       | int            | How much is being charged to customer's account                                                                                                              |
| TOTALDISCOUNTAMOUNT             | numeric (32 6)  | Amount of discount applied to transaction total                                                                                                              |
| TOTALMANUALDISCOUNTAMOUNT       | numeric (32 6)  | If manually applied vs automatic total discount                                                                                                              |
| TOTALMANUALDISCOUNTPERCENTAGE   | numeric (32 6)  | Percentage of manually applied total discount                                                                                                                |
| TRANSACTIONDATE                 | datetime       | Date                                                                                                                                                         |
| TRANSACTIONNUMBER               | nvarchar (44) NOT NULL   | Transaction ID                                                                                                                                               |
| TRANSACTIONSTATUS               | int            | Fields added to synchronization engine (DIXF) in Finance & Operations. They decline the export sequence.                                                                                                                                          |
| TRANSACTIONTIME                 | int            | Time                                                                                                                                                         |
| TRANSACTIONTYPE                 | int            | Cash and carry vs order                                                                                                                                      |
| TRANSFERSTATUS                  | int            |    Used to track status of transfers between warehouses                                                                                                                                                          |
| WAREHOUSE                       | nvarchar (10)   | Maps to Store 1:1                                                                                                                                            |

## Sales

| Field Name                       | Data Type                      | Description                                                                                        |
|---------------------------------|---------------------------|----------------------------------------------------------------------------------------------------|
| BARCODE                         | nvarchar (80)   | Bar code that was scanned                                                                          |
| CASHDISCOUNTAMOUNT              | numeric (32 6)  | Amount of cash disount, if applicable                                                              |
| CATEGORYHIERARCHYNAME           | nvarchar (128)  | Categrory hierarchy used to organize products                                                      |
| CATEGORYNAME                    | nvarchar (254)  | Name of the product category                                                                       |
| CHANNELLISTINGID                | nvarchar (50)  | Applies only for e-commerce, not required for retail                     |
| COSTAMOUNT                      | numeric (32 6) NOT NULL  | Product cost                                                                                       |
| CURRENCY                        | nvarchar (3)    | Currency of the sale                                                                                    |
| CUSTOMERACCOUNT                 | nvarchar (38) NOT NULL   | Customer account number                                                                            |
| CUSTOMERDISCOUNT                | numeric (32 6)  | Customer discount                                                                                  |
| CUSTOMERINVOICEDISCOUNTAMOUNT   | numeric (32 6)  | Discount associated at invoice level during fulfillment                                                                                                 |
| DATAAREAID                      | nvarchar (4) NOT NULL    | Company identifier (Eg:- MSFT US)                                                                                                   |
| DEFINITIONGROUP                 | nvarchar (60)   | Fields added by the synchronization engine (DIFX) in Finance & Operations to define the export sequence.                                                                                              |
| DISCOUNTAMOUNTFORPRINTING       | numeric (32 6)  |Discount amount printed on the receipt                                                                                                   |
| DISCOUNTAMOUNTWITHOUTTAX        | numeric (32 6)  |        Discount amount excluding tax                                                                                            |
| ELECTRONICDELIVERYEMAIL         | nvarchar (80)   | Email address                                                                                      |
| EXECUTIONID                     | nvarchar (90)   |     Fields added by the synchronization engine (DIFX) in Finance & Operations. They define the export sequence.                                                                                               |
| GIFTCARD                        | int            | Gift card number                                                                                   |
| INVENTORYSTATUS                 | int            | Status of the inventory levels                                                                                                 |
| ISLINEDISCOUNTED                | int            | Is the txn line discounted                                                                         |
| ISLINKEDPRODUCTNOTORIGINAL      | int            | If linked item was changed                                                                         |
| ISORIGINALOFLINKEDPRODUCTLIST   | int            | Default linked products                                                                                                   |
| ISPRICECHANGE                   | int            | If price was changed manually                                                                      |
| ISRETURNNOSALE                  | int            | Is this transaction a return or void                                                                                                  |
| ISSCALEPRODUCT                  | int            | Is the connected scale used to get Qty                                                             |
| ISSELECTED                      | int            |Fields added by the synchronization engine (DIFX) in Finance & Operations. They define the export sequence.                                                                                                    |
| ISWEIGHTMANUALLYENTERED         | int            | If scale is not connected, cashier can enter weight manually                                       |
| ISWEIGHTPRODUCT                 | int            | Is the connected scale used to get Qty                                                                              |
| ITEMCOLOR                       | nvarchar (25)   | Color                                                                                              |
| ITEMCONFIGID                    | nvarchar (50)   | Configuration ID for kits                                                                          |
| ITEMID                          | nvarchar (20)   | Product ID                                                                                         |
| ITEMRELATION                    | nvarchar (20)   | Grouping of related Items in a given product group                                                                                                  |
| ITEMSALESTAXGROUP               | nvarchar (10)   | Effective sales tax group for the item                                                             |
| ITEMSIZE                        | nvarchar (10)   | Size                                                                                               |
| ITEMSTYLE                       | nvarchar (10)   | Style, like color and size is another product dimension                                            |
| KEYBOARDPRODUCTENTRY            | int            | If product ID was keyed in                                                                         |
| LINEDISCOUNT                    | numeric (32 6)  | Discount on line                                                                                   |
| LINEMANUALDISCOUNTAMOUNT        | numeric (32 6)  | If discount was manually entered, the amount                                                       |
| LINEMANUALDISCOUNTPERCENTAGE    | numeric (32 6)  | If manual percentage discount was applied, the percentage                                          |
| LINENUMBER                      | numeric (32 16) NOT NULL | Line number on the transaction                                                                     |
| LINEPERCENTAGEDISCOUNT          | numeric(32 6)  | Automatic percentage discount amount                                                               |
| LOGISTICLOCATIONID              | nvarchar (30)   | Address ID in the global address book                                                                                                  |
| LOGISTICSPOSTALADDRESSVALIDFROM | datetime       | Date effective of address id                                                                                                  |
| LOTID   |  nvarchar (20)       | This field is not required                                                                                                 |
| MODEOFDELIVERY                  | nvarchar (10)   | Method of delivery to the customer                                                                 |
| NETAMOUNT                       | numeric (32 6) NOT NULL  | Net amount for transaction                                                                         |
| NETAMOUNTINCLUSIVETAX           | numeric (32 6) NOT NULL  | Net amount with tax included                                                                       |
| NETPRICE                        | numeric (32 6)  | Net price for the line before discounts                                                            |
| OFFERNUMBER                     | nvarchar (40)   | Unique identifier for the offer number                                                                                                  |
| OPERATINGUNITNUMBER             | nvarchar (30)   | Part of the reference data that comprises a store                                                  |
| ORIGINALITEMSALESTAXGROUP       | nvarchar (10)   | If tax is overridden, tracks what the original tax amt was.                                        |
| ORIGINALPRICE                   | numeric (32 6)  | Product price without sale pricing applied                                                         |
| ORIGINALSALESTAXGROUP           | nvarchar (10)   | Original sales tax group for the transaction                                                       |
| PARTITION                       | nvarchar (20) NOT NULL   | An identification of a data partition in Finance & Operations specific to D365                                                                                                                                                          |
| PERIODICDISCOUNTAMOUNT          | numeric (32 6)  | Discount amount for periodic discount(kind of like happy hour)                                     |
| PERIODICDISCOUNTGROUP           | nvarchar (10)   | Periodic discount group                                                                            |
| PERIODICDISCOUNTPERCENTAGE      | numeric (32 6)  | Periodic discount percentage                                                                       |
| PRICE                           | numeric (32 6)  | Price (I believe with discounts)                                                                   |
| PRICEGROUPS                     | nvarchar (10)   | Price group that products and customers belong to.                                                 |
| PRICEINBARCODE                  | int            | If price embedded bar code was scanned                                                             |
| PRODUCTSCANNED                  | int            | If the product was scanned                                                                         |
| QUANTITY                        | numeric (32 6) NOT NULL  | Quantity                                                                                           |
| REASONCODEDISCOUNT              | numeric (32 6)  | If a discount was applied, reason codes can be configured to prompt the cashier to select a reason |
| RECEIPTNUMBER                   | nvarchar (18)   | Receipt number                                                                                     |
| REQUESTEDRECEIPTDATE            | datetime NOT NULL       | For customer orders, date that the customer requests arrival/pickup                                |
| REQUESTEDSHIPDATE               | datetime       | Requested date for order to ship                                                                   |
| RETAILEMAILADDRESSCONTENT       | nvarchar (400)  | email address for receipt                                                                          |
| RETURNLINENUMBER                | numeric (32 16) | Line number from original transaction when returning from journal                                  |
| RETURNOPERATINGUNITNUMBER       | nvarchar (30)   | Store where the return is being processed                                                          |
| RETURNQUANTITY                  | numeric(32 6)  | Quantity being returned.                                                                           |
| RETURNTERMINAL                  | nvarchar (10)   | Terminal where txn is being returned.                                                              |
| RETURNTRANSACTIONNUMBER         | nvarchar (44) NOT NULL   | Original transaction number when returning from receipt/journal                                    |
| RFIDTAGID                       | nvarchar (24)   |  Identification for RFID. Not in Play yet.                                                                                                  |
| SALESTAXAMOUNT                  | numeric (32 6)  | Amt of sales tax applied to the transaction                                                        |
| SALESTAXGROUP                   | nvarchar (10)   | Effective sales tax group for the transaction                                                      |
| SECTIONNUMBER                   | nvarchar (10)   | Not used – physical location for a product in store                                                                                                  |
| SERIALNUMBER                    | nvarchar (20)   | Serial number for the product                                                                      |
| SHELFNUMBER                     | nvarchar (10)   | Shelf number where the product is kept(not really used).                                           |
| SITEID                          | nvarchar (10)   | Category to which store belongs (i.e. Pacific Northwest stores)                                    |
| SKIPREPORTS                     | int            | If set, the record is skipped in reports.                                                                                                   |
| STANDARDNETPRICE                | numeric (32 6)  | Price without discount or trade agreements                                                                              |
| SYNCSTARTDATETIME               | datetime NOT NULL       |  Fields added to synchronization engine (DIXF) in Finance & Operations. They decline the export sequence.                                                                                                   |
| TERMINAL                        | nvarchar (10) NOT NULL   |  The identifier for point of sale (POS)                                                                                                  |
| TOTALDISCOUNT                   | numeric (32 6)  | Amount of discount applied to order total.                                                         |
| TOTALDISCOUNTINFOCODELINENUM    | numeric (32 16) | If prompted for info code when applying total discount, reason code is saved here                  |
| TOTALDISCOUNTPERCENTAGE         | numeric (32 6)  | Discount percent applied to transaction total, if total discount by percent is used                |
| TRANSACTIONCODE                 | int            | Indicator of transaction type                                                                                                  |
| TRANSACTIONNUMBER               | nvarchar (44) NOT NULL   | Transaction number                                                                                 |
| TRANSACTIONSTATUS               | int            | Posted indicates that the statement has been completed(amounts have hit the GL in the back office) |
| TRANSFERSTATUS                  | int            |    Used to track status of transfers between warehouses                                                                                                 |
| UNIT                            | nvarchar (10)   | Measuring unit for the item. For example, gallons, oz, etc.                                                                        |
| UNITPRICE                       | numeric (32 6)  | Price per unit                                                                                     |
| UNITQUANTITY                    | numeric (32 6)  | Quantity of unit sold (not sure how this is different from unit)                                   |
| VARIANTNUMBER                   | nvarchar (10)   | ID for unit combination of color, size and style                                                   |
| WAREHOUSE                       | nvarchar (10)   | Reference data for store. Indicates physical location of the goods.                                |
## Payments

| Field Name                        | Data Type                      | Description                                                     |
|----------------------------------|---------------------------|-----------------------------------------------------------------|
| ACCOUNTNUMBER                    | nvarchar (30)   | Customer's account nubmer if named customer is on transaction   |
| AMOUNTINACCOUNTINGCURRENCY       | numeric (32 6)  | Amount due for line                                             |
| AMOUNTINTENDEREDCURRENCY         | numeric (32 6)  | amount tendered in currency (different if not store's currency) |
| AMOUNTTENDERED                   | numeric (32 6)  | Amount in store currency                                                 |
| AMOUNTTENDEREDADJUSTMENT         | numeric (32 6)  | It's a new feature in the product that allows changes in the transactions, with full audit trail.                                                |
| CARDNUMBER                       | nvarchar (30)    | Truncated card no.                                              |
| CARDTYPEID                       | nvarchar (10)   | Card name (AMEX, VISA, ETC)                                     |
| CREDITVOUCHERID                  | nvarchar (30)   | If paid by voucher, the voucher number                          |
| CURRENCYCODE                     | nvarchar (3)    | Currency paid                                                   |
| DATAAREAID                       | nvarchar (4) NOT NULL    | Company identifier (Eg:- MSFT US)                                                                |
| DEFINITIONGROUP                  | nvarchar (60)   |Fields added by the synchronization engine (DIFX) in Finance & Operations to define the export sequence.                                                                 |
| EXCHANGERATEINACCOUNTINGCURRENCY | numeric (32 16) | Exchange rate                                                   |
| EXCHANGERATEINTENDEREDCURRENCY   | numeric (32 16) | Exchange rate                                                   |
| EXECUTIONID                      | nvarchar (90)   | Fields added by the synchronization engine (DIFX) in Finance & Operations. They define the export sequence.                                                                |
| GIFTCARDID                       | nvarchar (30)   | Gift card number                                                |
| ISCHANGELINE                     | int            | If payment is due back to customer due to overpayment           |
| ISPREPAYMENT                     | int            | Is a deposit                                                    |
| ISSELECTED                       | int            | Fields added by the synchronization engine (DIFX) in Finance & Operations. They define the export sequence.                                                               |
| LINENUMBER                       | numeric (32 16) NOT NULL | Payment line number                                             |
| LOYALTYCARDID                    | nvarchar (30)   | If paying with loyalty points, the card number provided         |
| OPERATINGUNITNUMBER              | nvarchar (30) NOT NULL   | Operating unit unique to store                                  |
| PARTITION                        | nvarchar (20) NOT NULL   |An identification of a data partition in Finance & Operations specific to D365                                                                 |
| QUANTITY                         | numeric (32 6) NOT NULL  | Units Sold                                                               |
| RECEIPTID                        | nvarchar (18)   | Receipt ID. Different from Trasaction ID.                       |
| STAFF                            | nvarchar (25)   | User ID                                                         |
| SYNCSTARTDATETIME                | datetime NOT NULL       | Fields added to synchronization engine (DIXF) in Finance & Operations. They decline the export sequence.                                                                |
| TENDERTYPE                       | nvarchar (10)   | Type of tender paid                                             |
| TERMINAL                         | nvarchar (10) NOT NULL   | Register ID/POS                                                                |
| TRANSACTIONNUMBER                | nvarchar (44) NOT NULL   | Transaction number                                              |
| TRANSACTIONSTATUS                | int            | Status of payment line                                          |
| TRANSFERSTATUS                   | int            |   Used to track status of transfers between warehouses                                                              |
| VOIDSTATUS                       | int            | If a tender line was voided prior to tendering the transaction  |


## PaymentMethod

| Field Name           | Data Type                    | Description |
|---------------------|-------------------------|---------------------------------------------------------------|
| PAYMENTMETHODNUMBER | nvarchar (10) NOT NULL | Identifier for the payment method                            |
| NAME                | nvarchar (60) NOT NULL | Name describing the payment method                           |
| DEFAULTFUNCTION     | int          | Describes the type of payment method Eg:- Cash, Check, Credit Memo/Voucher, Currency|
