---
author: jegrif
description: Schema
ms.author: v-jegrif
ms.date: 02/25/2019
ms.service:
 - d365-fraud-protection
ms.topic: conceptual
title: Schema
---


# Schemas
The following document outlines the required schemas for data that will be manually uploaded into Dynamics 365 Fraud Protection.

## Transactions
Used in the Diagnose, Evaluate, and Protect experiences.

### Purchase

| Attribute	            | Type      | Description                                                                                    |
| --------------------- | --------- | ---------------------------------------------------------------------------------------------- |
| PurchaseId            | string    | Transaction (or purchase/order) identifier.                                                    |
| OriginalOrderId	      | string    | Original order identifier for payments of recurring billing, like subscription monthly billing.|
| CustomerLocalDate	    | DateTime  | Purchase creation date per customer local time zone. Format is ISO8601.                        |
| MerchantLocalDate     |	DateTime  |	Purchase ingestion date per merchant time zone. Format is ISO8601. "2019-03-14T20:18:11.254Z"  |
| TotalAmount           |	string	   | Total amount charged to the customer; tax included. Provided by merchant.                      |
| SalesTax	             | string	   | Sales tax charged for the transaction. Provided by merchant.                                   |
| Currency	             | string	   | Currency of the original purchase. 3-character currency code (for example, USD, aligns with OANDA currency code). Provided by merchant. |
| DeviceContextId	      | string    |	Session ID of the particular event's session (provided by Microsoft Device Fingerprinting) or the transaction ID if session is not available. |
| IPAddress	            | string    |	Customer's IP address (provided by Microsoft Device Fingerprinting).                           |
| UserId	               | string	   | Customer identifier provided by merchant.                                                      | 
| UserFirstName         |	string	   | Customer-provided first name on customer account.                                              | 
| UserLastName         	| string   	| Customer-provided last name on customer account.                                               |
| UserEmail             |	string	   | Email of customer. Case insensitive.                                                           |
| UserCreationDate     	| DateTime	 | Customer account creation date.                                                                |  
| UserUpdateDate       	| DateTime 	| Latest date customer data has changed.                                                         | 
| UserZipCode          	| string	   | Postal code of customer.                                                                       | 
| UserCountry          	| string	   | Country of customer. 2 alpha country code, e.g., "US"                                          | 
| UserTimeZone         	| string   	| Empty string                                                                                   | 
| UserLanguage         	| string   	| Language of customer. Locale, Language-Territory (for example, EN-US).                         | 
| UserPhoneNumber      	| string	   | Phone number of customer. Country code followed by phone number, with the country code and phone number separated by ‘-’ (for example, for US - +1-1234567890). | 
| IsEmailValidated	     | bool	     | Whether customer-provided email has been verified to be owned by the customer. (True or False) | 
| ShippingFirstName    	| string	   | First name provided with address.                                                              | 
| ShippingLastName	     | string   	| Last name provided with address.                                                               | 
| ShippingPhoneNumber  	| string	   | Phone number provided with address. Country code followed by phone number, with the country code and phone number separated by ‘-’ (for example, for US - +1-1234567890). | 
| Street1              	| string	   | First row provided with address.                                                               | 
| Street2	              | string   	| Second row provided with address (may be blank).                                               | 
| Street3	              | string   	| Third row provided with address (may be blank).                                                | 
| City	                 | string	   | City provided with address.                                                                    | 
| State	                | string	   | State/Region provided with address.                                                            | 
| ZipCode	              | string	   | Zip code provided with address.                                                                | 
| Country	              | string	   | ISO country code provided with address. 2 alpha country code, e.g., "US"                       | 



### Payment instruments

| Attribute	                   | Type       | Description                                                                            |
| ---------------------------- | ---------- | -------------------------------------------------------------------------------------- |
| PurchaseId                   | string     | Transaction (or purchase/order) identifier.                                            |
| MerchantPaymentInstrumentId  | string     | PaymentInstrument Identifier provided by merchant.                                     |
| Type                         | string     | Type of payment. "CreditCard", "Paypal", "Mobilepayment", "Giftcard"                   |
| PurchaseAmount               | string     | Total purchase amount using this PI for the transaction.                               |
| CreationDate                 | DateTime   | First entry date for PI in merchant system.                                            |
| UpdateDate                   | DateTime   | Latest update date for PI in merchant system.                                          |
| CardType                     | string     | For CREDITCARD only.                                                                   |
| HolderName                   | string     | Name of the customer of the PI. For CREDITCARD only.                                   |
| BIN                          | string     | For CREDITCARD only.                                                                   |
| ExpirationDate               | DateTime   | Expiration date for PI in merchant system. For CREDITCARD only.                        |
| LastFourDigits               | string     | For CREDITCARD only.                                                                   |
| Email                        | string     | Email associated with the PI. For PAYPAL only.                                         |
| BillingAgreementId           | string     | For PAYPAL only.                                                                       |
| PayerId                      | string     | For PAYPAL only.                                                                       |
| PayerStatus                  | string     | Indicates whether PayPal has verified the payer. For PAYPAL only.                      |
| AddressStatus                | string     | Indicates whether PayPal has verified the payer’s address. For PAYPAL only.            |
| IMEI                         | string     | For MOBILEPAYMENT only.                                                                |
| FirstName                    | string     | First name provided with address.                                                      |
| LastName                     | string     | Last name provided with address.                                                       |
| PhoneNumber                  | string     | Phone number provided with address. Country code followed by phone number, with the country code and phone number separated by ‘-’ (for example, for US - +1-1234567890). |
| Street1                      | string     | First row provided with address.                                                       |
| Street2                      | string     | Second row provided with address (may be blank).                                       |
| Street3                      | string     | Third row provided with address (may be blank).                                        |
| City                         | string     | City provided with address.                                                            |
| State                        | string     | State/Region provided with address.                                                    |
| ZipCode                      | string     | Zip code provided with address.                                                        |
| Country                      | string     | ISO country code provided with address. 2 alpha country code, e.g., "US"               |



### Products

| Attribute	                   | Type       | Description                                                                            |
| ---------------------------- | ---------- | -------------------------------------------------------------------------------------- |
| PurchaseId     	             | string	    | Transaction (or purchase/order) identifier.                                            |
| ProductId	                   | string	    | Product identifier.                                                                    |
| PurchasePrice	               | string	    | 	Price for line item of purchase.                                                      |
| Margin		                     | string	    | 	Margin gained by sale of item.                                                        |
| Quantity		                   | string	    | 	Number of items purchased.                                                            |
| ProductName		                | string	    | 	Customer-readable product name.                                                       |
| Category		                   | string	    | 	Category of product (for example, Apparel, Shoes, Accessories).                       |
| Market		                     | string     | Market in which product is offered. ISO, 2-character country code (for example, US).   |
| Sku		                        | string	    | Product SKU.                                                                           |
| SalesPrice	                  | string	    | Price of item sold (not including tax). Provided by merchant.                          |
| COGS		                       | string	    | 	Cost of Goods Sold – raw material cost of item. Provided by merchant.                 |
| IsRecurring	                 | bool	      | Indicates whether product is recurring subscription.                                   |
| IsFree		                     | bool	      | Indicates whether product is offered for free.                                         |

## Chargeback
Used in the Diagnose, Evaluate, and Protect experiences.

| Attribute	                   | Type       | Description                                                                            |
| ---------------------------- | ---------- | -------------------------------------------------------------------------------------- |
| chargebackId                 | string	    | Chargeback identifier.                                                                 |
| reason	                      | string	    | Reason provided by bank.                                                               |
| status	                      | string	    | Status. "INITIATED", "LOST", "WON"                                                     |
| bankEventTimestamp           | DateTime   | Timestamp from bank.                                                                   |
| amount	                      | string	    | Chargeback amount.                                                                     |
| currency: 	                  | string	    | Currency used for chargeback amount.                                                   |
| userId: 	                    | string	    | Customer identifier.                                                                   |
| purchaseId: 	                | string	    | Transaction (or purchase/order) identifier.                                            |
| merchantLocalDate:           | DateTime   | Purchase ingestion date per merchant time zone. Format is ISO8601.  "2019-03-14T20:18:11.254Z" |


## Refund
Used in the Evaluate and Protect experiences.

| Attribute	                   | Type       | Description                                                                            |
| ---------------------------- | ---------- | -------------------------------------------------------------------------------------- |
| refundId                     | string     |                                                                                        |
| reason	                      | string	    |                                                                                        |
| status	                      | string	    |                                                                                        |
| bankEventTimestamp           | DateTime   |                                                                                        |
| amount	                      | string	    |                                                                                        |
| currency: 	                  | string	    |                                                                                        |
| userId: 	                    | string	    |                                                                                        |
| purchaseId: 	                | string	    |                                                                                        |
| merchantLocalDate:           | DateTime   |                                                                                        |

## Purchase status
Used in the Evaluate and Protect experiences.

| Attribute	                   | Type       | Description                                                                            |
| ---------------------------- | ---------- | -------------------------------------------------------------------------------------- |
| purchaseId                   | string     |                                                                                        |
| statusType                   | string     |                                                                                        |
| statusDate                   | DateTime   |                                                                                        |
| reason	                      | string	    |                                                                                        |
| merchantLocalDate:           | DateTime   |                                                                                        |

## Bank event
Used in the Evaluate and Protect experiences.

| Attribute	                   | Type       | Description                                                                            |
| ---------------------------- | ---------- | -------------------------------------------------------------------------------------- |
| bankEventId                  | string	    |                                                                                        |
| type                         | string	    |                                                                                        |
| bankEventTimestamp           | DateTime   |                                                                                        |
| status                       | string	    |                                                                                        |
| bankResponseCode             | string	    |                                                                                        |
| paymentProcessor             | string	    |                                                                                        |
| mrn                          | string	    |                                                                                        |
| mid                          | string	    |                                                                                        |
| purchaseId                   | string	    |                                                                                        |
| merchantLocalDate            | DateTime   |                                                                                        |

## Account
Used in the Evaluate and Protect experiences.

### Update account

| Attribute	                   | Type       | Description                                                                            |
| ---------------------------- | ---------- | -------------------------------------------------------------------------------------- |
| customerLocalDate            | DateTime   |                                                                                        |
| userId                       | string	    |                                                                                        |
| usercreationDate             | DateTime   |                                                                                        |
| userupdateDate               | DateTime   |                                                                                        |
| firstName                    | string	    |                                                                                        |
| lastName                     | string	    |                                                                                        |
| country                      | string	    |                                                                                        |
| zipCode                      | string	    |                                                                                        |
| timeZone                     | string	    |                                                                                        |
| language                     | string	    |                                                                                        |
| phoneNumber                  | string	    |                                                                                        |
| email                        | string	    |                                                                                        |
| isEmailValidated             | bool	      |                                                                                        |
| emailValidatedDate           | DateTime   |                                                                                        |
| isPhoneNumberValidated       | bool	      |                                                                                        |
| phoneNumberValidatedDate     | DateTime   |                                                                                        |
| deviceContextId              | string	    |                                                                                        |
| provider                     | string	    |                                                                                        |
| deviceContextDC              | string	    |                                                                                        |
| externalDeviceId             | string	    |                                                                                        |
| externalDeviceType           | string	    |                                                                                        |
| ipAddress                    | string	    |                                                                                        |
| merchantLocalDate            | DateTime   |                                                                                        |

### Update address
| Attribute	                   | Type       | Description                                                                            |
| ---------------------------- | ---------- | -------------------------------------------------------------------------------------- |
| userId                       | string	    |                                                                                        |
| addresstype                  | string	    |                                                                                        |
| firstName                    | string	    |                                                                                        |
| lastName                     | string	    |                                                                                        |
| phoneNumber                  | string	    |                                                                                        |
| street1                      | string	    |                                                                                        |
| street2                      | string	    |                                                                                        |
| street3                      | string	    |                                                                                        |
| city                         | string	    |                                                                                        |
| state                        | string	    |                                                                                        |
| district                     | string	    |                                                                                        |
| zipCode                      | string	    |                                                                                        |
| country                      | string	    |                                                                                        |

### Update payment instruments

| Attribute	                    | Type       | Description                                                                            |
| ----------------------------- | ---------- | -------------------------------------------------------------------------------------- |
| userId                        | string	    |                                                                                        |
| merchantPaymentInstrumentId   | string	    |                                                                                        |
| PaymentInstrumenttype         | string	    |                                                                                        |
| PaymentInstrumentcreationDate | DateTime   |                                                                                        |
| PaymentInstrumentupdateDate   | DateTime   |                                                                                        |
| state                         | string	    |                                                                                        |
| cardType                      | string	    |                                                                                        |
| holderName                    | string	    |                                                                                        |
| bin                           | string	    |                                                                                        |
| expirationDate                | string	    |                                                                                        |
| lastFourDigits                | string	    |                                                                                        |
| email                         | string	    |                                                                                        |
| billingAgreementId            | string	    |                                                                                        |
| payerId                       | string	    |                                                                                        |
| payerStatus                   | string	    |                                                                                        |
| addressStatus                 | string	    |                                                                                        |
| imei                          | string	    |                                                                                        |
| billingAddress                | string	    |                                                                                        |
| BillingAddressfirstName       | string	    |                                                                                        |
| BillingAddresslastName        | string	    |                                                                                        |
| BillingAddressphoneNumber     | string	    |                                                                                        |
| street1                       | string	    |                                                                                        |
| street2                       | string	    |                                                                                        |
| street3                       | string	    |                                                                                        |
| city                          | string	    |                                                                                        |
| state                         | string	    |                                                                                        |
| district                      | string	    |                                                                                        |
| zipCode                       | string	    |                                                                                        |
| country                       | string	    |                                                                                        |
