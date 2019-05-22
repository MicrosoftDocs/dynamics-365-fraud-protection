---
author: jackwi111
description: This topic provides frequently asked questions about Microsoft Dynamics 365 Fraud Protection.
ms.author: v-jowigh
ms.service: crm-online
ms.date: 05/21/2019

ms.topic: conceptual
title: FAQ
---

# FAQ

## General product FAQ

**Can we upload historical data to compare our results with what Dynamics 365 Fraud Protection thinks about the data before we go through the full integration process?**

Yes. We have a Diagnosis experience that is designed exactly for this purpose. You upload historical data (which stays in your own merchant Azure tenant as we don’t have access to this data), and Dynamics 365 Fraud Protection will run that data through our ML and produce both a data diagnosis report and a risk diagnosis report. The data diagnosis report is designed to help you identify potential gaps or additional signals that would improve the risk score. The risk diagnosis report is designed to help you see how our ML would have performed, and to allow you to play with the risk score thresholds to understand the potential impact to your business in terms of both fraud prevention and overall profit. 

**Can we pick and choose which orders are subject to a fraud check?**

The quality of a Dynamics 365 Fraud Protection risk assessment improves with every transaction that is sent. While the decision to accept or reject a transaction is entirely up to you, we recommend that you assess all transactions to maximize the quality of the scores. 

**How does your network size compare to that of payment processors like Chase, Worldpay, and Adyen?**

While we cannot disclose the names of other customers operating within our fraud proteciton network, we have seeded it with Microsoft worldwide merchant data which covers billions of transactions with a wide variety of physical and digital goods in all major markets. 

**What is the role of manual review in this solution?**

TBD

**What role would a customer's purchase history play in the fraud models? Is the fraud engine stricter with new customers than it is with customers who have significant purchase history with our business? Would the fraud engine be more trusting of customers whose purchase behavior matches past behavior (same device, device location, IP, shipping address, etc.) and less trusting of customers whose behavior is irregular? **

TBD

**How does your device fingerprinting solution work? Is it a script I link to? Can I self-host it?**

TBD

**What type of latency guarantees do you offer?**

TBD

**What payment types do you support?**

TBD

**Does Dynamics 365 Fraud Protection provide a liability shift? **

TBD

**How does this work with PSD2?**

A: TBD

**Do you provide reason codes or an explanation for a given risk assessment score?**

TBD

**How do you obtain quality fraud labels for model training?**

TBD

**Do I need to upload chargeback data to you? How do I do that?**

TBD

**I’m an existing Dynamics 365 customer. What type of integration is available to me out of the box?**

TBD

## Privacy, security, and compliance FAQ

**Does Microsoft have access to my customer data?**

TBD

**What is your GDPR compliance story? Does this solution work in the EU?**

TBD

**How do you protect our data when we upload it? Do we need to hash everything before we upload it to you?**

Whenever you upload data (manually or via API calls), it lands in your own merchant space within your Azure tenant. This data is encrypted at rest, but can still be accessed by your risk support teams or other approved tenant users. Some of the data is then de-identified before crossing the trust boundary into our fraud protection network. This is where we compile data from across our merchant ecosystem and train some of the models. Whenever you call the transaction API for a risk assessment, the resulting score is based on a combination of context from within your merchant space, as well as context from the fraud protection network. 

**Do you collect, use, or disclose “sensitive personal data" (for example, race, ethnicity, political opinions, religious or other beliefs, etc.)?**

TBD

**I am an EU-based merchant. Will my customer’s data be shared outside of the EU? Where is this data hosted?**

TBD

**Will you directly seek consent from individuals to use their data in the context of fraud protection?**

TBD

**Why do you need to collect personal data?**

Personal data collected and shared with the vendor in the context of processing a transaction is necessary to safeguard the integrity of the transaction prior to transmission to payment gateways, issuing banks, or credit card networks, for banking processing purposes. By the same token, and as processing occurs at the corresponding financial services institution, fraud protection processing improves the efficiency of the assessments conducted by merchants on a transactional level, helping alleviate processing time for legitimate transactions.    

**Do you use tracking mechanisms (for example, cookies, pixels, etc.) to collect personal data?**

Dynamics 365 Fraud Protection uses device-specific context technology that assists customers in collecting personal data from end users of the booking.com services at a transactional level. This enables customers to protect their financial transactions during the e-commerce flow and to identify potential transactions that could be fraudulent. 

**How long do you retain collected personal data?**

The merchant retains ultimate control over the data pursuant to the licensing terms provided by the vendor. While offering Dynamics 365 Fraud Protection, Microsoft does not have standing access to tenant’s customer data. Control and management of the customer data, including personal data provided to process the services enabled by Dynamics 365 Fraud Protection, is exercised by the customer. Customers may delete data whenever they deem it necessary. 

Fractions of transactional data could be retained by Dynamics 365 Fraud Protection in a second-level repository of aggregated data to enrich (increase accuracy) processing at a transactional level. All data so retained is de-identified using robust hashing techniques which are further salted to prevent any possibility of re-identification after the customer has left the online service due to expiration or termination. 

**Can I delete personal data at any time while using Dynamics 365 Fraud Protection?**

Fractions of transactional data could be retained by Dynamics 365 Fraud Protection in a second-level repository of aggregated data to enrich (increase accuracy) processing at a transactional level (continued calibration of the machine learning model across all tenants). All data so retained are de-identified using robust hashing techniques which are further salted to prevent any possibility of re-identification after the customer has left the online service due to expiration or termination. 

**Do you provide independent periodic assurance reporting on the hosted environment, such as SOC 1/2 (AICPA), ISO 27001, Third-Party Trust, or other?** 

All underlying systems used by Dynamics 365 Fraud Protection comply with the list of certifications (including ISO 27001/27018, SSEA18 SOC 1 and 2) offered by Dynamics 365 Core Services. Certification of the corresponding application layers (for example, SaaS) is expected soon after the service is made generally available and Dynamics 365 Fraud Protection is added to the list of Dynamics 365 Core Services. During public preview, Dynamics 365 Fraud Protection is operated pursuant to security controls prescribed by ISO 27001/27018 standards.  

For more information, see [Microsoft Dynamics 365 Trust Center](https://www.microsoft.com/en-us/trustcenter/cloudservices/dynamics365).

**Do you do frequently do vulnerability scans or penetration testing on the hosted environment? Is this report available periodically?** 

Microsoft performs frequent penetration testing and constant monitoring for vulnerabilities. Dynamics 365 Core Services are subject to annual penetration tests as described in the report posted to the [Microsoft Service Trust Portal](https://servicetrust.microsoft.com/ViewPage/TrustDocumentsV3?command=Download&downloadType=Document&downloadId=25aa47b1-c510-43f2-84de-6b78ed3b1258&tab=7f51cb60-3d6c-11e9-b2af-7bb9f5d2d913&docTab=7f51cb60-3d6c-11e9-b2af-7bb9f5d2d913_Pen_Test_and_Security_Assessments).

Dynamics 365 Fraud Protection is not covered under the scope of the current penetration test but it is expected to be covered soon after the application is made generally available.

**Do you have a vulnerability disclosure policy?**

Microsoft performs and discloses frequent security assessments in combination with its penetration testing reports. Dynamics 365 Core Services are subject to annual penetration tests and security assessment as described in the report posted to the [Microsoft Service Trust Portal](https://servicetrust.microsoft.com/ViewPage/TrustDocumentsV3?command=Download&downloadType=Document&downloadId=25aa47b1-c510-43f2-84de-6b78ed3b1258&tab=7f51cb60-3d6c-11e9-b2af-7bb9f5d2d913&docTab=7f51cb60-3d6c-11e9-b2af-7bb9f5d2d913_Pen_Test_and_Security_Assessments).

Dynamics 365 Fraud Protection is not covered under the scope of the current security assessment but it is expected to be covered soon after the application is made generally available.

**What are your business continuity or disaster recovery practices?**

See [Dynamics 365 Business Recovery and Continuity Plan, and Security Incident Management policies](https://servicetrust.microsoft.com/ViewPage/TrustDocumentsV3?docTab=7f51cb60-3d6c-11e9-b2af-7bb9f5d2d913_FAQ_and_White_Papers).

**Do you have monitoring, audit logging controls, or other facilities on user access?**

Dynamics 365 Fraud Protection has active monitoring and audit logging on user access of all components. See [Dynamics 365 Security Incident Management policies](https://servicetrust.microsoft.com/ViewPage/TrustDocumentsV3?docTab=7f51cb60-3d6c-11e9-b2af-7bb9f5d2d913_FAQ_and_White_Papers).

**Where can I find your terms and conditions or privacy statement?**

See [Microsoft Licensing Terms](https://www.microsoft.com/en-us/licensing/product-licensing/products).

**Where can I find your privacy statement?**

See [Microsoft Privacy Statement](www.microsoft.com/privacy).
