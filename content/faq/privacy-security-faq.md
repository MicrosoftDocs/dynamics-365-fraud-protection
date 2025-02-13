---
author: josaw1
description: This article provides answers to frequently asked questions (FAQ) about privacy and security in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 12/09/2022
ms.topic: faq
search.audienceType:
  - admin
title: Privacy and security FAQ
---

# Privacy and security FAQ

[!include[deprecation](../includes/deprecation.md)]

This article provides answers to frequently asked questions (FAQ) about privacy and security in Microsoft Dynamics 365 Fraud Protection.

#### Has Fraud Protection experienced a security breach in the last 12 months? What are the breach notification process and timelines? 

Fraud Protection follows Microsoft's standard data breach notification process subject to General Data Protection Regulation (GDPR) requirements, regardless of whether a customer's data is subject to GDPR. For more information, including a description of the process and links to learn more, see [Microsoft Trust Center](https://www.microsoft.com/trust-center/privacy/gdpr-data-breach). While you're there, you can also set up your organization's privacy contact for notifications.

You can also find more information in [Azure, Dynamics 365, and Windows breach notification under the GDPR](/compliance/regulatory/gdpr-breach-azure-dynamics-windows).

#### Does Fraud Protection support encryption of data at rest? How is the encryption deployed? Is any data encrypted in transit? What are the protocols? 

The Fraud Protection service encrypts all customer data, both at rest and in transit, by using the latest capabilities of Azure. These capabilities are regularly reviewed by Microsoft security teams.

For data in transit, Fraud Protection uses encryption that is based on Transport Layer Security (TLS).

Microsoft technologies such as Azure Cosmos DB, Azure Blob Storage, and Azure Data Lake are used to store data at rest. Fraud Protection implements strict trust boundaries to ensure that there is no unauthorized access to a merchant's data in its environment.

For more information about Microsoft's approach to data encryption at rest and in transit, see [Azure encryption overview](/azure/security/fundamentals/encryption-overview) and [Azure Data Encryption-at-Rest](/azure/security/fundamentals/encryption-atrest).

> [!NOTE]
> Please note that Dynamics 365 Fraud Protection does not support Customer Managed Keys (CMK) or Lockbox capabilities. 

#### Does Fraud Protection process, access, transmit, or store its merchant's non-public personal data?  

Fraud Protection works with the data that its merchants provide via APIs, file upload, or other documented mechanisms. The data that merchants provide might contain non-public personal data that Fraud Protection processes, transmits, and stores inside its compliance boundary to provide the service. Merchants might use Fraud Protection to transmit the data to a different system or create additional copies to meet their business needs.

#### Who has access to merchant data and reports in the Fraud Protection system? How does Fraud Protection limit the number of people who have access?

The merchant and the Microsoft employees who are assigned to Fraud Protection have access to the merchant's data. For in-product reports, only merchants have access to merchant data. For out-of-product reports, Fraud Protection's data science team gives the merchants access to view the reports. Not all Microsoft employees will have access to the merchant's reports.

Fraud Protection implements network and role-based access controls to limit and manage external access to the data inside Fraud Protection. Tenants are provided with functionality for managing external access to their data.

Fraud Protection follows Microsoft internal policies and guidelines to manage internal access to production services and customer data. By default, access to merchant data and reports is denied to Microsoft personnel, according to the principle of least privilege. It's granted only to members of the appropriate security groups. Security group membership is granted at the user account level, and each user account is unique and identified with a specific Microsoft employee.

Microsoft internal policy allows Microsoft employees who have the appropriate security group membership to request temporary ("just-in-time") elevated access so that they can perform servicing and support activities on production systems. Every just-in-time access request is tracked and reviewed by the internal ticketing system.

#### Does Fraud Protection provide a published procedure for exiting the service arrangement, including an assurance that all computing resources will be sanitized of tenant data after a customer has exited the environment or vacated a resource?   

Yes. Microsoft [Commercial Licensing Terms](https://www.microsoft.com/licensing/terms/welcome/welcomepage) apply to Fraud Protection and define the procedures for canceling a service. The [data protection addendum](https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA) describes the details about how data is retained and deleted. The pseudonymized data that a merchant has already provided to the Fraud Protection Network will continue to be processed inside the Fraud Protection Network until the end of its sliding retention window. It will then be deleted.

#### Does Fraud Protection collaborate with any professional security services organization within Microsoft for security and technology support (for example, deployment, incident response, and reporting)? 

Yes. Fraud Protection is part of the Dynamics 365 family of products, and follows policies and guidelines that are defined for the Dynamics 365 and Cloud & AI organization. Fraud Protection collaborates with Azure Security, Microsoft Threat Intelligence Center, Azure Incident Response Team, Microsoft Global Security, and other internal security and compliance teams.

For more information about security for Fraud Protection, see [Security overview for Dynamics 365 Fraud Protection](../security.md).

#### How does Fraud Protection ensure that data quality errors and risks that are inherited from partners in the cloud supply chain are inspected, accounted for, and corrected? 

Fraud Protection has a dedicated data science team. It also has a monitoring and alerting system that is designed to detect and respond to data quality errors, and to maintain the quality of machine learning (ML) models. Data quality issues are treated as production incidents and are reviewed through the same process that is used for maintaining service reliability.

#### Does Fraud Protection regularly conduct network penetration tests of the cloud service infrastructure, as prescribed by industry best practices and guidance? Are the results of the network penetration tests available to tenants at their request?  

Fraud Protection uses industry-standard tools to scan the code, and the bug detection and severity are based on NIST 800-30 standards.

An independent third party does a penetration test (pen test) on the Azure environment at least annually. The scope of the pen test is determined by Azure's areas of risk and compliance requirements. The findings of the pen test are remediated based on criticality. For more information, see the [Service Trust Portal](https://servicetrust.microsoft.com).

#### Does Fraud Protection regularly conduct network-layer vulnerability scans, as prescribed by industry best practices? 

Yes, Fraud Protection follows industry standard best practices. As is outlined in the Azure-Dynamics SOC2 [audit reports](https://servicetrust.microsoft.com/ViewPage/MSComplianceGuideV3?command=Download&downloadType=Document&downloadId=34772c1f-ea02-4ba6-b4a7-20aeb5241243&tab=7027ead0-3d6b-11e9-b9e1-290b1eb4cdeb&docTab=7027ead0-3d6b-11e9-b9e1-290b1eb4cdeb_SOC_%2F_SSAE_16_Reports), the Cloud + AI Security team performs frequent internal and external scans to identify vulnerabilities and assess the effectiveness of the patch management process. Services are scanned for known vulnerabilities. New services are added to the next timed quarterly scan, based on their date of inclusion. They then follow at least a quarterly scanning schedule. These scans are used to ensure compliance with baseline configuration templates, validate that relevant patches are installed, and identify vulnerabilities. The scanning reports are reviewed by appropriate personnel, and remediation efforts are conducted in a timely manner.

## Additional resources

[Service FAQ](service-faq.md)

[Legal considerations FAQ](legal-faq.md)

[Data residency and GDPR FAQ](data-residency-faq.md)

[Compliance FAQ](compliance-faq.md)

[EU Data Boundary exceptions for Fraud Protection](../edbd.md)
