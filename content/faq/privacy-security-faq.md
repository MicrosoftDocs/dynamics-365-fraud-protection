---
author: josaw1
description: This article provides answers to frequently asked questions (FAQ) about privacy and security in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 06/02/2022
ms.topic: faq
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Privacy and security FAQ
---

# Privacy and security FAQ

This article provides answers to frequently asked questions (FAQ) about privacy and security in Microsoft Dynamics 365 Fraud Protection.

### Has Dynamics 365 Fraud Protection experienced a security breach in the last 12 months? What are the breach notification process and timelines? 

Fraud Protection follows Microsoft's standard data breach notification process subject to General Data Protection Regulation (GDPR) requirements regardless of whether a customer's data is subject to GDPR. For more information, including a description of the process and links to learn more, see [Microsoft Trust Center](https://www.microsoft.com/trust-center/privacy/gdpr-data-breach). While there you can also set up your organization's privacy contact for notifications.

More information can also be found in [Azure, Dynamics 365, and Windows breach notification under the GDPR](/compliance/regulatory/gdpr-breach-azure-dynamics-windows.md).

### Does Fraud Protection support encryption of data at rest? How is the encryption deployed? Is any data encrypted in transit? What are the protocols? 

The Fraud Protection service encrypts all customer data both at rest and in transit using the latest capabilities of Microsoft Azure, which are reviewed regularly by Microsoft security teams.

Fraud Protection uses transport layer security (TLS) based encryption for data in transit.

Microsoft technologies like Cosmos DB, Azure Blob storage, and Azure Data Lake are used to store data at rest. Fraud Protection implements strict trust boundaries to ensure that there is no unauthorized access to a merchant's data in its environment.

For more information about Microsoft's approach to data encryption at rest and in transit, see [Azure encryption overview](/azure/security/fundamentals/encryption-overview.md) and [Azure Data Encryption-at-Rest](/azure/security/fundamentals/encryption-atrest).

### Does Fraud Protection process, access, transmit, or store its merchant's non-public personal data?  

Fraud Protection works with the data, which is provided by its merchants via APIs, file upload, or other documented mechanisms. The data that merchants provide may contain non-public personal data that Fraud Protection processes, transmits, and stores within its compliance boundary to provide the service. A merchant may use Fraud Protection to transmit the data to a different system or create additional copies to meet the merchant's business needs.

### Who has access to merchant data and reports in the Fraud Protection system? How does Fraud Protection limit the number of people who have access?

The merchant and the Microsoft employees assigned to Fraud Protection have access to the merchant's data. For in-product reports, only merchants will have access to merchant data. For out-of-product reports, Fraud Protection's data science team gives access to the merchants to view the reports. Not all Microsoft employees will have access to the merchant's reports.

Fraud Protection implements network and role-based access controls to limit and manage external access to the data inside Fraud Protection. Tenants are provided functionality to manage external access to their data.

Fraud Protection follows Microsoft internal policies and guidelines to manage internal access to production services and customer data. Access to merchant data and reports by Microsoft personnel is denied by default following the principle of least privilege and is only granted to members of appropriate security groups. Security group membership is granted at the user account level, with each user account being unique and identified to a specific Microsoft employee.

Microsoft internal policy permits temporary ("just-in-time") elevated access that can be requested by Microsoft employees with appropriate security group membership to perform servicing and support activities on production systems. Each just-in-time access request is tracked and reviewed by the internal ticketing system.

### Does Fraud Protection provide a published procedure for exiting the service arrangement, including an assurance to sanitize all computing resources of tenant data once a customer has exited the environment or has vacated a resource?   

Yes. Microsoft [Commercial Licensing Terms](https://www.microsoft.com/licensing/terms/welcome/welcomepage) apply to Fraud Protection and define the procedures for how to cancel a service, and the [data protection addendum](https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA) describes the details of how data is retained and deleted. The pseudonymized data already provided by a merchant to the Fraud Protection Network will continue being processed inside the Fraud Protection Network until the end of its sliding retention window, and is deleted afterwards.

### Is Fraud Protection collaborating with any professional security services organization within Microsoft for security and technology support (for example deployment, incident response, and reporting)? 

Yes. Fraud Protection is a part of the Dynamics 365 family of products and it follows policies and guidelines defined for Dynamics 365 and Cloud & AI organization. Fraud Protection collaborates with Azure Security, Microsoft Threat Intelligence Center, Azure Incident Response Team, Microsoft Global Security, and other internal security and compliance teams.

To learn more about security for Fraud Protection, see [Security overview for Dynamics 365 Fraud Protection](../security.md).

### Does Fraud Protection support tenant-generated encryption keys or permit tenants to encrypt data to an identity without access to a public key certificate (for example, identity-based encryption)? 

Yes. For information on Azure Data Encryption at Rest, see [Azure Data Encryption at Rest](/azure/security/fundamentals/encryption-atrest.md).

### How does Fraud Protection ensure data quality errors and risks inherited from partners within the cloud supply-chain are inspected, accounted for, and corrected? 

Fraud Protection has a dedicated data science team and monitoring and alerting system designed to detect and respond to data quality errors and maintain the quality of machine learning models. Data quality problems are treated as production incidents and are reviewed following the same process for maintaining service reliability.

### Does Fraud Protection regularly conduct network penetration tests of the cloud service infrastructure as prescribed by industry best practices and guidance? Are the results of the network penetration tests available to tenants at their request?  

Fraud Protection uses industry standard tools to scan the code and the bug detection and severity is based on NIST 800-30 standards.

Penetration Testing (PEN Test) is performed at least annually on the Azure environment by an independent third party. The PEN Test scope is determined based on Azure's areas of risk and compliance requirements. PEN Test findings are remediated based on criticality. For more information, see the [Service Trust Portal](https://servicetrust.microsoft.com).

### Does Fraud Protection conduct network-layer vulnerability scans regularly as prescribed by industry best practices? 

Yes, Fraud Protection follows industry standard best practices. As outlined in the Azure-Dynamics SOC2 [audit reports](https://servicetrust.microsoft.com/ViewPage/MSComplianceGuideV3?command=Download&downloadType=Document&downloadId=34772c1f-ea02-4ba6-b4a7-20aeb5241243&tab=7027ead0-3d6b-11e9-b9e1-290b1eb4cdeb&docTab=7027ead0-3d6b-11e9-b9e1-290b1eb4cdeb_SOC_%2F_SSAE_16_Reports), the Cloud + AI Security team carries out frequent internal and external scans to identify vulnerabilities and assess the effectiveness of the patch management process. Services are scanned for known vulnerabilities. New services are added to the next timed quarterly scan based on their date of inclusion, and follow at least a quarterly scanning schedule thereafter. These scans are used to ensure compliance with baseline configuration templates, validate that relevant patches are installed, and identify vulnerabilities. The scanning reports are reviewed by appropriate personnel and remediation efforts are conducted in a timely manner.

## Additional resources

[Service FAQ](service-faq.md)

[Legal considerations FAQ](legal-faq.md)

[Data residency and GDPR FAQ](data-residency-gdpr-faq.md)

[Compliance FAQ](compliance-faq.md)
