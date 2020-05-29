---
author: yvonnedeq
description: This topic explains security in Dynamics 365 Fraud Protection.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 05/29/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Fraud Protection compliance and security
---


# Fraud Protection compliance and security 

Microsoft Dynamics 365 Fraud Protection has implemented and will continue to maintain appropriate technical and organizational measures to protect customer data and personal data. These measures are set forth in  Microsoft Security Policy. This policy is available to customers, as well as descriptions of the security controls in place for Fraud Protection and other information reasonably requested by the customer regarding Microsoft security practices and policies. 

For more information about Microsoft's security practice, please visit the [Microsoft Trust Center]https://www.microsoft.com/trust-center).

## Compliance certificate URLs

Here is a list of compliance certificate URLs for Fraud Protection.
 
-	[ISO 27001](https://servicetrust.microsoft.com/ViewPage/MSComplianceGuideV3?command=Download&downloadType=Document&downloadId=1db75ce8-45d3-41fb-a705-2bd2163c72eb&tab=7027ead0-3d6b-11e9-b9e1-290b1eb4cdeb&docTab=7027ead0-3d6b-11e9-b9e1-290b1eb4cdeb_ISO_Reports): https://servicetrust.microsoft.com/ViewPage/MSComplianceGuideV3?command=Download&downloadType=Document&downloadId=1db75ce8-45d3-41fb-a705-2bd2163c72eb&tab=7027ead0-3d6b-11e9-b9e1-290b1eb4cdeb&docTab=7027ead0-3d6b-11e9-b9e1-290b1eb4cdeb_ISO_Reports

-	[ISO 27018](https://servicetrust.microsoft.com/ViewPage/MSComplianceGuideV3?command=Download&downloadType=Document&downloadId=20a52f85-7901-4e96-88d1-7c83eacc44e1&tab=7027ead0-3d6b-11e9-b9e1-290b1eb4cdeb&docTab=7027ead0-3d6b-11e9-b9e1-290b1eb4cdeb_ISO_Reports): https://servicetrust.microsoft.com/ViewPage/MSComplianceGuideV3?command=Download&downloadType=Document&downloadId=20a52f85-7901-4e96-88d1-7c83eacc44e1&tab=7027ead0-3d6b-11e9-b9e1-290b1eb4cdeb&docTab=7027ead0-3d6b-11e9-b9e1-290b1eb4cdeb_ISO_Reports 

-	[ISO 27701](https://servicetrust.microsoft.com/Documents/ComplianceReports?command=Download&downloadType=Document&downloadId=c0431b3f-7716-4332-9c26-44b58174bdaf&docTab=4ce99610-c9c0-11e7-8c2c-f908a777fa4d_ISO_Reports): https://servicetrust.microsoft.com/Documents/ComplianceReports?command=Download&downloadType=Document&downloadId=c0431b3f-7716-4332-9c26-44b58174bdaf&docTab=4ce99610-c9c0-11e7-8c2c-f908a777fa4d_ISO_Reports 

-	[SOC 2](https://servicetrust.microsoft.com/ViewPage/MSComplianceGuide?command=Download&downloadType=Document&downloadId=22d75122-9d83-4b44-8e25-c273dcbafdc3&docTab=4ce99610-c9c0-11e7-8c2c-f908a777fa4d_SOC_%2F_SSAE_16_Reports): https://servicetrust.microsoft.com/ViewPage/MSComplianceGuide?command=Download&downloadType=Document&downloadId=22d75122-9d83-4b44-8e25-c273dcbafdc3&docTab=4ce99610-c9c0-11e7-8c2c-f908a777fa4d_SOC_%2F_SSAE_16_Reports 

-	[SOC 3](https://servicetrust.microsoft.com/ViewPage/MSComplianceGuide?command=Download&downloadType=Document&downloadId=ab827a49-6503-48ea-aa7d-e178efbb9eb1&docTab=4ce99610-c9c0-11e7-8c2c-f908a777fa4d_SOC_%2F_SSAE_16_Reports): https://servicetrust.microsoft.com/ViewPage/MSComplianceGuide?command=Download&downloadType=Document&downloadId=ab827a49-6503-48ea-aa7d-e178efbb9eb1&docTab=4ce99610-c9c0-11e7-8c2c-f908a777fa4d_SOC_%2F_SSAE_16_Reports 

-	[HITRUST](https://servicetrust.microsoft.com/ViewPage/MSComplianceGuideV3?command=Download&downloadType=Document&downloadId=02eaae7a-9d65-42e6-aec8-a8e22de1a494&tab=7027ead0-3d6b-11e9-b9e1-290b1eb4cdeb&docTab=7027ead0-3d6b-11e9-b9e1-290b1eb4cdeb_GRC_Assessment_Reports ): https://servicetrust.microsoft.com/ViewPage/MSComplianceGuideV3?command=Download&downloadType=Document&downloadId=02eaae7a-9d65-42e6-aec8-a8e22de1a494&tab=7027ead0-3d6b-11e9-b9e1-290b1eb4cdeb&docTab=7027ead0-3d6b-11e9-b9e1-290b1eb4cdeb_GRC_Assessment_Reports 

## Security documentation and SOP FAQs



## Security assessment FAQs

### Authentication and administration



### Auditing

| Question| Response    |
|---------|-------------|
|Does the application / service log information in an industry standard event format type, such as CSV, CEF, or Syslog?         |Log data is not shared by the product.  Service metrics and KPI's are surfaced via PowerBI views.             |
|Does the application / service collect or provide the following data:         |--             |
|User Login / Logoff / Password Change / Failed Login Attempts         |Yes.  See: Azure AD feature in merchant tenant https://docs.microsoft.com/en-us/azure/active-directory/reports-monitoring/concept-audit-logs             |
|Audit logs of administrator actions (user account Create / Update / Delete), or application-specific actions.         |An audit history of key changes such as rule or list updates is maintained by the application.  User account actions and corresponding audit history is controlled via AAD.  See: Overview: [Azure Active Directory reports and monitoring documentation](https://docs.microsoft.com/azure/active-directory/reports-monitoring/index) and [Audit activity reports in the Azure Active Directory portal](https://docs.microsoft.com/ azure/active-directory/reports-monitoring/concept-audit-logs).  For AZURE AD auditing, see core directory events for application role and group membership : [List of Azure Active Directory Audit Activities](https://blogs.technet.microsoft.com/motiba/2018/02/12/list-of-azure-active-directory-audit-activities/).  For access to audits from AAD Portal, see [Audit activity reports in the Azure Active Directory porta]( https://docs.microsoft.com/en-us/azure/active-directory/reports-monitoring/concept-audit-logs).               |
|  Audit logs of user actions (document or content Create / Read / Update / Delete)       |N/A.  Only the admin role supported.             |
|  Audit logs of metadata actions (Create / Read / Update / Delete).       |Yes.  Audit history of key changes such as list and rule updates are maintained.             |
|  Creation and Destruction for system-level objects as required for PCI compliant applications only.        |N/A            |
|  All logs must contain the source IP of the user.       |AAD has IP in its logs.  Certain internal logs do not have end-user IP but can be correlated with AAD information.             |
|  Audit trails on any activities performed on PII.        |The only PII is in the audit history of rule and list changes.  This is read-only and cannot be modified.               |
|Provide sample set of log data , Logs must be maintained for a period of 1 year and encrypted at rest by the vendor.         |Logs are maintained per standard Microsoft Azure Online Services policy.             |
|Does the vendor have procedures in place to detect, report and alert on the downtime of the Customer instance within an hour of the instance of being down?     |Yes            |
|  Will the application alert on unusual events, as determined by a baseline usage pattern determined by the vendor?       |Azure carve out, ISO Controls.             |
|  What information is provided to customer to validate the negotiated SLA?       |As a customer, you'll make a server to server call to the service and be able to monitor SLA directly.             |
|  How is this notification reported to me as a customer?       |No proactive downtime notification is in place. It's currently part of the roadmap.             |

### Business continuity and disaster recovery

| Question| Response    |
|---------|-------------|
|Does the application / service allow unstructured data to be exported in bulk into a non-proprietary format such as CSV?          |GDPR Export functionality only.             |
|  Does the unstructured data retain metadata?       | No            |
|  Does the unstructured data retain security ACLs?       |No             |
|  Note: Document the process.       |In product experience             |
|Does the application / service allow databases to be exported in bulk into a non-proprietary format?         |No             |
|  Note: Document the process.       |No             |
|Within the Service Level Agreement, there exists language to remove any bandwidth or API throttling in the case of legal discovery?         |--             |
|Provide a documented backup policy.         |There is no backup policy. Instead, we have multi-region data replication and resiliency strategy in place.             |
|  The policy must contain 30 days of backup, 12-hour RTO, 24-hour RPO.       |NA             |
|  Are the backups stored on the same Infrastructure vendor?       |NA             |
|  Are the backups stored encrypted at rest?         |NA             |
|  Note: Document the process.       |NA             |
|Does the application / service have a documented Disaster Recovery plan?         |Yes             |
|  Provide a business continuity runbook.       |Microsoft owned, available on request.             |
|  Note: Document the process.       |Microsoft process.             |


### Data security

| Question| Response    |
|---------|-------------|
|Does the vendor comply with the response expectations?          |Yes             |
|  Critical - same-day remediation          |Yes          | 
|  High - remediation in 5 business days    |             |
|  Medium - remediation in 15 business days |             |
|  Low - remediation in 30 business days    |             |
|  Can the vendor disable the application instance in the event of a security incident?         |Yes            |
|Does the application / service protect data using TLS encryption?         |Yes             |
|  Has SSLv3 been disabled for the application?         |Yes; disabled on all VMSS by default.             |
|  What level of encryption is being used?         |TLS 1.2             |
|What are the procedures to allow me as a customer the resources required to perform security penetration scanning?         |CELA and Security Approval from Microsoft is required.             |
|Does the application / service have a recent third-party network security penetration test? (The test must be less than 3 months old.)  |Yes, Azure             |
|Does the application / service have a recent third-party application security penetration test? (The test must be less than 3 months old.) |Yes, in house       |
|Does the application / service use a thick client or physical appliance?         |No             |
|  Is there a recent 3rd party security review available?         |N/A             |
|  Does the application/ service use a secure communications method such as TLS?   |N/A             |
|  Does the application support device pinning?       |N/A             |
|  Does the application log operational and security events?        |N/A             |
|  Describe the authentication mechanism available for the client.       |N/A             |
|  Is a secured subnet required for use?       |--             |
|  Note: Provide documentation.       |--             |
|Does the application / service have a mobile client?         |Web-based             |
|  Does the mobile client should use a secure communications method such as TLS?       |Yes             |
|  Does the application allow my own policies to enforce the presence of MDM before use?  |N/A         |
|  Is the application able to enforce data encryption?       |N/A             |
|  Is the application able to enforce a remote data wipe?       |N/A             |
|Does the application / service have a firewall in place that does not permit the application from sending traffic with a source IP or MAC address other than its own?         |Can you clarify the question?           |
|Can the application be limited to allow traffic only from trusted networks?         |It cannot be limited through the user interface, but it is possible to do so with a manual configuration.             |
|Does the application / service support Database or File Activity monitoring?         |Can you clarify the question?             |
|Does the application / service support network traffic baselining and alerting?         |Yes, through internal alerting and monitoring.             |
|Does the application have traffic reporting & the ability to alert on anomalous traffic?         |Yes, through internal alerting and monitoring.             |
|Does the application / service allow administrator control of 3rd party application integrations?|N/A             |
|  Can the administrator control OAuth or other API access per application?    |N/A             |
|  Can the administrator control OAuth or other API access using a time-lock?      |N/A             |
|  Can the administrator control OAuth or other API access using a time-lock?       |N/A             |
|  Can the administrator control OAuth or other API access per-user?        |N/A             |
|  Can the administrator control OAuth or other API access per-content-type?        |N/A             |
|  Can the application log an identifier to the application and user context under which it was authorized?       |N/A             |
|If the application / service utilizes virtual machine provisioning, provide documentation for the virtual machine migration / high availability process.         |We utilize Azure, Service Fabric, and Elastic AP.  We will comply with any request to provide additional detail for more specific questions.             |
|  Note: A virtual machine cannot be moved from a less-trusted environment to a more-trusted environment. Data should be exported, and the application built from the ground up on a trusted platform.       |--             |
|  Mixed mode (PCI and non-PCI data on the same hypervisor) must not be allowed.       |N/A           |
|If the application / service is PaaS / IaaS, my content must reside on a separate network segment and hypervisor.       |N/A             |
|If the infrastructure does not support encryption at rest by default, does the application / service provide the ability to store data at rest in an encrypted format?         |It is encrypted at rest.             |
|  All data at rest must be encrypted.    |Yes        |
|  All PaaS / IaaS VM "snapshots" must be stored on an encrypted file system.       |N/A             |
|  List the supported encryption formats.       |N/A             |
|Are there any technical requirements that would prohibit the use of a gateway encryption system such as CipherCloud?         |N/A            |
|Does the system have data retention and purge         |Yes            |
|Does the system have general retention schedule, which means the data is purged after a period?          |Yes             |
|Does the system have business justification to retain workforce data upon termination? If so, describe the justification and how long the data must be kept.           |N/A              |
|Does the system have the capability to purge the data if needed to? Describe the capability.  |N/A          |
|Do you have a well-defined security program? Provide a brief description.         |Yes             |
|Do you have someone from senior management accountable for security? Provide a name and contact information.         |Yes             |
|Does the vendor have established information security policies?         |Yes             |
|  Note: Provide a copy of all related information security policies.       |Yes             |
|Does the vendor have a third-party audit report for datacenter security and policies?         |--             |
|Furnish a copy of the report (i.e. SSAE 16 SOC 2, SAS70 Type II, etc.)         |Azure Trust Center             |
|Has the application / service performed the Cloud Security Alliance Cloud Controls Matrix (CCM) self-assessment?         |Yes             |
|  Note: Furnish a copy of the self-assessment.       |Azure Trust Center             |
|Does the vendor have a current change management policy document?         |Yes                         |
|Does the application / service have established incident response and triage policy and processes?         |Yes                          |
|  The policy must include dedicated out-of-band communications channels, incident definitions, roles and responsibilities, and resolution timelines.       |Yes                          |
|  Note: Provide a copy for review         |IcM Policy DOC             |
|Will the vendor share threat intelligence data with me?         |Yes, based on the TM not the Threat Intelligence from external bodies.             |

### Governance

| Question| Response    |
|---------|-------------|
|Do you have a well-defined security program? Provide a brief description. |Yes             |
|Do you have someone from senior management accountable for security? Provide a name and contact information.|Yes             |
|Does the vendor have established information security policies?  |Yes                         |
|Note: Provide a copy of all related information security policies.    |Yes                          |
|Does the vendor have a third-party audit report for datacenter security and policies?  |Yes             |
|Furnish a copy of the report (i.e., SSAE 16 SOC 2, SAS70 Type II, etc.).  |Azure Trust Center             |
|Has the application / service performed the Cloud Security Alliance Cloud Controls Matrix (CCM) self-assessment?         |Yes             |
|Note: Furnish a copy of the self-assessment.	         |Azure Trust Center             |
|Does the vendor have a current change management policy document?         |Yes         |
|Does the application / service have established incident response and triage policy and processes?         |Yes             |
|The policy must include dedicated out-of-band communications channels, incident definitions, roles and responsibilities, and resolution timelines.         |Yes             |
|Note: Provide a copy for review.    |IcM Policy DOC    |
|Will the vendor share threat intelligence data with me?         |Yes; based on the TM not the Threat Intelligence from external bodies.             |







