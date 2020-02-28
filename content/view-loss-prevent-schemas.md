---
author: veganesa
description: This topic outlines the required schema for the loss prevention feature in Microsoft Dynamics 365 Fraud Protection.
ms.author: veganesa
ms.service: fraud-protection
ms.date: 02/28/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin

title: Loss prevention schemas
---

# Loss prevention schemas

[!include [banner](includes/preview-banner.md)]

This topic outlines the schemas that define the data that is used to generate models and determine risk assessments.

Note the following formatting guidelines throughout:

- The files are in CSV UTF-8 (comma-delimited) format (\*.csv).
- The maximum file size is 10 gigabytes (GB).
- The **DateTime** columns are in International Organization for Standardization (ISO) 8601 format. For example, **DateTime.UtcNow.ToString("o")** might have the result **"2019-03-14T20:18:11.254Z"**.
- The decimal precision is two decimal places.
- The following characters are escaped in all columns: commas, new line characters, and multiline characters.
- Any field that has a "NOT NULL" constraint is **mandatory**. All other fields are **optional**.

## Transactions

| Field name                      | Data type                       | Description |
|---------------------------------|---------------------------------|-------------|
| AMOUNTPOSTEDTOACCOUNT           | numeric (32 6)                  | The amount that is posted to the account for general ledger (GL) posting. |
| BATCHID                         | bigint                          | The identifier for the batch or shift. |
| CHANNELREFERENCEID              | nvarchar (50)                   | An identifier that indicates the channel that is used for purchases in omni-channel scenarios for e-commerce merchants. |
| COMMENT                         | nvarchar (60)                   | A transaction-level comment. |
| COSTAMOUNT                      | numeric (32 6) NOT NULL         | The cost for items. |
| CREATEDOFFLINE                  | int                             | This field indicates if the transaction was created offline without database connectivity. |
| CURRENCY                        | nvarchar (3)                    | The currency code (for example, **USD**). |
| CUSTOMERACCOUNT                 | nvarchar (38) NOT NULL          | The account number. |
| CUSTOMERDISCOUNTAMOUNT          | numeric (32 6)                  | The discount that is mapped to the customer and automatically applied for that customer. |
| DATAAREAID                      | nvarchar (4) NOT NULL           | The identifier of the legal entity in Dynamics 365 Retail. |
| DEFINITIONGROUP                 | nvarchar (60)                   | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Retail. They define the export sequence. |
| DELIVERYMODE                    | nvarchar (10)                   | The mode of delivery, if the transaction isn't a cash-and-carry transaction. |
| DISCOUNTAMOUNT                  | numeric (32 6)                  | The discount amount, if any discounts are applied. |
| DISCOUNTAMOUNTWITHOUTTAX        | numeric (32 6)                  | The discount amount, excluding tax. |
| EXCHANGERATE                    | numeric (32 16)                 | The exchange rate, if a non-store currency was used for payment. |
| EXECUTIONID                     | nvarchar (90)                   | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Retail. They define the export sequence. |
| GROSSAMOUNT                     | numeric (32 6)                  | The total amount that is due before discounts are applied. |
| INCOMEEXPENSEAMOUNT             | numeric (32 6)                  | This field indicates the adjustment amount to refect drawer-related expenses if any.|
| INFOCODEDISCOUNTGROUP           | nvarchar (10)                   |This is the informaiton code assoicated with the discount applied. |
| INVOICEID                       | nvarchar (20)                   | This field is related to payments on customer accounts. It indicates the invoice that the customer is making a payment against. |
| ISSELECTED                      | int                             | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Retail. They define the export sequence. |
| ITEMSPOSTED                     | int                             | The count of items that are part of the shipment that is posted. |
| LOGISTICPOSTALADDRESSVALIDTO    | datetime                        | Delivery address effectivity, based on the date when the address is no longer valid for the delivery of items. |
| LOGISTICSLOCATIONID             | nvarchar (30)                   | This field identifies the location to which the shipment is getting delivered to. |
| LOGISTICSPOSTALADDRESSVALIDFROM | datetime                        | Delivery address effectivity, based on the date when the address is valid for the delivery of items. |
| LOGISTICSPOSTALCITY             | nvarchar (60)                   | The city where the item is delivered to. |
| LOGISTICSPOSTALCOUNTY           | nvarchar (10)                   | The county where the item is delivered to. |
| LOGISTICSPOSTALSTATE            | nvarchar (10)                   | The state where the item is delivered to. |
| LOGISTICSPOSTALSTREET           | nvarchar (250)                  | The street where the item is delivered to. |
| LOGISTICSPOSTALZIPCODE          | nvarchar (10)                   | The zip code where the item is delivered to. |
| LOYALTYCARDID                   | nvarchar (30)                   | The loality card number associated with the customer. |
| NETAMOUNT                       | numeric (32 6 NOT NULL          | The price before discounts are applied. |
| NETPRICE                        | numeric (32 6)                  | The number of lines on the transaction. |
| OPERATINGUNITNUMBER             | nvarchar (30) NOT NULL          | The business unit that the store is mapped to. |
| PARTITION                       | nvarchar (nvarchar 20) NOT NULL | The identifier of a data partition in Dynamics 365 Retail that is specific to Dynamics 365. |
| PAYMENTAMOUNT                   | numeric (32 6)                  | The payment amount. |
| POSTASSHIPMENT                  | int                             | This field indicates whether or not an item has an assoicated shipment.  |
| REFUNDRECEIPTID                 | nvarchar (18)                   | If the transaction is a refund, the receipt ID for the original transaction. |
| RETAILNCREXPORTED               | int                             | At the beginning of the roll-out, this field was used as a flag to push transactions to an NCR BOS system. |
| RRECEIPTID                      | nvarchar (18)                   | The receipt number. This number differs from the transaction number. |
| SALEISRETURNSALE                | int                             | A value that indicates whether the sale is a return. |
| SALESINVOICEAMOUNT              | numeric (32 6)                  | The amount of the sales invoice if the customer is picking up just a few items from an order. |
| SALESORDERAMOUNT                | numeric (32 6)                  | The total amount for customer orders. (These orders differ from cash-and-carry transactions, because they have shipping details.) |
| SALESORDERID                    | nvarchar (20)                   | The order number, for orders that have shipping details. |
| SALESPAYMENTDIFFERENCE          | numeric (32 6)                  | The difference amount after the customer makes a payment. |
| SHIFT                           | nvarchar (10)                   | The shift. A shift is a set of transactions during the day that cash and sales activity is calculated for. Shifts are useful for determining how much cash should be in the terminal. |
| SHIPPINGDATEREQUESTED           | datetime                        | The date when goods on the customer order should be shipped. |
| SITEID                          | nvarchar (10)                   | This field is typically used for retail stores. It's used to organize the stores by region (for example, **Northwest US stores**). |
| STAFF                           | nvarchar (25)                   | The ID of the point of sale (POS) user. |
| SYNCSTARTDATETIME               | datetime NOT NULL               | Fields that are added to the synchronization engine (DIXF) in Dynamics 365 Retail. They define the export sequence. |
| TAXCALCULATIONTYPE              | int                             | A value that indicates whether tax is based on the store, customer, or destination. |
| TERMINAL                        | nvarchar (10) NOT NULL          | The identifier for the POS. |
| TOACCOUNT                       | int                             | The amount that is being charged to the customer's account. |
| TOTALDISCOUNTAMOUNT             | numeric (32 6)                  | The amount of the discount that is applied to the transaction total. |
| TOTALMANUALDISCOUNTAMOUNT       | numeric (32 6)                  | This field indicates the total discount amount that is manually applied, not automatically calculated. |
| TOTALMANUALDISCOUNTPERCENTAGE   | numeric (32 6)                  | The percentage of the manually applied total discount. |
| TRANSACTIONDATE                 | datetime                        | The date. |
| TRANSACTIONNUMBER               | nvarchar (44) NOT NULL          | The transaction identifier. |
| TRANSACTIONSTATUS               | int                             | Fields that are added to the synchronization engine (DIXF) in Dynamics 365 Retail. They decline the export sequence. |
| TRANSACTIONTIME                 | int                             | The time of the transaction. |
| TRANSACTIONTYPE                 | int                             | A value that indicates whether the transaction is a cash-and-carry transaction or an order. |
| TRANSFERSTATUS                  | int                             | This field is used to track the status of transfers between warehouses. |
| WAREHOUSE                       | nvarchar (10)                   | The warehouse that is associated with a store. |

## Sales

| Field Name                      | Data Type                | Description |
|---------------------------------|--------------------------|-------------|
| BARCODE                         | nvarchar (80)            | The bar code that was scanned. |
| CASHDISCOUNTAMOUNT              | numeric (32 6)           | The amount of the cash discount, if a cash discount is applied. |
| CATEGORYHIERARCHYNAME           | nvarchar (128)           | The category hierarchy that is used to organize products. |
| CATEGORYNAME                    | nvarchar (254)           | The name of the product category. |
| CHANNELLISTINGID                | nvarchar (50)            | This field applies only to e-commerce. It isn't required for retail stores. |
| COSTAMOUNT                      | numeric (32 6) NOT NULL  | The product cost. |
| CURRENCY                        | nvarchar (3)             | The currency that is used for the sale (for example, **USD**). |
| CUSTOMERACCOUNT                 | nvarchar (38) NOT NULL   | The customer account number. |
| CUSTOMERDISCOUNT                | numeric (32 6)           | The customer discount. |
| CUSTOMERINVOICEDISCOUNTAMOUNT   | numeric (32 6)           | The discount that is associated at the invoice level during fulfillment. |
| DATAAREAID                      | nvarchar (4) NOT NULL    | The company identifier (for example, **MSFT**). |
| DEFINITIONGROUP                 | nvarchar (60)            | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Retail. They define the export sequence. |
| DISCOUNTAMOUNTFORPRINTING       | numeric (32 6)           | The discount amount that is printed on the receipt. |
| DISCOUNTAMOUNTWITHOUTTAX        | numeric (32 6)           | The discount amount, excluding tax. |
| ELECTRONICDELIVERYEMAIL         | nvarchar (80)            | The email address. |
| EXECUTIONID                     | nvarchar (90)            | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Retail. They define the export sequence. |
| GIFTCARD                        | int                      | The gift card number. |
| INVENTORYSTATUS                 | int                      | The status of the inventory levels. |
| ISLINEDISCOUNTED                | int                      | A value that indicates whether the transaction line is discounted. |
| ISLINKEDPRODUCTNOTORIGINAL      | int                      | This field indicates if there were any linked item within the same product group that were changed. |
| ISORIGINALOFLINKEDPRODUCTLIST   | int                      | The default linked products. |
| ISPRICECHANGE                   | int                      | This field indicates if there were any prices changes made manually to the list of products in the transaction. |
| ISRETURNNOSALE                  | int                      | A value that indicates whether this transaction is a return or void. |
| ISSCALEPRODUCT                  | int                      | A value that indicates whether the connected scale is used to get the quantity. |
| ISSELECTED                      | int                      | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Retail. They define the export sequence. |
| ISWEIGHTMANUALLYENTERED         | int                      | If a scale isn't connected, the cashier can manually enter the weight. |
| ISWEIGHTPRODUCT                 | int                      | A value that indicates whether the connected scale is used to get the quantity. |
| ITEMCOLOR                       | nvarchar (25)            | The color. |
| ITEMCONFIGID                    | nvarchar (50)            | The configuration ID for kits. |
| ITEMID                          | nvarchar (20)            | The product ID. |
| ITEMRELATION                    | nvarchar (20)            | A grouping of related items in a specific product group. |
| ITEMSALESTAXGROUP               | nvarchar (10)            | The effective sales tax group for the item. |
| ITEMSIZE                        | nvarchar (10)            | The size. |
| ITEMSTYLE                       | nvarchar (10)            | The style. Like color and size, style is a product dimension. |
| KEYBOARDPRODUCTENTRY            | int                      | This field indicates if the product ID was entered by the cashier manually on the keyboard at the POS. |
| LINEDISCOUNT                    | numeric (32 6)           | The discount amount that is applied for the line item. |
| LINEMANUALDISCOUNTAMOUNT        | numeric (32 6)           | If the discount was manually entered, the discount amount. |
| LINEMANUALDISCOUNTPERCENTAGE    | numeric (32 6)           | If a manual percentage discount was applied, the discount percentage. |
| LINENUMBER                      | numeric (32 16) NOT NULL | The line number on the transaction. |
| LINEPERCENTAGEDISCOUNT          | numeric(32 6)            | The amount of the automatic percentage discount. |
| LOGISTICLOCATIONID              | nvarchar (30)            | The address ID in the global address book. |
| LOGISTICSPOSTALADDRESSVALIDFROM | datetime                 | The effective date of the address ID. |
| LOTID                           | nvarchar (20)            | This field isn't required. |
| MODEOFDELIVERY                  | nvarchar (10)            | The method of delivery for the customer. |
| NETAMOUNT                       | numeric (32 6) NOT NULL  | The net amount for the transaction. |
| NETAMOUNTINCLUSIVETAX           | numeric (32 6) NOT NULL  | The net amount, including tax. |
| NETPRICE                        | numeric (32 6)           | The net price for the line before discounts are applied. |
| OFFERNUMBER                     | nvarchar (40)            | The unique identifier for the offer number. |
| OPERATINGUNITNUMBER             | nvarchar (30)            | The part of the reference data that comprises a store. |
| ORIGINALITEMSALESTAXGROUP       | nvarchar (10)            | If tax is overridden, this field tracks the original tax amount. |
| ORIGINALPRICE                   | numeric (32 6)           | The product price when sale pricing isn't applied. |
| ORIGINALSALESTAXGROUP           | nvarchar (10)            | The original sales tax group for the transaction. |
| PARTITION                       | nvarchar (20) NOT NULL   | The identifier of a data partition in Dynamics 365 Retail that is specific to Dynamics 365. |
| PERIODICDISCOUNTAMOUNT          | numeric (32 6)           | The discount amount for the periodic discount. |
| PERIODICDISCOUNTGROUP           | nvarchar (10)            | The periodic discount group. |
| PERIODICDISCOUNTPERCENTAGE      | numeric (32 6)           | The periodic discount percentage. |
| PRICE                           | numeric (32 6)           | The price of the item. |
| PRICEGROUPS                     | nvarchar (10)            | The price group that products and customers belong to. |
| PRICEINBARCODE                  | int                      | This field indicates if a price-embedded bar code was scanned for a specific product within the transaction. |
| PRODUCTSCANNED                  | int                      | This field indicates if the bar code in the product was scanned as part of the transaction. |
| QUANTITY                        | numeric (32 6) NOT NULL  | The quantity. |
| REASONCODEDISCOUNT              | numeric (32 6)           | If a discount was applied, reason codes can be configured to prompt the cashier to select a reason. |
| RECEIPTNUMBER                   | nvarchar (18)            | The receipt number. |
| REQUESTEDRECEIPTDATE            | datetime NOT NULL        | For customer orders, the date when the customer has requested arrival/pickup. |
| REQUESTEDSHIPDATE               | datetime                 | The requested shipping date for the order. |
| RETAILEMAILADDRESSCONTENT       | nvarchar (400)           | The email address for the receipt. |
| RETURNLINENUMBER                | numeric (32 16)          | The line number from the original transaction when the return is done from the journal. |
| RETURNOPERATINGUNITNUMBER       | nvarchar (30)            | The store where the return is being processed. |
| RETURNQUANTITY                  | numeric(32 6)            | The quantity that is being returned. |
| RETURNTERMINAL                  | nvarchar (10)            | The terminal where the return transaction is being processed. |
| RETURNTRANSACTIONNUMBER         | nvarchar (44) NOT NULL   | Original transaction number when the return is done from the receipt or journal. |
| RFIDTAGID                       | nvarchar (24)            | The identifier for radio frequency identification (RFID). |
| SALESTAXAMOUNT                  | numeric (32 6)           | The amount of sales tax that is applied to the transaction. |
| SALESTAXGROUP                   | nvarchar (10)            | The effective sales tax group for the transaction. |
| SECTIONNUMBER                   | nvarchar (10)            | The physical location of the product in the store. This field isn't used. |
| SERIALNUMBER                    | nvarchar (20)            | The serial number for the product. |
| SHELFNUMBER                     | nvarchar (10)            | The shelf number where the product is kept. |
| SITEID                          | nvarchar (10)            | The category that the store belongs to (for example, **PACNW**). |
| SKIPREPORTS                     | int                      | If this field is set, the record is skipped in reports. |
| STANDARDNETPRICE                | numeric (32 6)           | The price, excluding discounts and trade agreements. |
| SYNCSTARTDATETIME               | datetime NOT NULL        | Fields that are added to the synchronization engine (DIXF) in Dynamics 365 Retail. They define the export sequence. |
| TERMINAL                        | nvarchar (10) NOT NULL   | The identifier for the POS. |
| TOTALDISCOUNT                   | numeric (32 6)           | The amount of the discount that is applied to the order total. |
| TOTALDISCOUNTINFOCODELINENUM    | numeric (32 16)          | If the user is prompted for an info code when a total discount is applied, the reason code is saved in this field. |
| TOTALDISCOUNTPERCENTAGE         | numeric (32 6)           | The discount percentage that is applied to the transaction total, if a total discount by percentage is used. |
| TRANSACTIONCODE                 | int                      | An indicator of the transaction type. |
| TRANSACTIONNUMBER               | nvarchar (44) NOT NULL   | The transaction number |
| TRANSACTIONSTATUS               | int                      | A value of **Posted** indicates that the statement has been completed (that is, amounts have reached the GL in the back office). |
| TRANSFERSTATUS                  | int                      | This field is used to track the status of transfers between warehouses. |
| UNIT                            | nvarchar (10)            | The unit of measure for the item. Examples include gallons and ounces (oz.). |
| UNITPRICE                       | numeric (32 6)           | The price per unit. |
| UNITQUANTITY                    | numeric (32 6)           | The quantity of units that was sold. |
| VARIANTNUMBER                   | nvarchar (10)            | The ID for the unit combination of color, size, and style. |
| WAREHOUSE                       | nvarchar (10)            | Reference data for the store. This field indicates the physical location of the goods. |

## Payments

| Field Name                       | Data Type                | Description |
|----------------------------------|--------------------------|-------------|
| ACCOUNTNUMBER                    | nvarchar (30)            | The customer account number, if a named customer appears on the transaction. |
| AMOUNTINACCOUNTINGCURRENCY       | numeric (32 6)           | The amount that is due for the line. |
| AMOUNTINTENDEREDCURRENCY         | numeric (32 6)           | The amount that was tendered in local currency as it applies to the country where the store is located. |
| AMOUNTTENDERED                   | numeric (32 6)           | The amount in the store currency. |
| AMOUNTTENDEREDADJUSTMENT         | numeric (32 6)           | A new feature in the product allows for changes to the transactions and provides a full audit trail. |
| CARDNUMBER                       | nvarchar (30)            | The card number that was used to make a payment. |
| CARDTYPEID                       | nvarchar (10)            | The card name (for example, **AMEX** or **VISA**). |
| CREDITVOUCHERID                  | nvarchar (30)            | If a voucher is used for payment, the voucher number. |
| CURRENCYCODE                     | nvarchar (3)             | The currency that was paid. |
| DATAAREAID                       | nvarchar (4) NOT NULL    | The company identifier (for example, **MSFT**). |
| DEFINITIONGROUP                  | nvarchar (60)            | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Retail. They define the export sequence. |
| EXCHANGERATEINACCOUNTINGCURRENCY | numeric (32 16)          | The exchange rate in relation to US dollars (USD). |
| EXCHANGERATEINTENDEREDCURRENCY   | numeric (32 16)          | The exchange rate in relation to USD. |
| EXECUTIONID                      | nvarchar (90)            | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Retail. They define the export sequence. |
| GIFTCARDID                       | nvarchar (30)            | The gift card number. |
| ISCHANGELINE                     | int                      | This field indicates if payment amount that is due back to the customer. |
| ISPREPAYMENT                     | int                      | A value that indicates whether the payment is a deposit. |
| ISSELECTED                       | int                      | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Retail. They define the export sequence. |
| LINENUMBER                       | numeric (32 16) NOT NULL | The payment line number. |
| LOYALTYCARDID                    | nvarchar (30)            | If loyalty points are used for payment, the card number that was provided. |
| OPERATINGUNITNUMBER              | nvarchar (30) NOT NULL   | The operating unit that is unique to the store. |
| PARTITION                        | nvarchar (20) NOT NULL   | The identifier of a data partition in Dynamics 365 Retail that is specific to Dynamics 365. |
| QUANTITY                         | numeric (32 6) NOT NULL  | The number of units that were sold. |
| RECEIPTID                        | nvarchar (18)            | The receipt ID. This ID differs from the transaction ID. |
| STAFF                            | nvarchar (25)            | The user ID. |
| SYNCSTARTDATETIME                | datetime NOT NULL        | Fields that are added to the synchronization engine (DIXF) in Dynamics 365 Retail. They decline the export sequence. |
| TENDERTYPE                       | nvarchar (10)            | The type of tender that was paid. |
| TERMINAL                         | nvarchar (10) NOT NULL   | The identifier of the register or Point of Sale (POS). |
| TRANSACTIONNUMBER                | nvarchar (44) NOT NULL   | The transaction number. |
| TRANSACTIONSTATUS                | int                      | The status of the payment line. |
| TRANSFERSTATUS                   | int                      | This field is used to track the status of transfers between warehouses. |
| VOIDSTATUS                       | int                      | A value that indicates whether a tender line was voided before the transaction was tendered. |

## PaymentMethod

| Field Name          | Data Type              | Description |
|---------------------|------------------------|-------------|
| PAYMENTMETHODNUMBER | nvarchar (10) NOT NULL | The identifier for the payment method. |
| NAME                | nvarchar (60) NOT NULL | The descriptive name for the payment method. |
| DEFAULTFUNCTION     | int                    | A description of the type of payment method, such as **Cash**, **Check**, **Credit Memo/Voucher**, or **Currency**. |
