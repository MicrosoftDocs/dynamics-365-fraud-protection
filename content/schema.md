---
author: jegrif
description: View schemas
ms.author: v-jegrif
ms.service: fraud-protection
ms.date: 02/25/2019
- crm-online
ms.topic: conceptual
title: View schemas
---


# View schemas
The following document outlines the required schemas for historical data that will be bulk uploaded into Dynamics 365 Fraud Protection as CSV files. Please see [Data upload](data-upload.md) for guidelines on the upload procedure. For data to be ingested via the API, see [Send real-time data](send-real-time-api.md).

Note that all DateTime fields are formatted in ISO8601. Example: DateTime.UtcNow.ToString("o"), with a result of "2019-03-14T20:18:11.254Z". 

## Transactions
Used in the Diagnose, Evaluate, and Protect experiences.

### Purchases

| Attribute	            | Type      | Description                                                                                    |
| --------------------- | --------- | ---------------------------------------------------------------------------------------------- |
| PurchaseId            | string    | Transaction (or purchase/order) identifier.                                                    |
| OriginalOrderId	      | string    | Original order identifier for payments of recurring billing, like subscription monthly billing.|
| CustomerLocalDate	    | DateTime  | Purchase creation date per customer local time zone. Format is ISO8601.                        |
| MerchantLocalDate     |	DateTime  |	Purchase ingestion date per merchant time zone. Format is ISO8601.                             |
| TotalAmount           |	double	   | Total amount charged to the customer; tax included. Provided by merchant.                      |
| SalesTax	             | double	   | Sales tax charged for the transaction. Provided by merchant.                                   |
| Currency	             | string	   | Currency of the original purchase. 3-character currency code (for example, USD, aligns with OANDA currency code). Provided by merchant. |
| DeviceContextId	      | string    |	Session ID of the particular event's session (provided by Microsoft Device Fingerprinting) or the transaction ID if session is not available. |
| IPAddress	            | string    |	Customer's IP address (provided by Microsoft Device Fingerprinting).                           |
| UserId	               | string	   | Customer identifier provided by merchant.                                                      | 
| UserFirstName         |	string	   | Customer-provided first name on customer account.                                              | 
| UserLastName         	| string   	| Customer-provided last name on customer account.                                               |
| UserEmail             |	string	   | Email of customer. Case insensitive.                                                           |
| UserCreationDate     	| DateTime	 | Customer account creation date. Format is ISO8601.                                             |  
| UserUpdateDate       	| DateTime 	| Latest date customer data has changed. Format is ISO8601.                                      | 
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
| PurchaseAmount               | double     | Total purchase amount using this PI for the transaction.                               |
| CreationDate                 | DateTime   | First entry date for PI in merchant system. Format is ISO8601.                         |
| UpdateDate                   | DateTime   | Latest update date for PI in merchant system. Format is ISO8601.                       |
| CardType                     | string     | For CREDITCARD only.                                                                   |
| HolderName                   | string     | Name of the customer of the PI. For CREDITCARD only.                                   |
| BIN                          | string     | For CREDITCARD only.                                                                   |
| ExpirationDate               | string   | Expiration date for PI in merchant system. For CREDITCARD only. Format is ISO8601.     |
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
| PurchasePrice	               | double	    | Price for line item of purchase.                                                       |
| Margin		                     | string	    | Margin gained by sale of item.                                                         |
| Quantity		                   | Int32 	    | Number of items purchased.                                                             |
| ProductName		                | string	    | Customer-readable product name.                                                        |
| Type       		                | string	    | Denotes physical or digital goods.                                                     |
| Category		                   | string	    | Category of product (for example, Apparel, Shoes, Accessories).                        |
| Market		                     | string     | Market in which product is offered. ISO, 2-character country code (for example, US).   |
| Sku		                        | string	    | Product SKU.                                                                           |
| SalesPrice	                  | double	    | Price of item sold (not including tax). Provided by merchant.                          |
| COGS		                       | string	    | Cost of Goods Sold – raw material cost of item. Provided by merchant.                  |
| IsRecurring	                 | bool	      | Indicates whether product is recurring subscription.                                   |
| IsFree		                     | bool	      | Indicates whether product is offered for free.                                         |
| Language                     | string     | Locale, Language-Territory (for example, EN-US).                                       |



## Chargebacks
Used in the Diagnose, Evaluate, and Protect experiences.

| Attribute	                   | Type       | Description                                                                            |
| ---------------------------- | ---------- | -------------------------------------------------------------------------------------- |
| chargebackId                 | string	    | Chargeback identifier.                                                                 |
| reason	                      | string	    | Reason provided by bank.                                                               |
| status	                      | string	    | Status. "INITIATED", "LOST", "WON"                                                     |
| bankEventTimestamp           | DateTime   | Timestamp from bank. Format is ISO8601.                                                |
| amount	                      | double	    | Chargeback amount.                                                                     |
| currency                     | string	    | Currency used for chargeback amount.                                                   |
| userId  	                    | string	    | Customer identifier.                                                                   |
| purchaseId  	                | string	    | Transaction (or purchase/order) identifier.                                            |
| merchantLocalDate            | DateTime   | Purchase ingestion date per merchant time zone. Format is ISO8601.                     |


## Refunds
Used in the Evaluate and Protect experiences.

| Attribute	                   | Type       | Description                                                                            |
| ---------------------------- | ---------- | -------------------------------------------------------------------------------------- |
| refundId                     | string     | Refund identifier.                                                                     |
| reason	                      | string	    | Customer-provided reason.                                                              |
| status	                      | string	    | Refund status. "INITIATED", "COMPLETED"                                                |
| bankEventTimestamp           | DateTime   | Timestamp from bank. Format is ISO8601.                                                |
| amount	                      | double	    | Refund amount.                                                                         |
| currency: 	                  | string	    | Currency used for sales price amount.                                                  |
| userId: 	                    | string	    | Customer identifier.                                                                   |
| purchaseId: 	                | string	    | Transaction (or purchase/order) identifier.                                            |
| merchantLocalDate            | DateTime   | Format is ISO8601.                                                                     |

## Purchase status
Used in the Evaluate and Protect experiences.

| Attribute	                   | Type       | Description                                                                            |
| ---------------------------- | ---------- | -------------------------------------------------------------------------------------- |
| purchaseId                   | string     | Transaction (or purchase/order) identifier.                                            |
| statusType                   | string     | Type of status. "APPROVED", "CANCELED", "HELD", "FULFILLED"                            |
| statusDate                   | DateTime   | DateTime when status was applied. Format is ISO8601.                                   |
| reason	                      | string	    | Reason for status transition.                                                          |
| merchantLocalDate            | DateTime   | Format is ISO8601.                                                                     |

## Bank events
Used in the Evaluate and Protect experiences.

| Attribute	                   | Type       | Description                                                                            |
| ---------------------------- | ---------- | -------------------------------------------------------------------------------------- |
| bankEventId                  | string	    | Bank event identifier.                                                                 |
| type                         | string	    | Bank event type. "AUTH", "CHARGE"                                                      |
| bankEventTimestamp           | DateTime   | Timestamp from bank. Format is ISO8601.                                                |
| status                       | string	    | Status.  "APPROVED", "REJECTED"                                                        |
| bankResponseCode             | string	    | Bank code on response.                                                                 |
| paymentProcessor             | string	    | Processor name. "FDC", "PAYPAL", …                                                     |
| mrn                          | string	    | Merchant Reference Number used to identify the transaction from the merchant side.     |
| mid                          | string	    | MID used for bank communication.                                                       |
| purchaseId                   | string	    | Transaction (or purchase/order) identifier.                                            |
| merchantLocalDate            | DateTime   | Format is ISO8601.                                                                     |

## Account
Used in the Evaluate and Protect experiences.

### Update account

| Attribute	                   | Type       | Description                                                                            |
| ---------------------------- | ---------- | -------------------------------------------------------------------------------------- |
| customerLocalDate            | DateTime   | Format is ISO8601.                                                                     |
| userId                       | string	    | Customer identifier.                                                                   |
| usercreationDate             | DateTime   | Format is ISO8601.                                                                     |
| userupdateDate               | DateTime   | Format is ISO8601.                                                                     |
| firstName                    | string	    | Customer-provided first name on customer account.                                      |
| lastName                     | string	    | Customer-provided last name on customer account.                                       |
| country                      | string	    | Country of customer. 2 alpha country code, e.g., "US"                                  |
| zipCode                      | string	    | Postal code of customer.                                                               |
| timeZone                     | string	    | deprecated. Please provide empty string                                                |
| language                     | string	    | Language of customer. Locale, Language-Territory (for example, EN-US).                 |
| phoneNumber                  | string	    | Phone number of customer. Country code followed by phone number; with the country code and phone number separated by ‘-’ (for example, for US - +1-1234567890). |
| email                        | string	    | Email of customer. Case insensitive.                                                   |
| isEmailValidated             | bool	      | Whether customer-provided email has been verified to be owned by the customer.         |
| emailValidatedDate           | DateTime   | Date when customer-provided email has been verified to be owned by the customer. Format is ISO8601.    |
| isPhoneNumberValidated       | bool	      | Whether customer-provided phone number has been verified to be owned by the customer.  |
| phoneNumberValidatedDate     | DateTime   | Date when customer-provided phone number date has been verified to be owned by the customer. Format is ISO8601.  |
| deviceContextId              | string	    | Session ID of the particular event's session (provided by Microsoft Device Fingerprinting) or the transaction ID if session is not available.  |
| provider                     | string	    | Indicates whether "deviceContextId" is from "DFP Fingerprinting" or "Merchant"         |
| deviceContextDC              | string	    | Microsoft Device Fingerprinting Datacenter for the customer’s session ID.              |
| externalDeviceId             | string	    | Customer’s device ID (provided and mastered by merchant).                              |
| externalDeviceType           | string	    | Device Type, identified by Merchant, e.g., "PC", "Mobile Device", etc.                 |
| ipAddress                    | string	    | Customer’s IP address (provided by Microsoft Device Fingerprinting).                   |
| merchantLocalDate            | DateTime   | Format is ISO8601.                                                                     |

### Update address
| Attribute	                   | Type       | Description                                                                            |
| ---------------------------- | ---------- | -------------------------------------------------------------------------------------- |
| userId                       | string	    | Customer identifier.                                                                   |
| addresstype                  | string	    | Address type.  "BILLING", "SHIPPING", "ACCOUNT"                                        |
| firstName                    | string	    | First name provided with address.                                                      |
| lastName                     | string	    | Last name provided with address.                                                       |
| phoneNumber                  | string	    | Phone number provided with address.                                                    |
| street1                      | string	    | First row provided with address.                                                       |
| street2                      | string	    | Second row provided with address (may be blank).                                       |
| street3                      | string	    | Third row provided with address (may be blank).                                        |
| city                         | string	    | City provided with address.                                                            |
| state                        | string	    | State/Region provided with address.                                                    |
| district                     | string	    | District provided with address (may be blank).                                         |
| zipCode                      | string	    | Zip code provided with address.                                                        |
| country                      | string	    | ISO country code provided with address. 2 alpha country code, e.g., “US”               |

### Update payment instrument

| Attribute	                    | Type       | Description                                                                            |
| ----------------------------- | ---------- | -------------------------------------------------------------------------------------- |
| userId                        | string	    | Customer identifier.                                                                   |
| merchantPaymentInstrumentId   | string	    | PaymentInstrument Identifier provided by merchant.                                     |
| PaymentInstrumenttype         | string	    | Type of payment. "CreditCard", "Paypal", "Mobilepayment", "Giftcard"                   |
| PaymentInstrumentcreationDate | DateTime   | First entry date for PI in merchant system. Format is ISO8601.                         |
| PaymentInstrumentupdateDate   | DateTime   | Latest update date for PI in merchant system. Format is ISO8601.                       |
| PaymentInstrumentState        | string	    | State of the PI. "Active", "Block", "Expire"                                           |
| cardType                      | string	    | For CREDITCARD only.                                                                   |
| holderName                    | string	    | Name of the customer of the PI. For CREDITCARD only.                                   |
| bin                           | string	    | For CREDITCARD only.                                                                   |
| expirationDate                | string	    | Expiration date for PI in merchant system. For CREDITCARD only.                        |
| lastFourDigits                | string	    | For CREDITCARD only.                                                                   |
| email                         | string	    | Email associated with the PI. For PAYPAL only.                                         |
| billingAgreementId            | string	    | For PAYPAL only.                                                                       |
| payerId                       | string	    | For PAYPAL only.                                                                       |
| payerStatus                   | string	    | Indicates whether PayPal has verified the payer. For PAYPAL only.                      |
| addressStatus                 | string	    | Indicates whether PayPal has verified the payer’s address. For PAYPAL only.            |
| imei                          | string	    | For MOBILEPAYMENT only.                                                                |
| BillingAddressfirstName       | string	    | First name provided with address.                                                      |
| BillingAddresslastName        | string	    | Last name provided with address.                                                       |
| BillingAddressphoneNumber     | string	    | Phone number provided with address. Country code followed by phone number; with the country code and phone number separated by ‘-’ (for example, for US - +1-1234567890). |
| street1                       | string	    | First row provided with address (may be blank).                                        |
| street2                       | string	    | Second row provided with address (may be blank).                                       |
| street3                       | string	    | Third row provided with address (may be blank).                                        |
| city                          | string	    | City provided with address.                                                            |
| state                         | string	    | State/Region provided with address.                                                    |
| district                      | string	    | District provided with address (may be blank).                                         |
| zipCode                       | string	    | Zip code provided with address.                                                        |
| country                       | string	    | ISO country code provided with address. 2 alpha country code, e.g., "US"               |
