---
author: cschlegel2
description: This article describes how Microsoft Dynamics 365 Fraud Protection account protection works.
ms.author: cschlegel
ms.date: 10/27/2022
ms.topic: reference
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - Admin
  - IT Pro
title: How account protection works
---

# How account protection works

This article describes how Microsoft Dynamics 365 Fraud Protection account protection works.

This article provides visual abstract representation and description of how Microsoft Dynamics 365 Fraud Protection – Account Protection interacts with our customers to support their users. 

Dynamics 365 Fraud Protection provides merchants with the capability to assess if attempts to create new accounts and attempts to sign in to a merchant's ecosystem are fraudulent. Risk assessment in Fraud Protection can be used by customers to block or challenge suspicious attempts to create new fake accounts or to compromise existing accounts. 

The following illustration highlights some of Fraud Protection's capabilities and application programming interfaces (APIs) to help you better understand risk assessment interactions.

![Abstract overview of how Fraud Protection account protection works](media/architecture-abstract1-overview.png)

- **Device fingerprinting (1)** - Device fingerprinting lets you collect crucial device telemetry during online actions. This information includes hardware information, browser information, geographic information, and the Internet protocol (IP) address used. This feature is based on artificial intelligence (AI) and can be used as input to the fraud assessments process. A Java-based web software development kit (SDK) is available, as are iOS, Android, and React Native SDKs for mobile applications.
- **Account payload (2)** - Information related to the account creation or account sign-in that customers pass along to Fraud Protection. This data is compared to data already within the Fraud Protection network, where the machine learning model analyzes the data for linkages. 
- **Risk assessment (3)** - The machine learning model can return a score to you for bot and risk scores. The scoring advises you of the probability of fraud risk, or the likelihood of possible fraud that you may want to review or reject.  

<!--
On the left side of the illustration above, you can see these are the Dynamics 365 Fraud Protection customers and our merchant's customers. For example, if a user is creating a new account or signing into an existing account, the merchant or payment service provider (PSP) can add Fraud Protection's device fingerprinting to their user interfaces (UIs), so that when someone is interacting to access a website, we are collecting device forensics. We then assign a unique device ID to the session to help identify whenever the user completes some specific event such as an account creation or account login attempt.   

When a new account is created or if an account sign-in takes place, there is an API from Fraud Protection side that is being called with specific information, to then pass along to Dynamics 365 Fraud Protection **(number 2)**. Then that data is compared to the data already within our fraud protection network. Our machine learning will then try to find linkages and see past behavior coming from data attributes such as IP address, geo location, email address, phone number, and other system information. There are many other device fingerprinting attributes, as well as other data attributes related to the activity of the entities within the transaction such as velocities or the timing of login attempts. For example, how frequently are we seeing some activity coming from the same account; and then these data attributes that are sent through machine learning analysis to enable us to then return a fraud risk score to you. 

Then on top of the machine learning analysis, there are some simple predefined rules that  Dynamics 365 Fraud Protection customers can set up or you can set up your own custom rules, which would give a response back to you saying the probability the login transaction is fraudulent, with this kind of fraud risk or bot score, and along with the reason for the decision that was made.    

As you can see in **(number 3)**, Risk Assessment. These device attributes go into the Dynamics 365 Fraud Protection machine learning model with which we then return a score to you for bot and risk scores. The scoring is important because it tells you the probability of fraud risk, or the likelihood of fraud that you may want to consider reviewing or rejecting. The lower the score, the less likelihood of fraud and the higher the score, the greater probability of fraud.  
-->
## Required APIs and components
 
 The following APIs and components are required to take advantage of Fraud Protection account protection's features.

- **Device fingerprinting** - Device fingerprinting lets you collect crucial device telemetry during online actions. This information includes hardware information, browser information, geographic information, and the Internet Protocol (IP) address. This feature is based on artificial intelligence (AI) and can be used as input to the process of fraud assessments. A Java-based web SDK and iOS, Android and React Native SDKs for mobile applications are available.

- **Account creation and/or account sign-in API** - Data attributes our customers pass along to Dynamics Fraud Protection related to the Account Creation or Account Login. This data is compared to data already within our fraud protection network where our machine learning will look for linkages. 

- **Rules or policies** - There are predefined rules in the Account Protection solution, or you can set up custom rules based on your policies. The rule scoring can tell you the probability of fraud risk, or the likelihood of fraud that you may want to review or reject. 

- **Account status API** - Used to inform Dynamics Fraud Protection of the merchant’s final decision on a transaction.  For example, did the login transaction actually happen or was it rejected for what reason.  It is important to let Dynamics Fraud Protection adapt and learn from the merchant’s fraud patterns. 

- **Account label API** - Enables you to send additional information to Dynamics Fraud Protection in addition to the data that informs the virtual fraud analyst and scorecard features. The labels API provides additional knowledge for model training based on an additional set of fraud signals.

## How Fraud Protection account protection connects with customer front and back ends

The following illustration shows how Fraud Protection account protection typically connects with customers' front and back ends. For example, at what stage of the process does an API call take place, which API is called, and which Dynamics 365 components return information to customers.

The numbered elements in the illustration are further explained below the diagram.

![Account Protection Integration Abstract](media/ap-architecture-rev-diagram2-abstract.png)

**Device fingerprinting (1), front end** - Fraud Protection's device fingerprinting feature is based on artificial intelligence (AI), and device identification can be used as input to the fraud assessment process. This feature helps Fraud Protection track and link unrelated events in the fraud network to help identify patterns of fraud. The data collected is not just a static list of attributes but also includes dynamically captured data based on the evaluation of specific combinations of attributes such as browser, system, network, and geolocation coordinates. When device characteristics and attributes are collected, the device fingerprinting service uses machine learning to probabilistically identify the device. For example, when a user is entering their credentials, the device fingerprinting will look to do an authentication layer to help determine that the credentials are correct, and that this is in fact the right username and password combination. Device fingerprinting runs on Azure, and includes benefits from proven cloud scalability, reliability, and enterprise-grade security. Merchants and PSPs have control of their user experience (UX) and systems and can decide to implement Fraud Protection's device fingerprinting service on the front-end.  

**Account sign up or account sign-in API (2)** - This is the first API call. However, device fingerprinting is technically the first time you are communicating with Fraud Protection account protection. There is a common link between device fingerprinting and the Account sign up or account sign-in API calls. For example, when you initiate device fingerprinting, you create a unique device context ID that you include when you make the second API call. 

**Data enrichment (3)** - Data enrichment helps connect device fingerprinting, account sign up, and account sign-in. Fraud Protection account protection does some data enrichment before running the data attributes through the bot, account creation, and account sign-in models. 

**Dynamics Fraud Protection AI model (4, 5)** - Within a few milliseconds of the data attributes going through the AI models, you get a response through to Fraud Protection rules and decisions. Fraud Protection then provides a bot and risk score (5, back end) in the response based on the machine learning scores. 

**Rules engine (6)** - The output of the scores and decisions is dependent on the customer policies set in the Fraud Protection rules engine. The scores provided are based on a risk or bot scale, with a lower score indicating less fraud, and a higher score indicating the likelihood of fraud. There are four decisions that you can make: approve, reject, challenge, or review. A challenge decision indicates that you should possibly implement a capture or some other type of verification challenge. A review decision typically indicates that you should do a manual review. The decisions are recommendations from Fraud Protection that are based on the policies that have been configured in the rules engine. It is up to you what rules or decisions you want to set up or activate.

**Account sign-in or account creation status API (7)** - Fraud Protection wants to know what final status decision you made on the account attempt. For example, did you approve or reject? The account status that you send back to Fraud Protection helps ensure that the right information is being considered in machine learning going forward. 

**Scorecards (8)** - Transactions that come through from you to Fraud Protection also make their way into scorecard dashboards. The scorecard dashboard isn't in real time, but updates every few minutes to show you the aggregated data and trends that Fraud Protection has received. 

**Rules updates (9)** - You may decide that you need to update some of your rules or policies. For example, a member of your team reviews the scorecard dashboards, and you decide to update rules or policies based on what you see in those scorecards.  

**Label API (10)** - The label API enables you to send additional information to Fraud Protection about account sign-in attempts, instrument details, and reversals, in addition to the data that informs the virtual fraud analyst and scorecard features. The labels API provides knowledge for model training based on a set of fraud signals. 


