---
author: josaw1
description: This article outlines data schemas for loss prevention in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Data schemas for loss prevention
---

# Data schemas for loss prevention

[!include[deprecation](includes/deprecation.md)]

This article outlines the data schemas used to generate models and determine risk assessments.

Follow these requirements:

[!INCLUDE[data-upload-req](includes/data-upload-req.md)]

## Transactions

| Field name                      | Data type                       | Description |
|---------------------------------|---------------------------------|-------------|
| DEFINITIONGROUP      | string       | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Commerce. They define the export sequence.      |
| EXECUTIONID      | string       | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Commerce. They define the export sequence.      |
| ISSELECTED      | int      | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Commerce. They define the export sequence.      |
| TRANSFERSTATUS      | int      | This field is used to track the status of transfers between warehouses.  |
| BATCHID      | int      | The identifier for the batch or shift.      |
| TERMINAL      | string       | The identifier for the POS.      |
| AMOUNTPOSTEDTOACCOUNT      | double       | The amount that is posted to the account for general ledger (GL) posting.      |
| CHANNELREFERENCEID      | string       | An identifier that indicates the channel that is used for purchases in omni-channel scenarios for e-commerce merchants.      |
| COSTAMOUNT      | double       | The cost for items.      |
| CREATEDOFFLINE      | int      | This field indicates if the transaction was created offline without database connectivity.      |
| CURRENCY      | string       | The currency code (for example, USD).      |
| CUSTOMERACCOUNT      | string       | The account number.      |
| CUSTOMERDISCOUNTAMOUNT      | double       | The discount that is mapped to the customer and automatically applied for that customer.      |
| DISCOUNTAMOUNT      | double       | The discount amount, if any discounts are applied.      |
| DELIVERYMODE      | string       | The mode of delivery, if the transaction isn't a cash-and-carry transaction.      |
| TRANSACTIONSTATUS      | int        | Fields that are added to the synchronization engine (DIXF) in Dynamics 365 Commerce. They define the export sequence.      |
| EXCHANGERATE      | double       | The exchange rate, if a non-store currency was used for payment.      |
| GROSSAMOUNT      | double       | The total amount that is due before discounts are applied.     |
| INCOMEEXPENSEAMOUNT      | double       | This field indicates the adjustment amount to reflect drawer-related expenses if any.      |
| INFOCODEDISCOUNTGROUP      | string       | This is the information code associated with the discount applied.      |
| WAREHOUSE      | string       | The warehouse that is associated with a store.      |
| SITEID      | string       | This field is typically used for retail stores. It's used to organize the stores by region (for example, Northwest US stores).      |
| INVOICEID      | string       | This field is related to payments on customer accounts. It indicates the invoice that the customer is making a payment against.      |
| ITEMSPOSTED      | int      | The count of items that are part of the shipment that is posted.      |
| LOYALTYCARDID      | string       | The locality card number associated with the customer.      |
| NETAMOUNT      | double       | The price before discounts are applied.      |
| PAYMENTAMOUNT      | double       | The payment amount.      |
| POSTASSHIPMENT      | int      | This field indicates whether or not an item has an associated shipment.|
| RECEIPTID      | string       | The receipt number. This number differs from the transaction number.      |
| REFUNDRECEIPTID      | string       | If the transaction is a refund, the receipt ID for the original transaction.      |
| SALEISRETURNSALE      | int      | A value that indicates whether the sale is a return.      |
| SALESINVOICEAMOUNT      | double       | The amount of the sales invoice if the customer is picking up just a few items from an order.      |
| SALESORDERAMOUNT      | double       | The total amount for customer orders. (These orders differ from cash-and-carry transactions, because they have shipping details.)      |
| SALESORDERID      | string       | The order number, for orders that have shipping details.      |
| SALESPAYMENTDIFFERENCE      | double       | The difference amount after the customer makes a payment.      |
| SHIFT      | string       | The shift. A shift is a set of transactions during the day that cash and sales activity is calculated for. Shifts are useful for determining how much cash should be in the terminal.      |
| SHIPPINGDATEREQUESTED      | datetime      | The date when goods on the customer order should be shipped.      |
| STAFF      | string         | The ID of the point of sale (POS) user.      |
| TOACCOUNT      | int      | The amount that is being charged to the customer's account.      |
| TOTALDISCOUNTAMOUNT      | double       | The amount of the discount that is applied to the transaction total.      |
| TOTALMANUALDISCOUNTAMOUNT      | double       | This field indicates the total discount amount that is manually applied, not automatically calculated.      |
| TOTALMANUALDISCOUNTPERCENTAGE      | double       | The percentage of the manually applied total discount.      |
| TRANSACTIONNUMBER      | string        | The transaction identifier.      |
| TRANSACTIONDATE      | datetime      | The date.      |
| TRANSACTIONTIME      | int      | The time of the transaction.      |
| TRANSACTIONTYPE      | int      | A value that indicates whether the transaction is a cash-and-carry transaction or an order.      |
| LOGISTICSLOCATIONID      | string       | This field identifies the location to which the shipment is getting delivered to.      |
| LOGISTICSPOSTALCITY      | string       | The city where the item is delivered to.      |
| LOGISTICSPOSTALCOUNTY      | string       | The county where the item is delivered to.      |
| LOGISTICSPOSTALSTATE      | string       | The state where the item is delivered to.      |
| LOGISTICSPOSTALSTREET      | string       | The street where the item is delivered to.      |
| LOGISTICSPOSTALZIPCODE      | string       | The zip code where the item is delivered to.      |
| LOGISTICSPOSTALADDRESSVALIDFROM      | datetime      | Delivery address effectivity, based on the date when the address is valid for the delivery of items.      |
| LOGISTICPOSTALADDRESSVALIDTO      | datetime      | Delivery address effectivity, based on the date when the address is no longer valid for the delivery of items.      |
| OPERATINGUNITNUMBER      | string       | The business unit that the store is mapped to.      |
| COMMENT      | string       | A transaction-level comment.      |
| TAXCALCULATIONTYPE      | int      | A value that indicates whether tax is based on the store, customer, or destination.      |
| DISCOUNTAMOUNTWITHOUTTAX      | double       | The discount amount, excluding tax.      |
| NETPRICE      | double       | The number of lines on the transaction.      |
| RETAILNCREXPORTED      | int      | At the beginning of the roll-out, this field was used as a flag to push transactions to an NCR BOS system.      |
| PARTITION      | string       | The identifier of a data partition in Dynamics 365 Commerce that is specific to Dynamics 365.      |
| DATAAREAID      | string       | The identifier of the legal entity in Dynamics 365 Commerce.      |
| SYNCSTARTDATETIME      | datetime       | Fields that are added to the synchronization engine (DIXF) in Dynamics 365 Commerce. They define the export sequence.      |

## Sales

| Field Name                      | Data Type                | Description |
|---------------------------------|--------------------------|-------------|
| DEFINITIONGROUP      | string       | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Commerce. They define the export sequence.      |
| EXECUTIONID      | string       | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Commerce. They define the export sequence.      |
| ISSELECTED      | int      | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Commerce. They define the export sequence.      |
| TRANSFERSTATUS      | int       | This field is used to track the status of transfers between warehouses. |
| SALESTAXGROUP      | string       | The effective sales tax group for the transaction.      |
| ITEMSALESTAXGROUP      | string       | The effective sales tax group for the item.      |
| TERMINAL      | string       | The identifier for the POS.      |
| TRANSACTIONNUMBER      | string       | The transaction number      |
| BARCODE      | string       | The bar code that was scanned.      |
| COSTAMOUNT      | double       | The product cost.      |
| CURRENCY      | string       | The currency that is used for the sale (for example, USD).      |
| CUSTOMERACCOUNT      | string       | The customer account number.      |
| CUSTOMERDISCOUNT      | double       | The customer discount.      |
| CUSTOMERINVOICEDISCOUNTAMOUNT      | double       | The discount that is associated at the invoice level during fulfillment.      |
| CASHDISCOUNTAMOUNT      | double        | The amount of the cash discount, if a cash discount is applied.      |
| PRICEGROUPS      | string       | The price group that products and customers belong to.      |
| OFFERNUMBER      | string       | The unique identifier for the offer number.      |
| DISCOUNTAMOUNTFORPRINTING      | double       | The discount amount that is printed on the receipt.      |
| MODEOFDELIVERY      | string       | The method of delivery for the customer.      |
| ELECTRONICDELIVERYEMAIL      | string       | The email address.      |
| RETAILEMAILADDRESSCONTENT      | string       | The email address for the receipt.      |
| GIFTCARD      | int       | The gift card number.      |
| REASONCODEDISCOUNT      | double       | If a discount was applied, reason codes can be configured to prompt the cashier to select a reason.      |
| WAREHOUSE      | string       | Reference data for the store. This field indicates the physical location of the goods.      |
| SERIALNUMBER      | string       | The serial number for the product.      |
| SITEID      | string       | The category that the store belongs to (for example, PACNW).      |
| INVENTORYSTATUS      | int      | The status of the inventory levels.      |
| LOTID      | string       | This field isn't required.      |
| ITEMID      | string       | The product ID.      |
| PRODUCTSCANNED      | int      | This field indicates if the bar code in the product was scanned as part of the transaction.      |
| ITEMRELATION      | string       | A grouping of related items in a specific product group.      |
| KEYBOARDPRODUCTENTRY      | int      | This field indicates if the product ID was entered by the cashier manually on the keyboard at the POS.      |
| LINEDISCOUNT      | double       | The discount amount that is applied for the line item.      |
| LINEMANUALDISCOUNTAMOUNT      | double      | If the discount was manually entered, the discount amount.      |
| LINEMANUALDISCOUNTPERCENTAGE      | double       | If a manual percentage discount was applied, the discount percentage.      |
| LINENUMBER      | double       | The line number on the transaction.      |
| ISLINEDISCOUNTED      | int      | A value that indicates whether the transaction line is discounted.      |
| ISLINKEDPRODUCTNOTORIGINAL      | int      | This field indicates if there were any linked item within the same product group that were changed.      |
| CHANNELLISTINGID      | string       | This field applies only to e-commerce. It isn't required for retail stores.      |
| NETAMOUNT      | double        | The net amount for the transaction.      |
| NETAMOUNTINCLUSIVETAX      | double       | The net amount, including tax.      |
| NETPRICE      | double       | The net price for the line before discounts are applied.    |
| ISORIGINALOFLINKEDPRODUCTLIST      | int      | The default linked products.      |
| ORIGINALPRICE      | double       | The product price when sale pricing isn't applied.   |
| ORIGINALSALESTAXGROUP      | string       | The original sales tax group for the transaction.      |
| ORIGINALITEMSALESTAXGROUP      | string       | If tax is overridden, this field tracks the original tax amount.      |
| PERIODICDISCOUNTAMOUNT      | double       | The discount amount for the periodic discount.      |
| PERIODICDISCOUNTGROUP      | string       | The periodic discount group.      |
| PERIODICDISCOUNTPERCENTAGE      | double       | The periodic discount percentage.      |
| PRICE      | double       | The price of the item.      |
| ISPRICECHANGE      | int       | This field indicates if there were any prices changes made manually to the list of products in the transaction.      |
| PRICEINBARCODE      | int      | This field indicates if a price-embedded bar code was scanned for a specific product within the transaction.      |
| QUANTITY      | double       | The quantity.      |
| REQUESTEDRECEIPTDATE      | datetime       | For customer orders, the date when the customer has requested arrival/pickup.      |
| RECEIPTNUMBER      | string       | The receipt number.      |
| RETURNLINENUMBER      | double       | The line number from the original transaction when the return is done from the journal.      |
| ISRETURNNOSALE      | int      | A value that indicates whether this transaction is a return or void.      |
| RETURNQUANTITY      | double      | The quantity that is being returned.      |
| RETURNTERMINAL      | string       | The terminal where the return transaction is being processed.      |
| RETURNTRANSACTIONNUMBER      | string       | Original transaction number when the return is done from the receipt or journal.      |
| RFIDTAGID      | string       | The identifier for radio frequency identification (RFID).      |
| ISSCALEPRODUCT      | int      | A value that indicates whether the connected scale is used to get the quantity.      |
| SECTIONNUMBER      | string       | The physical location of the product in the store. This field isn't used.      |
| SHELFNUMBER      | string       | The shelf number where the product is kept.      |
| REQUESTEDSHIPDATE      | datetime      | The requested shipping date for the order.      |
| STANDARDNETPRICE      | double       | The price, excluding discounts and trade agreements.      |
| SALESTAXAMOUNT      | double       | The amount of sales tax that is applied to the transaction.      |
| TOTALDISCOUNT      | double       | The amount of the discount that is applied to the order total.      |
| TOTALDISCOUNTINFOCODELINENUM      | double       | If the user is prompted for an info code when a total discount is applied, the reason code is saved in this field.      |
| TOTALDISCOUNTPERCENTAGE      | double       | The discount percentage that is applied to the transaction total, if a total discount by percentage is used.      |
| TRANSACTIONCODE      | int      | An indicator of the transaction type.      |
| TRANSACTIONSTATUS      | int       | A value of Posted indicates that the statement has been completed (that is, amounts have reached the GL in the back office).      |
| UNIT      | string       | The unit of measure for the item. Examples include gallons and ounces (oz.).      |
| UNITPRICE      | double       | The price per unit.      |
| UNITQUANTITY      | double       | The quantity of units that was sold.      |
| VARIANTNUMBER      | string       | The ID for the unit combination of color, size, and style.      |
| ISWEIGHTPRODUCT      | int      | A value that indicates whether the connected scale is used to get the quantity.      |
| ISWEIGHTMANUALLYENTERED      | int      | If a scale isn't connected, the cashier can manually enter the weight.      |
| CATEGORYNAME      | string       | The name of the product category.      |
| CATEGORYHIERARCHYNAME      | string       | The category hierarchy that is used to organize products.      |
| LOGISTICSPOSTALADDRESSVALIDFROM      | datetime      | The effective date of the address ID.      |
| LOGISTICLOCATIONID      | string       | The address ID in the global address book.      |
| OPERATINGUNITNUMBER      | string       | The part of the reference data that comprises a store.      |
| RETURNOPERATINGUNITNUMBER      | string       | The store where the return is being processed.      |
| ITEMCOLOR      | string      | The color.      |
| ITEMSIZE      | string       | The size.      |
| ITEMSTYLE      | string       | The style. Like color and size, style is a product dimension.      |
| ITEMCONFIGID      | string      | The configuration ID for kits.      |
| SKIPREPORTS      | int      | If this field is set, the record is skipped in reports.      |
| LINEPERCENTAGEDISCOUNT      | double       | The amount of the automatic percentage discount.      |
| DISCOUNTAMOUNTWITHOUTTAX      | double        | The discount amount, excluding tax.      |
| PARTITION      | string       | The identifier of a data partition in Dynamics 365 Commerce that is specific to Dynamics 365.      |
| DATAAREAID      | string       | The company identifier (for example, MSFT).      |
| SYNCSTARTDATETIME      | datetime       | Fields that are added to the synchronization engine (DIXF) in Dynamics 365 Commerce. They define the export sequence.      |

## Payments

| Field Name                       | Data Type                | Description |
|----------------------------------|--------------------------|-------------|
| DEFINITIONGROUP      | string       | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Commerce. They define the export sequence.      |
| EXECUTIONID      | string       | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Commerce. They define the export sequence.      |
| ISSELECTED      | int      | Fields that are added by the synchronization engine (DIFX) in Dynamics 365 Commerce. They define the export sequence.      |
| TRANSFERSTATUS      | int      | This field is used to track the status of transfers between warehouses.  |
| AMOUNTINTENDEREDCURRENCY      | double       | The amount that was tendered in local currency as it applies to the country/region where the store is located.      |
| AMOUNTINACCOUNTINGCURRENCY      | double       | The amount that is due for the line.      |
| AMOUNTTENDERED      | double       | The amount in the store currency.      |
| MERCHANTPAYMENTINSTRUMENTTYPEID      | string       | The name of the payment instrument (for example, AMEX or VISA).      |
| ISCHANGELINE      | int      | This field indicates if payment amount that is due back to the customer.    |
| CREDITVOUCHERID      | string       | If a voucher is used for payment, the voucher number.      |
| CURRENCYCODE      | string       | The currency that was paid.      |
| EXCHANGERATEINTENDEREDCURRENCY      | double       | The exchange rate in relation to USD.      |
| EXCHANGERATEINACCOUNTINGCURRENCY      | double       | The exchange rate in relation to US dollars (USD).      |
| GIFTCARDID      | string       | The gift card number.      |
| ISPREPAYMENT      | int       | A value that indicates whether the payment is a deposit.      |
| LINENUMBER      | double       | The payment line number.      |
| LOYALTYCARDID      | string       | If loyalty points are used for payment, the card number that was provided.      |
| QUANTITY      | double       | The number of units that were sold.      |
| RECEIPTID      | string       | The receipt ID. This ID differs from the transaction ID.      |
| TENDERTYPE      | string       | The type of tender that was paid.      |
| TERMINAL      | string       | The identifier of the register or Point of Sale (POS).      |
| TRANSACTIONNUMBER      | string       | The transaction number.      |
| TRANSACTIONSTATUS      | int       | The status of the payment line.      |
| OPERATINGUNITNUMBER      | string       | The operating unit that is unique to the store.      |
| MERCHANTPAYMENTINSTRUMENTID      | string       | The identifier of the payment instrument. This information is provided by the merchant.      |
| ACCOUNTNUMBER      | string       | The customer account number, if a named customer appears on the transaction.      |
| VOIDSTATUS      | int       | A value that indicates whether a tender line was voided before the transaction was tendered.      |
| AMOUNTTENDEREDADJUSTMENT      | double       | A new feature in the product allows for changes to the transactions and provides a full audit trail.      |
| STAFF      | string       | The user ID.      |
| PARTITION      | string       | The identifier of a data partition in Dynamics 365 Commerce that is specific to Dynamics 365.      |
| DATAAREAID      | string       | The company identifier (for example, MSFT).      |
| SYNCSTARTDATETIME      | datetime      | Fields that are added to the synchronization engine (DIXF) in Dynamics 365 Commerce. They define the export sequence.      |

## PaymentMethod

| Field Name          | Data Type              | Description |
|---------------------|------------------------|-------------|
| PAYMENTMETHODNUMBER      | string       | The identifier for the payment method.       |
| DEFAULTFUNCTION          | string       | A description of the type of payment method, such as Cash, Check, Credit Memo/Voucher, or Currency.       |
| NAME                     | string       | The descriptive name for the payment method. |



[!INCLUDE[footer-include](includes/footer-banner.md)]
