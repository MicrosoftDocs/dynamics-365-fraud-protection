---
author: yvonnedeq
description: This topic outlines data schemas for loss prevention in Microsoft Dynamics 365 Fraud Protection.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 01/28/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Data schemas for loss prevention in Fraud Protection
---

# Data schemas for loss prevention in Fraud Protection

This topic outlines the schemas that define the data that is used to generate models and determine risk assessments.

Note the following formatting guidelines throughout:

- The files are in CSV UTF-8 (comma-delimited) format (\*.csv).
- The maximum file size is 10 gigabytes (GB).
- The **DateTime** columns are in International Organization for Standardization (ISO) 8601 format. For example, **DateTime.UtcNow.ToString("o")** might have the result **"2019-03-14T20:18:11.254Z"**.
- The decimal precision is two decimal places.
- The following characters are escaped in all columns: commas, new line characters, and multiline characters.

## Transactions

| Field name                      | Data type                       | Description |
|---------------------------------|---------------------------------|-------------|
| DEFINITIONGROUP      | string (60)      | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Commerce. They define the export sequence.      |
| EXECUTIONID      | string (90)      | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Commerce. They define the export sequence.      |
| ISSELECTED      | int      | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Commerce. They define the export sequence.      |
| TRANSFERSTATUS      | int      | This field is used to track the status of transfers between warehouses.  |
| BATCHID      | int      | The identifier for the batch or shift.      |
| TERMINAL      | string (10) NOT NULL      | The identifier for the POS.      |
| AMOUNTPOSTEDTOACCOUNT      | double (32 6)      | The amount that is posted to the account for general ledger (GL) posting.      |
| CHANNELREFERENCEID      | string (50)      | An identifier that indicates the channel that is used for purchases in omni-channel scenarios for e-commerce merchants.      |
| COSTAMOUNT      | double (32 6) NOT NULL      | The cost for items.      |
| CREATEDOFFLINE      | int      | This field indicates if the transaction was created offline without database connectivity.      |
| CURRENCY      | string (3)      | The currency code (for example, USD).      |
| CUSTOMERACCOUNT      | string (38) NOT NULL      | The account number.      |
| CUSTOMERDISCOUNTAMOUNT      | double (32 6)      | The discount that is mapped to the customer and automatically applied for that customer.      |
| DISCOUNTAMOUNT      | double (32 6)      | The discount amount, if any discounts are applied.      |
| DELIVERYMODE      | string (10)      | The mode of delivery, if the transaction isn't a cash-and-carry transaction.      |
| TRANSACTIONSTATUS      | int  NOT NULL      | Fields that are added to the synchronization engine (DIXF) in Dynamics 365 Commerce. They define the export sequence.      |
| EXCHANGERATE      | double (32 16)      | The exchange rate, if a non-store currency was used for payment.      |
| GROSSAMOUNT      | double (32 6)      | The total amount that is due before discounts are applied.     |
| INCOMEEXPENSEAMOUNT      | double (32 6)      | This field indicates the adjustment amount to reflect drawer-related expenses if any.      |
| INFOCODEDISCOUNTGROUP      | string (10)      | This is the information code associated with the discount applied.      |
| WAREHOUSE      | string (10) NOT NULL      | The warehouse that is associated with a store.      |
| SITEID      | string (10)      | This field is typically used for retail stores. It's used to organize the stores by region (for example, Northwest US stores).      |
| INVOICEID      | string (20)      | This field is related to payments on customer accounts. It indicates the invoice that the customer is making a payment against.      |
| ITEMSPOSTED      | int      | The count of items that are part of the shipment that is posted.      |
| LOYALTYCARDID      | string (30)      | The locality card number associated with the customer.      |
| NETAMOUNT      | double (32 6 NOT NULL      | The price before discounts are applied.      |
| PAYMENTAMOUNT      | double (32 6)      | The payment amount.      |
| POSTASSHIPMENT      | int      | This field indicates whether or not an item has an associated shipment.|
| RECEIPTID      | string (18)      | The receipt number. This number differs from the transaction number.      |
| REFUNDRECEIPTID      | string (18)      | If the transaction is a refund, the receipt ID for the original transaction.      |
| SALEISRETURNSALE      | int      | A value that indicates whether the sale is a return.      |
| SALESINVOICEAMOUNT      | double (32 6)      | The amount of the sales invoice if the customer is picking up just a few items from an order.      |
| SALESORDERAMOUNT      | double (32 6)      | The total amount for customer orders. (These orders differ from cash-and-carry transactions, because they have shipping details.)      |
| SALESORDERID      | string (20)      | The order number, for orders that have shipping details.      |
| SALESPAYMENTDIFFERENCE      | double (32 6)      | The difference amount after the customer makes a payment.      |
| SHIFT      | string (10)      | The shift. A shift is a set of transactions during the day that cash and sales activity is calculated for. Shifts are useful for determining how much cash should be in the terminal.      |
| SHIPPINGDATEREQUESTED      | datetime      | The date when goods on the customer order should be shipped.      |
| STAFF      | string (25)  NOT NULL      | The ID of the point of sale (POS) user.      |
| TOACCOUNT      | int      | The amount that is being charged to the customer's account.      |
| TOTALDISCOUNTAMOUNT      | double (32 6)      | The amount of the discount that is applied to the transaction total.      |
| TOTALMANUALDISCOUNTAMOUNT      | double (32 6)      | This field indicates the total discount amount that is manually applied, not automatically calculated.      |
| TOTALMANUALDISCOUNTPERCENTAGE      | double (32 6)      | The percentage of the manually applied total discount.      |
| TRANSACTIONNUMBER      | string (44) NOT NULL      | The transaction identifier.      |
| TRANSACTIONDATE      | datetime      | The date.      |
| TRANSACTIONTIME      | int      | The time of the transaction.      |
| TRANSACTIONTYPE      | int      | A value that indicates whether the transaction is a cash-and-carry transaction or an order.      |
| LOGISTICSLOCATIONID      | string (30)      | This field identifies the location to which the shipment is getting delivered to.      |
| LOGISTICSPOSTALCITY      | string (60)      | The city where the item is delivered to.      |
| LOGISTICSPOSTALCOUNTY      | string (10)      | The county where the item is delivered to.      |
| LOGISTICSPOSTALSTATE      | string (10)      | The state where the item is delivered to.      |
| LOGISTICSPOSTALSTREET      | string (250)      | The street where the item is delivered to.      |
| LOGISTICSPOSTALZIPCODE      | string (10)      | The zip code where the item is delivered to.      |
| LOGISTICSPOSTALADDRESSVALIDFROM      | datetime      | Delivery address effectivity, based on the date when the address is valid for the delivery of items.      |
| LOGISTICPOSTALADDRESSVALIDTO      | datetime      | Delivery address effectivity, based on the date when the address is no longer valid for the delivery of items.      |
| OPERATINGUNITNUMBER      | string (30) NOT NULL      | The business unit that the store is mapped to.      |
| COMMENT      | string (60)      | A transaction-level comment.      |
| TAXCALCULATIONTYPE      | int      | A value that indicates whether tax is based on the store, customer, or destination.      |
| DISCOUNTAMOUNTWITHOUTTAX      | double (32 6) NOT NULL      | The discount amount, excluding tax.      |
| NETPRICE      | double (32 6) NOT NULL      | The number of lines on the transaction.      |
| RETAILNCREXPORTED      | int      | At the beginning of the roll-out, this field was used as a flag to push transactions to an NCR BOS system.      |
| PARTITION      | string (string 20) NOT NULL      | The identifier of a data partition in Dynamics 365 Commerce that is specific to Dynamics 365.      |
| DATAAREAID      | string (4) NOT NULL      | The identifier of the legal entity in Dynamics 365 Commerce.      |
| SYNCSTARTDATETIME      | datetime NOT NULL      | Fields that are added to the synchronization engine (DIXF) in Dynamics 365 Commerce. They define the export sequence.      |

## Sales

| Field Name                      | Data Type                | Description |
|---------------------------------|--------------------------|-------------|
| DEFINITIONGROUP      | string (60)      | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Commerce. They define the export sequence.      |
| EXECUTIONID      | string (90)      | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Commerce. They define the export sequence.      |
| ISSELECTED      | int      | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Commerce. They define the export sequence.      |
| TRANSFERSTATUS      | int       | This field is used to track the status of transfers between warehouses. |
| SALESTAXGROUP      | string (10)      | The effective sales tax group for the transaction.      |
| ITEMSALESTAXGROUP      | string (10)      | The effective sales tax group for the item.      |
| TERMINAL      | string (10) NOT NULL      | The identifier for the POS.      |
| TRANSACTIONNUMBER      | string (44) NOT NULL      | The transaction number      |
| BARCODE      | string (80)      | The bar code that was scanned.      |
| COSTAMOUNT      | double (32 6) NOT NULL      | The product cost.      |
| CURRENCY      | string (3)      | The currency that is used for the sale (for example, USD).      |
| CUSTOMERACCOUNT      | string (38) NOT NULL      | The customer account number.      |
| CUSTOMERDISCOUNT      | double (32 6)      | The customer discount.      |
| CUSTOMERINVOICEDISCOUNTAMOUNT      | double (32 6)      | The discount that is associated at the invoice level during fulfillment.      |
| CASHDISCOUNTAMOUNT      | double (32 6) NOT NULL      | The amount of the cash discount, if a cash discount is applied.      |
| PRICEGROUPS      | string (10)      | The price group that products and customers belong to.      |
| OFFERNUMBER      | string (40)      | The unique identifier for the offer number.      |
| DISCOUNTAMOUNTFORPRINTING      | double (32 6)      | The discount amount that is printed on the receipt.      |
| MODEOFDELIVERY      | string (10)      | The method of delivery for the customer.      |
| ELECTRONICDELIVERYEMAIL      | string (80)      | The email address.      |
| RETAILEMAILADDRESSCONTENT      | string (400)      | The email address for the receipt.      |
| GIFTCARD      | int NOT NULL      | The gift card number.      |
| REASONCODEDISCOUNT      | double (32 6)      | If a discount was applied, reason codes can be configured to prompt the cashier to select a reason.      |
| WAREHOUSE      | string (10) NOT NULL      | Reference data for the store. This field indicates the physical location of the goods.      |
| SERIALNUMBER      | string (20)      | The serial number for the product.      |
| SITEID      | string (10)      | The category that the store belongs to (for example, PACNW).      |
| INVENTORYSTATUS      | int      | The status of the inventory levels.      |
| LOTID      | string (20)      | This field isn't required.      |
| ITEMID      | string (20)      | The product ID.      |
| PRODUCTSCANNED      | int      | This field indicates if the bar code in the product was scanned as part of the transaction.      |
| ITEMRELATION      | string (20)      | A grouping of related items in a specific product group.      |
| KEYBOARDPRODUCTENTRY      | int      | This field indicates if the product ID was entered by the cashier manually on the keyboard at the POS.      |
| LINEDISCOUNT      | double (32 6) NOT NULL      | The discount amount that is applied for the line item.      |
| LINEMANUALDISCOUNTAMOUNT      | double (32 6) NOT NULL      | If the discount was manually entered, the discount amount.      |
| LINEMANUALDISCOUNTPERCENTAGE      | double (32 6) NOT NULL      | If a manual percentage discount was applied, the discount percentage.      |
| LINENUMBER      | double (32 16) NOT NULL      | The line number on the transaction.      |
| ISLINEDISCOUNTED      | int      | A value that indicates whether the transaction line is discounted.      |
| ISLINKEDPRODUCTNOTORIGINAL      | int      | This field indicates if there were any linked item within the same product group that were changed.      |
| CHANNELLISTINGID      | string (50)      | This field applies only to e-commerce. It isn't required for retail stores.      |
| NETAMOUNT      | double (32 6) NOT NULL      | The net amount for the transaction.      |
| NETAMOUNTINCLUSIVETAX      | double (32 6) NOT NULL      | The net amount, including tax.      |
| NETPRICE      | double (32 6) NOT NULL      | The net price for the line before discounts are applied.    |
| ISORIGINALOFLINKEDPRODUCTLIST      | int      | The default linked products.      |
| ORIGINALPRICE      | double (32 6) NOT NULL      | The product price when sale pricing isn't applied.   |
| ORIGINALSALESTAXGROUP      | string (10)      | The original sales tax group for the transaction.      |
| ORIGINALITEMSALESTAXGROUP      | string (10)      | If tax is overridden, this field tracks the original tax amount.      |
| PERIODICDISCOUNTAMOUNT      | double (32 6) NOT NULL      | The discount amount for the periodic discount.      |
| PERIODICDISCOUNTGROUP      | string (10)      | The periodic discount group.      |
| PERIODICDISCOUNTPERCENTAGE      | double (32 6)      | The periodic discount percentage.      |
| PRICE      | double (32 6) NOT NULL      | The price of the item.      |
| ISPRICECHANGE      | int NOT NULL      | This field indicates if there were any prices changes made manually to the list of products in the transaction.      |
| PRICEINBARCODE      | int      | This field indicates if a price-embedded bar code was scanned for a specific product within the transaction.      |
| QUANTITY      | double (32 6) NOT NULL      | The quantity.      |
| REQUESTEDRECEIPTDATE      | datetime NOT NULL      | For customer orders, the date when the customer has requested arrival/pickup.      |
| RECEIPTNUMBER      | string (18)      | The receipt number.      |
| RETURNLINENUMBER      | double (32 16)      | The line number from the original transaction when the return is done from the journal.      |
| ISRETURNNOSALE      | int      | A value that indicates whether this transaction is a return or void.      |
| RETURNQUANTITY      | double(32 6)      | The quantity that is being returned.      |
| RETURNTERMINAL      | string (10)      | The terminal where the return transaction is being processed.      |
| RETURNTRANSACTIONNUMBER      | string (44) NOT NULL      | Original transaction number when the return is done from the receipt or journal.      |
| RFIDTAGID      | string (24)      | The identifier for radio frequency identification (RFID).      |
| ISSCALEPRODUCT      | int      | A value that indicates whether the connected scale is used to get the quantity.      |
| SECTIONNUMBER      | string (10)      | The physical location of the product in the store. This field isn't used.      |
| SHELFNUMBER      | string (10)      | The shelf number where the product is kept.      |
| REQUESTEDSHIPDATE      | datetime      | The requested shipping date for the order.      |
| STANDARDNETPRICE      | double (32 6)      | The price, excluding discounts and trade agreements.      |
| SALESTAXAMOUNT      | double (32 6) NOT NULL      | The amount of sales tax that is applied to the transaction.      |
| TOTALDISCOUNT      | double (32 6) NOT NULL      | The amount of the discount that is applied to the order total.      |
| TOTALDISCOUNTINFOCODELINENUM      | double (32 16)      | If the user is prompted for an info code when a total discount is applied, the reason code is saved in this field.      |
| TOTALDISCOUNTPERCENTAGE      | double (32 6)      | The discount percentage that is applied to the transaction total, if a total discount by percentage is used.      |
| TRANSACTIONCODE      | int      | An indicator of the transaction type.      |
| TRANSACTIONSTATUS      | int NOT NULL      | A value of Posted indicates that the statement has been completed (that is, amounts have reached the GL in the back office).      |
| UNIT      | string (10)      | The unit of measure for the item. Examples include gallons and ounces (oz.).      |
| UNITPRICE      | double (32 6)      | The price per unit.      |
| UNITQUANTITY      | double (32 6)      | The quantity of units that was sold.      |
| VARIANTNUMBER      | string (10)      | The ID for the unit combination of color, size, and style.      |
| ISWEIGHTPRODUCT      | int      | A value that indicates whether the connected scale is used to get the quantity.      |
| ISWEIGHTMANUALLYENTERED      | int      | If a scale isn't connected, the cashier can manually enter the weight.      |
| CATEGORYNAME      | string (254)  NOT NULL      | The name of the product category.      |
| CATEGORYHIERARCHYNAME      | string (128)      | The category hierarchy that is used to organize products.      |
| LOGISTICSPOSTALADDRESSVALIDFROM      | datetime      | The effective date of the address ID.      |
| LOGISTICLOCATIONID      | string (30)      | The address ID in the global address book.      |
| OPERATINGUNITNUMBER      | string (30)  NOT NULL      | The part of the reference data that comprises a store.      |
| RETURNOPERATINGUNITNUMBER      | string (30)      | The store where the return is being processed.      |
| ITEMCOLOR      | string (25)      | The color.      |
| ITEMSIZE      | string (10)      | The size.      |
| ITEMSTYLE      | string (10)      | The style. Like color and size, style is a product dimension.      |
| ITEMCONFIGID      | string (50)      | The configuration ID for kits.      |
| SKIPREPORTS      | int      | If this field is set, the record is skipped in reports.      |
| LINEPERCENTAGEDISCOUNT      | double (32 6)      | The amount of the automatic percentage discount.      |
| DISCOUNTAMOUNTWITHOUTTAX      | double (32 6) NOT NULL      | The discount amount, excluding tax.      |
| PARTITION      | string (20) NOT NULL      | The identifier of a data partition in Dynamics 365 Commerce that is specific to Dynamics 365.      |
| DATAAREAID      | string (4) NOT NULL      | The company identifier (for example, MSFT).      |
| SYNCSTARTDATETIME      | datetime NOT NULL      | Fields that are added to the synchronization engine (DIXF) in Dynamics 365 Commerce. They define the export sequence.      |

## Payments

| Field Name                       | Data Type                | Description |
|----------------------------------|--------------------------|-------------|
| DEFINITIONGROUP      | string (60)      | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Commerce. They define the export sequence.      |
| EXECUTIONID      | string (90)      | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Commerce. They define the export sequence.      |
| ISSELECTED      | int      | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Commerce. They define the export sequence.      |
| TRANSFERSTATUS      | int      | This field is used to track the status of transfers between warehouses.  |
| AMOUNTINTENDEREDCURRENCY      | double (32 6)      | The amount that was tendered in local currency as it applies to the country/region where the store is located.      |
| AMOUNTINACCOUNTINGCURRENCY      | double (32 6) NOT NULL      | The amount that is due for the line.      |
| AMOUNTTENDERED      | double (32 6) NOT NULL      | The amount in the store currency.      |
| MERCHANTPAYMENTINSTRUMENTTYPEID      | string (10)      | The name of the payment instrument (for example, AMEX or VISA).      |
| ISCHANGELINE      | int      | This field indicates if payment amount that is due back to the customer.    |
| CREDITVOUCHERID      | string (30)      | If a voucher is used for payment, the voucher number.      |
| CURRENCYCODE      | string (3)      | The currency that was paid.      |
| EXCHANGERATEINTENDEREDCURRENCY      | double (32 16)      | The exchange rate in relation to USD.      |
| EXCHANGERATEINACCOUNTINGCURRENCY      | double (32 16)      | The exchange rate in relation to US dollars (USD).      |
| GIFTCARDID      | string (30)      | The gift card number.      |
| ISPREPAYMENT      | int NOT NULL      | A value that indicates whether the payment is a deposit.      |
| LINENUMBER      | double (32 16) NOT NULL      | The payment line number.      |
| LOYALTYCARDID      | string (30)      | If loyalty points are used for payment, the card number that was provided.      |
| QUANTITY      | double (32 6) NOT NULL      | The number of units that were sold.      |
| RECEIPTID      | string (18)  NOT NULL      | The receipt ID. This ID differs from the transaction ID.      |
| TENDERTYPE      | string (10) NOT NULL      | The type of tender that was paid.      |
| TERMINAL      | string (10) NOT NULL      | The identifier of the register or Point of Sale (POS).      |
| TRANSACTIONNUMBER      | string (44) NOT NULL      | The transaction number.      |
| TRANSACTIONSTATUS      | int NOT NULL      | The status of the payment line.      |
| OPERATINGUNITNUMBER      | string (30) NOT NULL      | The operating unit that is unique to the store.      |
| MERCHANTPAYMENTINSTRUMENTID      | string (30)      | The identifier of the payment instrument. This information is provided by the merchant.      |
| ACCOUNTNUMBER      | string (30)      | The customer account number, if a named customer appears on the transaction.      |
| VOIDSTATUS      | int NOT NULL      | A value that indicates whether a tender line was voided before the transaction was tendered.      |
| AMOUNTTENDEREDADJUSTMENT      | double (32 6) NOT NULL      | A new feature in the product allows for changes to the transactions and provides a full audit trail.      |
| STAFF      | string (25)  NOT NULL      | The user ID.      |
| PARTITION      | string (20) NOT NULL      | The identifier of a data partition in Dynamics 365 Commerce that is specific to Dynamics 365.      |
| DATAAREAID      | string (4) NOT NULL      | The company identifier (for example, MSFT).      |
| SYNCSTARTDATETIME      | datetime NOT NULL      | Fields that are added to the synchronization engine (DIXF) in Dynamics 365 Commerce. They define the export sequence.      |

## PaymentMethod

| Field Name          | Data Type              | Description |
|---------------------|------------------------|-------------|
| PAYMENTMETHODNUMBER      | string (10) NOT NULL      | The identifier for the payment method.       |
| DEFAULTFUNCTION          | string                      | The identifier for the payment method.       |
| NAME                     | string (60) NOT NULL      | The descriptive name for the payment method. |

