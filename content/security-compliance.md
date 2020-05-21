---
author: yvonnedeq
description: This topic provides information about security, compliance, and data subject requests.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 05/21/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Compliance


---

# Compliance

Microsoft Dynamics 365 Fraud Protection was designed with compliance, privacy, security, and confidentiality in mind and is only intended to be used to prevent fraud and help identify legitimate payment transactions. Microsoft offers Fraud Protection under the Microsoft Online Services Terms, which includes robust Data Protection Terms.

To review the Microsoft Online Services Terms, which include Fraud Protection-specific provisions, to determine if Fraud Protection meets your requirements, visit: https://www.microsoft.com/licensing/product-licensing/products.

It is your responsibility to:

- Inform your customers of your data processing practice, for example by disclosing the data you collect and how it is used. 
- Disclose your use of third parties working on your behalf to process the data you collect, including Fraud Protection service providers. 
- Comply with all laws and regulations applicable to the use of Fraud Protection, including data protection laws. 

## Start with transparency 

Prior to implementing Fraud Protection, make sure the privacy disclosures in your ecommerce experience describe how you use personal data, including how it is used to prevent and detect fraud. You can leverage the Fraud Protection documentation to meet your transparency needs. 

## Honor data subject requests

Fraud Protection provides tools to help you comply with data subject requests from your customers. These tools enable you to delete and export customer data from the service which has not been processed using deidentification techniques in the fraud network. Data processed in the fraud network cannot be accessed, exported, viewed, or deleted. 

For more information, see the following resources:
- [Data Subject Requests for the GDPR](https://docs.microsoft.com/microsoft-365/compliance/gdpr-data-subject-requests)
- [Safeguard individual privacy with the Microsoft Cloud](https://www.microsoft.com/trustcenter/privacy/gdpr/gdpr-overview)
- [Microsoft Dynamics 365 and GDPR](https://docs.microsoft.com/dynamics365/get-started/gdpr/index)
- [Microsoft Power BI GDPR white paper](https://powerbi.microsoft.com/blog/power-bi-gdpr-whitepaper-is-now-available/)

In the *Diagnose experience* for Fraud Protection, you can delete the offline data that you've uploaded into Fraud Protection. At the top of the page, select **Delete my data**.

In the *Evaluate* and *Protect experiences*, you can perform the following tasks for all entities that contain personal data:

- Identify entities that contain personal data.
- Delete entities.
- Export entities.

## Manage data subject requests

A data subject request (DSR) is a request asking for modification of personal data held by a third party. 

#### To manage DSR requests with Fraud Protection:

1. On the left navigation bar, select **Data engineering**, and then select **Subject requests**. 

    The **Search** tab provides the following selections to expedite your search:

    - User.Email
    - User.UserId
    - Purchase.PurchaseId
    - PaymentInstrument.PaymentInstrumentId

1. After you make your selection, if you require more specificity, you can use the search bar to enter keywords. 
1. From the search results, select either **Export user and associated data** or **Delete user and associated data**.
1. Select the **Requests** tab that identifies the following properties for your search:

    - Request ID
    - Request types (delete or export)
    - Subject ID
    - Statuses (pending or complete)
    - Exported data links.

