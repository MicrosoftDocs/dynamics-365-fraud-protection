---
author: josaw1
description: This topic provides frequently asked questions and answers (FAQ) about compliance in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 06/01/2022
ms.topic: faq
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Compliance FAQ
---

# Compliance FAQ

1.  Are all the staff and sub-contractors working at Fraud Protection receive regular trainings on data protection and information security?

Yes

2.  What information security certifications does Fraud Protection hold?

Currently, 23 NYCRR 500, AFM and DNB (Netherlands), AMF and ACPR (France), APRA(Australia), Argentina PDPA, CDSA, CFTC 1.31, CSA STAR Attestation, CSA STAR Certification, CSA STAR Self-Assessment, Canadian Privacy Laws, DPP(UK), EU EN 301 549, EU ENISA IAF, EU Model Clauses, EU-US Privacy Shield, European Banking Authority, FCA and PRA (UK), FERPA (US), FFIEC(US), FINMA (Switzerland), FSA (Denmark), GDPR, GLBA (US), GSMA SAS-SM, Germany C5, GxP (FDA 21 CFR Part 11), HIPAA and the HITECH Act (US), HITRUST, ISO 20000-1:2011, ISO 22301:2012, ISO 27001:2013, ISO 27017:2015, ISO 27018:2014, ISO 27701:2019, ISO 9001:2015, Japan My Number Act, KNF(Poland), MAS and ABS (Singapore), MPAA(US), NBB and FSMA (Belgium), NEN 7510:2011 (Netherlands), NHS IG Toolkit (UK), Netherlands BIR 2012, OSFI(Canada), OSPAR, PCI 3DS, PCI DSS Level 1, RBI and IRDAI (India), SEC 17a-4 (US), SEC Regulation SCI, SOC 1 Type 2, SOC 2 Type 2, SOC 3, SOX (US), Spain DPA, TISAX, TruSight, WCAG 2.0

Visit <https://servicetrust.microsoft.com/> to access the latest audit reports.

3.  Does Fraud Protection subcontract any of its data processing activities?

No

4.  What procedures does Fraud Protection have in place for disposal of confidential customer data?

Microsoft uses industry standard processes to delete Customer Data and Professional Services Data. Hard disk and offsite backup tape destruction guidelines have been established for appropriate disposal.

5.  How is data confidentiality assured within Fraud Protection?

Fraud Protection requires all access be authenticated with AAD and implements role-based access control to prevent unauthorized access by another customer and that it follows many security procedures internally to authorize and audit all access to data by Microsoft personnel and allow it only when required to ensure service stability and resolve issues.

As stated in the Microsoft data protection addendum ([Licensing Documents (microsoft.com)](https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA) ):

Microsoft will ensure that its personnel engaged in the processing of Customer Data, Professional Services Data, and Personal Data will process such data only on instructions from Customer or as described in the data protection addendum, and will be obligated to maintain the confidentiality and security of such data even after their engagement ends. Microsoft shall provide periodic and mandatory data privacy and security training and awareness to its employees with access to Customer Data, Professional Services Data, and Personal Data in accordance with applicable Data Protection Requirements and industry standards.

6.  Is Fraud Protection subject to any legal or regulatory requirements related to security? If yes, list all those requirements and how Fraud Protection is meeting those requirements.

Microsoft is subject to various legal and regulatory obligations. Information concerning security, privacy or compliance can be found at the Microsoft Trust Center ([<u>https://www.microsoft.com/trustcenter/default.aspx</u>](https://www.microsoft.com/trustcenter/default.aspx)).

7.  What steps does Fraud Protection take to ensure accuracy of the end user data collected and maintained?

It is the responsibility of the merchant to ensure the accuracy of the data.

8.  Does Fraud Protection provide end users access to data that Fraud Protection collected about them, to allow users to correct any inaccuracies in the data?

No. Any end user wishing to update or access their information should do so through the merchant. That said, Fraud Protection provides customers with tools to assist in managing "End User Data Subject Access Requests".

More details can be found here: <https://docs.microsoft.com/en-us/dynamics365/fraud-protection/security-compliance>

9.  Does Fraud Protection conduct internal audits regularly as prescribed by industry best practices and guidance? Are the audit results available to the customers?

Fraud Protection follows a Microsoft wide cadence of internal and external audits. Internal audit results are not provided to the customers; however, all the external audit results are published in Service Trust Portal. Customers can access all External Audit reports at [<u>https://servicetrust.microsoft.com</u>](https://servicetrust.microsoft.com); [<u>https://www.microsoft.com/en-us/securityengineering/osa</u>](https://www.microsoft.com/en-us/securityengineering/osa)

10. Does Fraud Protection produce audit assertions using a structured, industry accepted format (ex. CloudAudit/A6 URI Ontology, CloudTrust, SCAP/CYBEX, GRC XML, ISACA's Cloud Computing Management Audit/Assurance Program, etc.)?

Yes. Fraud Protection as a SaaS service runs on Azure and comes with ISO 27001, 27018, SOC2, SOC3 and PCI compliance. Also, Microsoft Azure covers a wide range of Industry compliance for all the services within Azure which Fraud Protection relies on.
