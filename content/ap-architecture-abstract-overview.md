---
author: cschlegel2
description: This article is a visual abstract of how Dyanmics 365 Fraud Protection Account Protection Works
ms.author: cschlegel
ms.date: 10/27/2022
ms.topic: reference
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - Admin
  - IT Pro
title: Abstract Diagram of How Dynamics 365 Fraud Protection - Account Protection Works
---

# Abstract Diagram of How Dynamics 365 Fraud Protection - Account Protection Works

This article provides visual abstract representation and description of how Microsoft Dynamics 365 Fraud Protection – Account Protection interacts with our customers to support their users. Microsoft Dynamics 365 Fraud Protection provides merchants the capability to assess if the risk of attempts to create new accounts and attempts to log in on merchant’s ecosystem are fraudulent. Risk assessment in Fraud Protection can be used by the customer to block or challenge suspicious attempts to create new fake accounts or to compromise existing accounts. The diagram below highlights some of the product capabilities and APIs (Application Programming Interfaces) to help you better understand these interactions. Particularly for Account Create and Account Login scenarios.

![overview 1](media/architecture-abstract1-overview.png)

- **1.Device Fingerprinting:** Device fingerprinting lets you collect crucial device telemetry during online actions. This information includes hardware information, browser information, geographic information, and the Internet Protocol (IP) address. This feature is based on artificial intelligence (AI) and can be used as input to the process of fraud assessments. A Java-based web SDK (software development kits) and iOS, Android and React Native SDKs for mobile applications are available.

- **2.Account Payload:** Information our customers pass along to Dynamics Fraud Protection related to the Account Creation or Account Login. This data is then compared to data already within our fraud protection network where our machine learning will look for linkages. 

- **3.Risk Assessment:** The machine learning model can then return a score to you for bot and risk scores. The scoring can tell you the probability of fraud risk, or the likelihood of possible fraud that you may want to review or reject.  

At elevated level this is how Dynamics 365 Fraud Protection works for Account Protection.  

On the left-hand side. You can see these are the Dynamics 365 Fraud Protection customers and our merchant’s customers. For example, if an end user is creating a new account or logging into an existing account, the merchant or PSP (Payment Service Provider) can add Dynamics Fraud Protection’s device fingerprinting **(number 1 and 2)** in their UI (user interfaces), so that when someone is interacting to access a website, we are collecting device forensics. We then assign a unique device ID to the session to help identify whenever the user completes some specific event such as an account creation or account login attempt.   

When a new account is created or if an account login takes place, there is an API from Dynamics 365 Fraud Protection side that is being called with specific information, to then pass along to Dynamics 365 Fraud Protection **(number 2)**. Then that data is compared to the data already within our fraud protection network. Our machine learning will then try to find linkages and see past behavior coming from data attributes such as IP address, geo location, email address, phone number, and other system information. There are many other device fingerprinting attributes, as well as other data attributes related to the activity of the entities within the transaction such as velocities or the timing of login attempts. For example, how frequently are we seeing some activity coming from the same account; and then these data attributes that are sent through machine learning analysis to enable us to then return a fraud risk score to you. 

Then on top of the machine learning analysis, there are some simple predefined rules that  Dynamics 365 Fraud Protection customers can set up or you can set up your own custom rules, which would give a response back to you saying the probability the login transaction is fraudulent, with this kind of fraud risk or bot score, and along with the reason for the decision that was made.    

As you can see in **(number 3)**, Risk Assessment. These device attributes go into the Dynamics 365 Fraud Protection machine learning model with which we then return a score to you for bot and risk scores. The scoring is important because it tells you the probability of fraud risk, or the likelihood of fraud that you may want to consider reviewing or rejecting. The lower the score, the less likelihood of fraud and the higher the score, the greater probability of fraud.  

**API Abstract Diagram** - Below is an abstract diagram of how Microsoft Dynamics 365 Fraud Account Protection typically connects with our customer’s front and back end. For example, at what time in the process does and API call take place, to which API, and what Microsoft Dynamics 365 components would then return to our customers. 

 ![overview 2](media/ap-architecture-rev-diagram2-abstract.png)

 **Microsoft Dynamics 365 Fraud Protection Customers Will Need to Set Up these APIs or Components:** 

- **Device Fingerprinting:** Device fingerprinting lets you collect crucial device telemetry during online actions. This information includes hardware information, browser information, geographic information, and the Internet Protocol (IP) address. This feature is based on artificial intelligence (AI) and can be used as input to the process of fraud assessments. A Java-based web SDK and iOS, Android and React Native SDKs for mobile applications are available.

- **Account Creation and/or Account Login API:** Data attributes our customers pass along to Dynamics Fraud Protection related to the Account Creation or Account Login. This data is compared to data already within our fraud protection network where our machine learning will look for linkages. 

- **Rules or Policies:** There are predefined rules in the Account Protection solution, or you can set up custom rules based on your policies. The rule scoring can tell you the probability of fraud risk, or the likelihood of fraud that you may want to review or reject. 

- **Account Status API:** Is used to inform Dynamics Fraud Protection of the merchant’s final decision on a transaction.  For example, did the login transaction actually happen or was it rejected for what reason.  It is important to let Dynamics Fraud Protection adapt and learn from the merchant’s fraud patterns. 


- **Account Label API:** Enables you to send additional information to Dynamics Fraud Protection in addition to the data that informs the virtual fraud analyst and scorecard features. The labels API provides additional knowledge for model training based on an additional set of fraud signals.

**Device Fingerprinting (#1, front end)** On the left-hand side of the above diagram we have Device Fingerprinting for both a Java-based web SDK and iOS, Android and React Native SDKs for mobile applications are available. Merchants or PSPs (Payment service providers) have control of their UX (user experience) and systems and can decide to implement Dynamics Fraud Protection’s Device Fingerprinting on the front-end side. Device fingerprinting lets you collect crucial device telemetry during online actions. This information includes hardware information, browser information, geographic information, and the Internet Protocol (IP) address. Microsoft Dynamics 365 Fraud Protection provides a device fingerprinting feature that is based on artificial intelligence (AI). Therefore, device identification can be used as input to the process of fraud assessment. Additionally, this feature helps the Fraud Protection service track and link unrelated events in the fraud network, to help identify patterns of fraud. The data collected is not just a static list of attributes but also includes data dynamically captured based on the evaluation of specific combinations of attributes, such as browser, system, network, and geo-location attributes. When device characteristics and attributes are collected, the device fingerprinting service uses machine learning to probabilistically identify the device. For example, when a user is entering their credentials the device fingerprinting will look to do an authentication layer, to help determine that the credentials are correct, and this is in fact the right username and password combination if it passes. Device fingerprinting runs on Azure, and includes benefits from proven cloud scalability, reliability, and enterprise-grade security.   

 

**Account Sign Up or Account Login API (#2):** This is the first API call. However, device fingerprinting seen in number 1 is technically the first time you are communicating with Microsoft Dynamics 365 Account Protection. There is a common link between device fingerprinting and the Account Sign Up or Account Login API calls, for example when you initiate device fingerprinting, you will create what we call unique device context ID, and you will include that when you make the second API call. 

**Data Enrichment (#3):** Data enrichment helps us to connect the Device Fingerprinting, Account Sign Up and Account Login together. We do a bunch of data enrichments (number 3), run it through our models (number 4). 

**Dynamics Fraud Protection AI Model (#4 & #5):** Within a few milliseconds of these data attributes going through our AI models, you get a response through to Dynamics Fraud Protection rules and decisions. Dynamics Fraud Protection will then provide a Bot & Risk Score (#5 back end) in the response based off the Machine Learning scores. 

**Rules Engine (#6):** The output of the scores and decisions is dependent on the customer policies set in the Rules Engine. The scores provided will be based on a risk or bot scale with the closer the result is to zero indicates less fraud and a higher score indicates the likelihood of fraud. Decisions are all driven by the policies in the rules you configured.  There are four decisions that you can make Approve, Reject, Challenge, or Review. Challenge would indicate that possibly you should issue, for example a capture challenge or some other kind of verification challenge and review is typically used for a manual review. The decisions are recommendations from Dynamics Fraud Protection based on what you configured in the rules engine. It is up to you what rules or decisions you want to set up or activate. 

**Account Login or Account Create Status API (#7):** Dynamics Fraud Protection wants to know what the final status decision our customers made on the account attempt. For example, did you approve or reject? The Account Status that you send back to Dynamics Fraud Protection will help ensure the right information is being considered in our machine learning going forward and helps with the robust reporting that we provide you. 

 

**Scorecards (#8):** Transactions that are coming through from you to Dynamics Fraud Protection will also make their way into our scorecard dashboards. The scorecard dashboard is not instantaneous, but every few minutes your scorecard will update and show you the aggregated data and trends that we have received. 

**Rules Updates (#9):** For example, a member of your team can login and review the scorecard dashboards, and based on what you see in those scorecards, you might decide that you may need to update some of your rules or policies.  

**Label API (#10):** The Label API enables you to send additional information to Microsoft Dynamics 365 Fraud Protection in addition to the data that informs the virtual fraud analyst and scorecard features. The labels API provides additional knowledge for model training based on an additional set of fraud signals. Labels are charged by manual review and any other way you can confirm fraud. As well as any additional data or not required data that you can provide to DFP (Dynamics 365 Fraud Protection) to help improve the machine learning and reporting we provide you. You can use the Fraud Protection Label API to send information about account login attempts, instrument details, and reversals. 
