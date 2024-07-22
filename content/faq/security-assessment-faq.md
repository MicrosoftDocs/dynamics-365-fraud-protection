---
author: josaw1
description: This article provides answers to frequently asked questions about security assessment in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 12/02/2022
ms.topic: conceptual
search.audienceType:
 - admin
title: Security assessment FAQ 
---

# Security assessment FAQ

This article provides answers to frequently asked questions about security assessment in Microsoft Dynamics 365 Fraud Protection.

## Authentication and administration
 
#### Does the application or service support single sign-on (SSO) through Security Assertion Markup Language (SAML) 1.1, SAML 2.0, or Web Services Federation (WS-Fed)?

Yes.

- **Portal:** SPA - OAuth 2.0 and OpenID Connect, using authentication code flow with PKCE via the [MSAL v2 library](https://github.com/AzureAD/microsoft-authentication-library-for-js).
- **Service-to-service backend API:** OAuth 2.0
- **Fingerprinting service:** Anonymous
- **Azure Stack:** Shared access signature (SAS) token for storage

#### Is there a "back door" URL that lets users or administrators bypass SSO?

No. 

#### Does the application support Okta integration (SSO platform)?

Okta integration isn't supported by default. Microsoft Entra supports custom integrations. Because the merchant owns the tenant, the merchant can take advantage of Microsoft Entra identity integration points. For more information, see the [Microsoft Entra documentation](/azure/active-directory/).

#### Does the application or service support two-factor authentication (2FA)?

Yes. The merchant can enable 2FA in Microsoft Entra ID.
 
#### What is the 2FA solution?

The 2FA solution is Azure Multi-Factor Authentication, a Microsoft Entra feature. For more information, see [How it works: Azure Multi-Factor Authentication](/azure/active-directory/authentication/concept-mfa-howitworks).
 
#### Does the application support application-level passwords?

No. User and application identities are managed in the customer's Microsoft Entra account. 
 
#### Which hash or encryption algorithm is used to protect passwords?

Not applicable.
 
#### Is hash salting used?

Not applicable.
 
#### Does the application or service use automatic account provisioning? If so, how is it accomplished (for example, on-demand via SAML, automated comma-separated values [CSV] feed over secure transmission, or API)?

No, and not applicable. 
 
#### Does the application or service use immediate account access termination, including closing open sessions?

No. Microsoft Entra token expiration is aligned with user access termination, not the session. 

#### If account termination isn't automatic, is this action performed within one hour of an account access termination request?

Yes, per Microsoft Entra policy. For more information, see the [Microsoft Entra documentation](/azure/active-directory/).

#### What is the session idle time-out of the application?

Per Microsoft Entra policy, the session idle time-out is aligned with the token validity period. 
 
#### Does the application or service use an automatic account deprovisioning process via an API?

No. 
 
#### Does the application or service provide a disposition strategy for content that is attached to a user's account upon deprovisioning?

No. Only audit logs are tracked and retained as features per Online Services Terms (OST) guidelines and the Microsoft Privacy Statement. 
 
#### Does the application or service let the administrator explicitly grant authorization to data and capabilities based on role and/or function, according to the least privilege model?

Yes. Via Microsoft Entra roles, administrators can grant access within their tenant. 
 
#### A minimum expectation is support for the administrator role, user role, read-only administrator (log) role, and unprivileged administrator (no access to content) role. Do you provide this support?

The application/service doesn't have any roles except the administrator role. Users in the administrator role are responsible for creating additional roles within their tenant. For information about how to add and remove roles, see [Configure user access](../configure-user-access.md). 
 
#### If there are sharing permissions in the application, does the application or service let the administrator review user requests for additional access to data?

Not applicable. 
 
#### Does the application or service let the administrator user distinguish administrator users and regular users?

No.

#### What rights are available for the various roles in the application or service?

For more information, see [User roles and access](../user-roles-access.md).

## Auditing

#### Does the application or service log information in an industry-standard type of event format, such as CSV, Common Event Format (CEF), or Syslog?

Log data isn't shared by the product. Service metrics and key performance indicators (KPIs) are available via Power BI views.

#### Does the application or service collect or provide data about user sign-in, sign-out, password changes, and failed sign-in attempts?

Yes. For more information, see [Audit activity reports in the Microsoft Entra portal](/azure/active-directory/reports-monitoring/concept-audit-logs).

#### Does the application or service collect or provide audit logs of administrator actions (user account create/update/delete) or application-specific actions?

The application maintains an audit history of key changes, such as rule or list updates. User account actions and corresponding audit history are controlled via Microsoft Entra ID. For more information, see [Microsoft Entra reports and monitoring documentation](/azure/active-directory/reports-monitoring).
 
For information about Microsoft Entra auditing, see the core directory events for application role and group membership in [List of Microsoft Entra Audit Activities](/archive/blogs/motiba/list-of-azure-active-directory-audit-activities). For access to audits from the Microsoft Entra portal, see [Audit logs in Microsoft Entra ID](/azure/active-directory/reports-monitoring/concept-audit-logs).

#### Does the application or service collect or provide audit logs of user actions (document or content create/read/update/delete)?

Not applicable. Only the administrator role is supported.

#### Does the application or service collect or provide audit logs of metadata actions (create/read/update/delete)?

Yes. An audit history of key changes, such as list and rule updates, is maintained.

#### Can Microsoft provide audit trails for any activities that are performed on personally identifiable information (PII)?

The only PII is in the audit history of rule and list changes. This history is read-only and can't be modified.

#### Can Microsoft store logs and encrypted data at rest?

Logs are maintained per standard Microsoft Azure Online Services policy.

#### Does Microsoft have procedures in place to detect, report, and alert about the downtime of the customer instance within a reasonable time frame if the instance is down?

Yes, advanced monitoring and alerting capabilities are in place.

#### What information is provided to customers to validate the negotiated service level agreement (SLA)?

As a customer, you can make server-to-server calls to the service and monitor the SLA directly.

#### How is downtime notification reported to customers?

No proactive downtime notification is in place, but it's currently part of the roadmap. Customers are notified about any incidents that are discovered via alerting through the standard communications channel.

## Business continuity and disaster recovery

#### Does the application or service enable unstructured data to be exported in bulk in a non-proprietary format, such as CSV?

In the product, the General Data Protection Regulation (GDPR) experience lets users export data under the guidelines that are described in the [Compliance documentation](../security-compliance.md). 

#### Does the unstructured data retain security access control lists (ACLs)?

No. For more information, see [Data Subject Requests and the GDPR and CCPA](/compliance/regulatory/gdpr-data-subject-requests).

#### Does the application or service enable databases to be exported in bulk in a non-proprietary format?

No.

#### Is there a documented backup policy?

A multi-region data replication and resiliency strategy is in place. For more information about the backup and restore capability, see [Online backup and on-demand data restore in Azure Cosmos DB](/azure/cosmos-db/online-backup-and-restore).

#### Does the application or service have a documented disaster recovery plan?

For more information about the Microsoft enterprise business continuity management (EBCM) plan, see the [Enterprise Business Continuity Management Program white paper](https://go.microsoft.com/fwlink/?linkid=2121521). (Sign-in is required.)

## Data security

#### Can Microsoft disable the application instance in the event of a security incident?

Yes.

#### Does the application or service protect data by using Transport Layer Security (TLS) encryption?

Yes.

#### What level of TLS encryption is used?

TLS 1.2.

#### What are the procedures for allowing customers to access the resources that are required to do security penetration scanning?

Corporate, External, & Legal Affairs (CELA) and security approval from Microsoft are required.

#### Does the application or service have a recent (less than three months old) third-party network security penetration test?

Yes. Azure periodically performs this test.

#### Does the application or service have a recent (less than three months old) third-party application security penetration test?

Yes. This test will be provided on request.

#### Does the application or service use a secure communications method, such as TLS?

Yes.

#### Does the application or service have a mobile client?

Fraud Protection is a web-based software as a service (SaaS) offering.

#### Can the application be limited so that it allows traffic only from trusted networks?

The application can't be limited through the user interface (UI). However, it can be limited through manual configuration.

#### Does the application have traffic reporting and the ability to alert about normal traffic?

Yes. These capabilities are available through internal alerting and monitoring. For more information, see [API call monitoring](../monitoring.md).

#### If the infrastructure doesn't support encryption at rest by default, does the application or service enable data at rest to be stored in an encrypted format?

All data is encrypted at rest. For more information, see [Data encryption in Azure Cosmos DB](/azure/cosmos-db/database-encryption-at-rest).

#### Does the system have a general retention schedule, so that data is purged after a period?

Yes. For more information, see the [Online Services Terms (OST)](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/all) guidelines.

## Governance

#### Do you have a well-defined security program?

Yes. For information, see [Microsoft Security Development Lifecycle (SDL)](https://www.microsoft.com/securityengineering/sdl/).

#### Does Microsoft have established information security policies?

Yes. For information, see the [Microsoft Security Development Lifecycle (SDL)](https://www.microsoft.com/securityengineering/sdl/).

#### Does Microsoft have a third-party audit report for datacenter security and policies that I can access?

Yes. For more information, visit the [Microsoft Service Trust Portal](https://servicetrust.microsoft.com/ViewPage/TrustDocuments?command=Download&downloadType=Document&downloadId=64f922a6-d624-40dd-a8ae-6f996b5186f3&docTab=6d000410-c9e9-11e7-9a91-892aae8839ad_FAQ_and_White_Papers).

#### Has the application or service completed the Cloud Security Alliance CCM self-assessment? If so, can I access it?

Yes. Visit the [Microsoft Service Trust Portal](https://servicetrust.microsoft.com/ViewPage/TrustDocuments?command=Download&downloadType=Document&downloadId=64f922a6-d624-40dd-a8ae-6f996b5186f3&docTab=6d000410-c9e9-11e7-9a91-892aae8839ad_FAQ_and_White_Papers).
 
#### Does Microsoft have a current change management policy document?

Yes.

#### Does the application or service have an established incident response and triage policy and established processes?

Yes.
 
## Additional resources
 
[Service FAQ](service-faq.md)

[Legal considerations FAQ](legal-faq.md)

[Privacy and security FAQ](privacy-security-faq.md)

[Data residency FAQ](data-residency-faq.md)

[Compliance FAQ](compliance-faq.md)

[EU Data Boundary exceptions for Fraud Protection](../edbd.md)

[!INCLUDE[footer-include](../includes/footer-banner.md)]