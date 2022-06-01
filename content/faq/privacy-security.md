---
author: josaw1
description: This topic provides frequently asked questions and answers about privacy and security in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 06/01/2022
ms.topic: faq
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Privacy and security FAQ
---

# Privacy and security FAQ

## Has Dynamics 365 Fraud Protection experienced a security breach in the last 12 months? What are the breach notification process and timelines? 

DFP follows Microsoft's standard data breach notification process subject to GDPR requirements regardless of whether a Customer's data is subject to GDPR. More information can be located at Microsoft's Trust Center (<https://www.microsoft.com/en-ww/trust-center/privacy/gdpr-data-breach> ) which contains a description of the process, links to learn more and to set up your organization's privacy contact for notifications.

More information can also be found at: [Azure, Dynamics 365, and Windows breach notification under the GDPR - Microsoft GDPR \| Microsoft Docs](https://docs.microsoft.com/en-us/compliance/regulatory/gdpr-breach-azure-dynamics-windows)

## Does DFP support encryption of data at rest?  Please describe how the encryption is deployed (disk, table?) Is any data encrypted in transit? Please specify protocols used. 

Dynamics 365 Fraud Protection service encrypts all customer data both at rest and in transit, utilizing the latest capabilities of Microsoft Azure, which are reviewed regularly by Microsoft security teams.



DFP uses TLS based encryption for data in transit.

Microsoft technologies like Cosmos DB, Azure Blob storage, and Azure Data Lake are used to store data at rest and their encryption strategies are detailed through Microsoft.com documentation. DFP implements strict trust boundaries to ensure there is no unauthorized access to a merchant's data in its environment.

more information about Microsoft's approach to data encryption at rest and in transit (which DFP follows) can be found at:

[Azure encryption overview \| Microsoft Docs](https://docs.microsoft.com/en-us/azure/security/fundamentals/encryption-overview)

[Azure Data Encryption-at-Rest - Azure Security \| Microsoft Docs](https://docs.microsoft.com/en-us/azure/security/fundamentals/encryption-atrest)



## Will DFP process, access, transmit or store its merchant's non-public personal data?  

DFP works with the data, which is provided by its merchants via APIs, file upload, or other

documented mechanisms. The data which merchants provide may contain non-public personal data which DFP will process, transmit and store within its compliance boundary to provide the service. A merchant may leverage DFP to transmit the data to a different system or create additional copies to meet the merchant's business needs.



## Who will have access to merchant's data and reports in the DFP system? Describe how DFP will limit the number of people who will have access. 



The merchant and the Microsoft employees assigned to DFP will have access to the merchant's data. For in-product reports, only merchants will have access to merchant data. For out of product reports, DFP's data science team gives access to the merchants to view the reports. Not all Microsoft employees will have access to the merchant's reports.

DFP implements network ACL and RBAC controls to limit and manage external access to the data inside DFP. Tenants are provided functionality to manage external access to their data.

DFP follows Microsoft internal policies and guidelines to manage internal access to production services and customer data. The policy requires the access for Microsoft personnel to be denied by default following the principle of least privilege and be granted only to members of appropriate security groups. The security group membership is granted at user account level, with each user account being unique and identified to a specific Microsoft employee.

Microsoft internal policy permits temporary (just in time) elevated access can be requested by Microsoft employees with appropriate security group membership to perform servicing and support activities on production systems. Each just-in-time access request is tracked and reviewed by the internal ticketing system.



## Will DFP provide a published procedure for exiting the service arrangement, including assurance to sanitize all computing resources of tenant data once a customer has exited the environment or has vacated a resource?   



Yes. Microsoft [Commercial Licensing Terms (microsoft.com)](https://www.microsoft.com/licensing/terms/welcome/welcomepage) apply to DFP and define the procedures for how to cancel a service, and the data protection addendum (link [Licensing Documents (microsoft.com)](https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA)) describes the details of how the data is retained and deleted. The pseudonymized data already provided by a merchant to Fraud Protection Network will continue being processed inside FPN until the end of its sliding retention window and is deleted after.



## Is DFP collaborating with any professional security services organization within Microsoft for security and technology support (e.g., deployment, incident response and reporting, etc.)? 



Yes. DFP is a part of Dynamics 365 family of products, it follows policies and guidelines defined for Dynamics 365 and Cloud & AI organizations and collaborate with Azure Security, Microsoft Threat Intelligence Center, Azure Incident Response Team, Microsoft Global Security, and other internal security and compliance teams.

To learn more about security for DFP, please visit: [Security overview for Dynamics 365 Fraud Protection - Dynamics 365 Fraud Protection \| Microsoft Docs](https://docs.microsoft.com/en-us/dynamics365/fraud-protection/security).



## Does DFP support tenant generated encryption keys or permit tenants to encrypt data to an identity without access to a public key certificate? (e.g., Identity based encryption)? 



Yes, please refer to this document for understanding Azure Data Encryption at Rest

[Azure Data Encryption-at-Rest - Azure Security \| Microsoft Docs](https://docs.microsoft.com/en-us/azure/security/fundamentals/encryption-atrest)

## How does DFP ensure data quality errors and risks inherited from partners within the cloud supply-chain are inspected, accounted for, and corrected? 

DFP has a dedicated data science team and a dedicated monitoring and alerting system designed to detect and respond to data quality errors and maintain the quality of machine learning models doesn't degrade. Data quality problems are treated as production incidents and are reviewed following the same process for maintaining service reliability.



## Does DFP conduct network penetration tests of the cloud service infrastructure regularly as prescribed by industry best practices and guidance?  Are the results of the network penetration tests available to tenants at their request?  



DFP uses industry standard tools to scan the code and the bug detection and severity is based on NIST 800-30 standards.

Penetration Testing (PEN Test) is performed at least annually on the Azure environment by an independent third party. The PEN Test scope is determined based on Azure's areas of risk and compliance requirements. PEN Test findings are remediated based on criticality
Please visit [<u>https://servicetrust.microsoft.com</u>](https://servicetrust.microsoft.com) for more details.





## Does DFP conduct network-layer vulnerability scans regularly as prescribed by industry best practices? 



Yes, DFP follows industry standard best practices. As outlined in the Azure-Dynamics SOC2 audit report ([Audit Reports (microsoft.com)](https://servicetrust.microsoft.com/ViewPage/MSComplianceGuideV3?command=Download&downloadType=Document&downloadId=34772c1f-ea02-4ba6-b4a7-20aeb5241243&tab=7027ead0-3d6b-11e9-b9e1-290b1eb4cdeb&docTab=7027ead0-3d6b-11e9-b9e1-290b1eb4cdeb_SOC_%2F_SSAE_16_Reports) ), Cloud + AI Security team carries out frequent internal and external scans to identify vulnerabilities and assess the effectiveness of the patch management process. Services are scanned for known vulnerabilities; new services are added to the next timed quarterly scan, based on their date of inclusion, and follow at least a quarterly scanning schedule thereafter. These scans are used to ensure compliance with baseline configuration templates, validate that relevant patches are installed, and identify vulnerabilities. The scanning reports are reviewed by appropriate personnel and remediation efforts are conducted in a timely manner.
