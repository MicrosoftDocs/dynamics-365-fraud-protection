---
author: josaw1
description: This article provides information about security, compliance, and data subject requests.
ms.author: josaw
ms.date: 10/19/2022
ms.topic: overview
search.audienceType:
  - admin
title: Compliance overview

---

# Compliance overview

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
- [Data Subject Requests for the GDPR](/microsoft-365/compliance/gdpr-data-subject-requests)
- [Safeguard individual privacy with the Microsoft Cloud](https://www.microsoft.com/trustcenter/privacy/gdpr/gdpr-overview)
- [Microsoft Dynamics 365 and GDPR](/dynamics365/get-started/gdpr/index)
- [Microsoft Power BI GDPR white paper](https://powerbi.microsoft.com/blog/power-bi-gdpr-whitepaper-is-now-available/)

In the evaluate and protect experiences, you can perform the following tasks for all entities that contain personal data:

- Identify entities that contain personal data.
- Delete entities.
- Export entities.

## Manage data subject requests

A data subject request (DSR) is a request asking for modification of personal data held by a third party. 

### To manage DSR requests with Fraud Protection:

1. On the left navigation bar, select **Settings**, and then select **Subject requests**. 

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

### Data subject request API

Fraud Protection allows you to programmatically honor data subject requests using our API. Below is the schema for our GDPR APIs.


| Attribute                   | Type     | Description | Required? |
|-----------------------------|----------|-------------|---------|
| SubjectID                   | string   | Takes the form of "**User**:userId", where userId is an attribute of the User object. | Yes |



For further documentation about this and other Fraud Protection APIs, see [Dynamics 365 Fraud Protection API](https://go.microsoft.com/fwlink/?linkid=2084942).

### Data subject request for reports
Data modifications through data subject requests affect the aggregation numbers of the reports. Fraud Protection recalculates reports to reflect new status updates (for example, chargeback rates in purchase protection). However, it keeps only snapshots of aggregated data outside that moving time window. The aggregated snapshot no longer contains transaction-level details or personally identifiable information. Therefore, the aggregated snapshot can't reflect the impact of GDPR deletion. For example, a customer might request to delete all transactions on the account, including two transactions from the last month and one transaction from five months ago. When this GDPR deletion request is processed in Fraud Protection, an updated report that's configured to reflect the last four months of data might show no transactions in the previous month. Reports that are older than the previously stated time window of four months won't be updated. However, these reports don't affect any delete action in the underlying data.

## Fair Credit Reporting Act

The Fair Credit Reporting Act (FCRA) is a federal privacy law that regulates the disclosure and use of consumer personal information to determine a consumer's eligibility to obtain a product or service or otherwise engage in a transaction. FCRA also applies to the use of consumer personal information for non-credit-related transactions, such as insurance, employment, or even retail purchases, where the consumer's reputation or personal characteristics are relevant to eligibility. 

Why does FCRA matter to users of Fraud Protection? Fraud Protection wasn't designed to analyze the characteristics or behavior of credit card users, which is primarily an area that FCRA protects for consumers. Fraud Protection only informs you about the risk that the transaction might have been initiated by a fraudster, not whether the specific purchaser has a history of committing fraud. If Fraud Protection is ever abused to assess the personal characteristics of a given purchaser for purposes that are restricted by FCRA, this abuse could bring serious legal consequences for both users and Microsoft. For this reason, we take special care to educate our customers about the usage limitations of Fraud Protection.

Therefore, during the first-run experience in Fraud Protection, usage consent forms are provided to tenant administrators, but only when they access the application for the first time. Product Admin, Global Admin, PSP Admin, and All Areas Admin are presented with this user experience. 

[!INCLUDE[footer-include](includes/footer-banner.md)]
