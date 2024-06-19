---
author: josaw1
description: This article provides answers to frequently asked questions (FAQ) about compliance in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 06/19/2024
ms.topic: faq
search.audienceType:
  - admin
title: Compliance FAQ
---

# Compliance FAQ

This article provides answers to frequently asked questions (FAQ) about compliance in Microsoft Dynamics 365 Fraud Protection.

#### Do staff and subcontractors who work on Fraud Protection receive regular training about data protection and information security?

Yes.

#### What information security certifications does Fraud Protection hold?

Currently, Fraud Protection holds the following information security certifications: 23 NYCRR 500, AFM and DNB (Netherlands), AMF and ACPR (France), APRA (Australia), Argentina PDPA, CDSA, CFTC 1.31, CSA STAR Attestation, CSA STAR Certification, CSA STAR Self-Assessment, Canadian Privacy Laws, DPP (UK), EU EN 301 549, EU ENISA IAF, EU Model Clauses, EU-US Privacy Shield, European Banking Authority, FCA and PRA (UK), FERPA (US), FFIEC (US), FINMA (Switzerland), FSA (Denmark), GLBA (US), GSMA SAS-SM, Germany C5, GxP (FDA 21 CFR Part 11), HIPAA and the HITECH Act (US), HITRUST, ISO 20000-1:2011, ISO 22301:2012, ISO 27001:2013, ISO 27017:2015, ISO 27018:2014, ISO 27701:2019, ISO 9001:2015, Japan My Number Act, KNF (Poland), MAS and ABS (Singapore), MPAA (US), NBB and FSMA (Belgium), NEN 7510:2011 (Netherlands), NHS IG Toolkit (UK), Netherlands BIR 2012, OSFI (Canada), OSPAR, PCI 3DS, PCI DSS Level 1, RBI and IRDAI (India), SEC 17a-4 (US), SEC Regulation SCI, SOC 1 Type 2, SOC 2 Type 2, SOC 3, SOX (US), Spain DPA, TISAX, TruSight, and WCAG 2.0.

To access the latest audit reports, see [Service Trust Portal](https://servicetrust.microsoft.com).

#### Does Fraud Protection subcontract any of its data processing activities?

No.

#### What procedures does Fraud Protection have in place for the disposal of confidential customer data?

Microsoft uses industry-standard processes to delete customer data and professional services data. Guidelines for the destruction of hard disks and offsite backup tapes have been established to ensure appropriate disposal.

#### How is data confidentiality ensured in Fraud Protection?

Fraud Protection requires that all access be authenticated with Microsoft Entra and implements role-based access control to prevent unauthorized access by other customers. Fraud Protection also follows many internal security procedures to authorize and audit all access to data by Microsoft personnel, and to allow access only when it's required to ensure service stability and resolve issues.

As is stated in the Microsoft data protection addendum on the [Licensing Documents](https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA) page of the Microsoft Licensing Resources and Documents site:

> Microsoft will ensure that its personnel engaged in the processing of Customer Data, Professional Services Data, and Personal Data will process such data only on instructions from Customer or as described in the data protection addendum, and will be obligated to maintain the confidentiality and security of such data even after their engagement ends. Microsoft shall provide periodic and mandatory data privacy and security training and awareness to its employees with access to Customer Data, Professional Services Data, and Personal Data in accordance with applicable Data Protection Requirements and industry standards.

#### Is Fraud Protection subject to any legal or regulatory requirements that are related to security? If so, what are they, and how is Fraud Protection meeting them?

Microsoft is subject to various legal and regulatory obligations. For information about security, privacy, and compliance, see [Microsoft Trust Center](https://www.microsoft.com/trustcenter/default.aspx).

#### What steps does Fraud Protection take to ensure the accuracy of the user data that it collects and maintains?

It's the responsibility of the merchant to ensure the accuracy of the data.

#### Does Fraud Protection give users access to data that it collected about them, so that they can correct any inaccuracies?

No. Users who want to update or access their data should do so through the merchant.

Fraud Protection provides tools to help customers manage Data Subject Access Requests (DSARs). For more information, see [Security measures for protecting data](../compliance-and-security.md).

#### Does Fraud Protection regularly conduct internal audits, as prescribed by industry best practices and guidance? Are the audit results available to the customers?

Fraud Protection follows a Microsoft-wide cadence of internal and external audits. Internal audit results aren't provided to the customers. However, all external audit results are published to the [Service Trust Portal](https://servicetrust.microsoft.com). For more information, see [Operational Security Assurance (OSA)](https://www.microsoft.com/securityengineering/osa).

#### Does Fraud Protection produce audit assertions in a structured, industry-accepted format?

Yes. As a software as a service (SaaS) application, Fraud Protection runs on Azure, and includes ISO 27001, 27018, SOC2, SOC3, and PCI compliance. In addition, Azure covers a wide range of industry compliance for all the services in Azure that Fraud Protection relies on.

#### What is the retention period of data in the Fraud Protection Network?

Data processed within the Fraud Protection network is pseudonymized and retained for 24 months. Authorized Microsoft personnel may access your data for the purposes of providing Online Services or Professional Services, in accordance with Microsoft policy. To learn more about how Microsoft handles your data, visit [Microsoft Product and Services Data Protection Addendum (DPA)](https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA?lang=1)

#### Which persons within Fraud Protection have access to Customer Data?

Please note that Microsoft employees, including Microsoft-approved subcontractors, may access Customer Data with the permission of the Customer for the purposes of providing Online Services or Professional Services. Data related to a transaction is deidentified and aggregated prior to transmission into the fraud network. Microsoft employees may access aggregated data related to a transaction in the fraud network for the purposes of improving the Online Services. 

#### Does Fraud Protection use cookies in device fingerprinting?

Yes. Fraud Protection uses cookies to collect information for a device, not for a particular individual. To opt out of using cookies you can, but it would degrade the device fingerprinting.

#### Is Fraud Protection device fingerprinting affected by ad blockers?

If DNS/SSL certificate information is properly set up for [web integration](../df-web.md), then the fingerprinting script will be considered a first party integration and will be excluded from most ad blockers. 

## Additional resources

[EU Data Boundary exceptions for Fraud Protection](../edbd.md)

[Service FAQ](service-faq.md)

[Legal considerations FAQ](legal-faq.md)

[Privacy and security FAQ](privacy-security-faq.md)

[Data residency FAQ](data-residency-faq.md)
