---
author: josaw1
description: This article provides information about security, compliance, and data subject requests.
ms.author: josaw
ms.date: 04/10/2024
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

Fraud Protection provides tools to help you comply with data subject requests from your customers. These tools enable you to delete and export Transactional Data from Assessments which haven't been processed using pseudonymization techniques in the Fraud Protection network. After Transactional Data is processed in the network, it can't be accessed, exported, viewed, or deleted. Transactional Data is defined as all the data from the request and response payload, plus any attributes and enrichments that are attached to a transaction. Fraud Protection may still retain aggregated data calculated with a contribution from the transaction.    

> [!NOTE]
> The **User ID** field in the API payload for Delete or Export calls is mandatory for Fraud Protection to successfully process the corresponding data subject requests (DSRs). The User ID should be identical to the one that was provided for the Account creation, Account login, or Purchase API call for the same Data Subject. If a User ID isn't provided, or a different User ID is provided from the one that was provided before, it will be extremely difficult for Fraud Protection to identify the transaction and DSRs will be difficult to process without significant efforts of investment.

For more information, see the following resources:
- [Dynamics 365 Fraud Protection API](https://go.microsoft.com/fwlink/?linkid=2084942).
- [Data Subject Requests](/microsoft-365/compliance/gdpr-data-subject-requests)
- [Safeguard individual privacy with the Microsoft Cloud](https://www.microsoft.com/trustcenter/privacy/gdpr/gdpr-overview)

On the **Subject Requests** page, you can perform the following tasks for all transactions:

-	Identify transactions that contain personal data
-	Delete transactions
-	Export transactions

## Manage data subject requests

A data subject request (DSR) is a request asking for modification of personal data held by a third party. 

### Manage DSR requests with Fraud Protection:

1. On the left navigation bar, select **Settings**, and then select **Subject requests**. 

   You can make requests for each assessment. For a request, select the assessment, the Data subject ID, and the value for the Data subject ID.

    - For Account Creation, Account Login, and Purchase Protection, the Data subject ID is user.userId.
    - For more information on the data subject IDs for assessments created using the [Assessment wizard](assessment-create-new.md#assessment-wizard-overview), see [Data subject IDs](assessment-create-new.md#data-subject-ids).
   
1. Select the type of request you would like to make (export or delete), and then review and confirm.

   The **Requests** table identifies the following properties for your requests. The log will retain exported data links and information for 28 days.

    - Request ID
    - Requestor
    - Timestamp
    - Request types (delete or export)
    - Statuses (pending or complete)
    - Exported data links

### Data subject request API

Fraud Protection allows you to programmatically honor data subject requests using our API. Below is the schema for our GDPR APIs.

GDPR API payload. The GDPR API is used for [Account protection](ap-overview.md) and [Purchase protection](purchase-protection.md).

| Attribute                   | Type     | Description | Required? |
|-----------------------------|----------|-------------|---------|
| SubjectID                   | string   | Takes the form of "**User**:userId", where userId is an attribute of the User object. | Yes |

Subject Request API payload. The subject request API is used for [Assessments](assessment-create-new.md#assessment-wizard-overview).

| Attribute                   | Type     | Description | Required? |
|-----------------------------|----------|-------------|-----------|
| AssessmentName              | string   | The name of the assessment. | Yes |
| PropertyName                | string   | The name of the property that's the data subject ID. For example **user.id**,. | Yes |
| PropertyValue               | string   | The value of the property that's the data subject ID you're making the request on. For example, **user123**. | Yes |

For further documentation about this and other Fraud Protection APIs, see [Dynamics 365 Fraud Protection API](https://go.microsoft.com/fwlink/?linkid=2084942).

### Data subject request for reports
Data modifications through data subject requests affect the aggregation numbers of the reports. Fraud Protection recalculates reports to reflect new status updates (for example, chargeback rates in purchase protection). However, it keeps only snapshots of aggregated data outside that moving time window. The aggregated snapshot no longer contains transaction-level details or personally identifiable information. Therefore, the aggregated snapshot can't reflect the impact of GDPR deletion. For example, a customer might request to delete all transactions on the account, including two transactions from the last month and one transaction from five months ago. When this GDPR deletion request is processed in Fraud Protection, an updated report that's configured to reflect the last four months of data might show no transactions in the previous month. Reports that are older than the previously stated time window of four months won't be updated. However, these reports don't affect any delete action in the underlying data.

## Fair Credit Reporting Act

The Fair Credit Reporting Act (FCRA) is a federal privacy law that regulates the disclosure and use of consumer personal information to determine a consumer's eligibility to obtain a product or service or otherwise engage in a transaction. FCRA also applies to the use of consumer personal information for non-credit-related transactions, such as insurance, employment, or even retail purchases, where the consumer's reputation or personal characteristics are relevant to eligibility. 

Why does FCRA matter to users of Fraud Protection? Fraud Protection wasn't designed to analyze the characteristics or behavior of credit card users, which is primarily an area that FCRA protects for consumers. Fraud Protection only informs you about the risk that the transaction might have been initiated by a fraudster, not whether the specific purchaser has a history of committing fraud. If Fraud Protection is ever abused to assess the personal characteristics of a given purchaser for purposes that are restricted by FCRA, this abuse could bring serious legal consequences for both users and Microsoft. For this reason, we take special care to educate our customers about the usage limitations of Fraud Protection.

Therefore, during the first-run experience in Fraud Protection, usage consent forms are provided to tenant administrators, but only when they access the application for the first time. Product Admin, Global Admin, PSP Admin, and All Areas Admin are presented with this user experience. 

[!INCLUDE[footer-include](includes/footer-banner.md)]
