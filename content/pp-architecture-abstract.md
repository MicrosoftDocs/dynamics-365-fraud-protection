author: cschlegel2
description: This article explains Dynamics Fraud Protection - purchase protection architecture abstract diagram
ms.author: cschlege2
ms.date: 10/14/2022
ms.topic: reference
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - Admin
  - IT Pro
title: Visual Abstract of How Dynamics 365 Fraud Protection - Purchase Protection Works 
ms.custom:

This article provides visual abstract representation and description of how Microsoft Dynamics 365 Fraud Protection – Purchase Protection interacts with various entities such as customers and banks. The diagram below highlights at an elevated level some of the product capabilities and APIs (Application Programming Interfaces) to help you better understand these interactions.  


![overview diagram](media/pp-architecture-abstract1.png)

**The areas in the above diagram include:** 

- **1.Device Fingerprinting:** Device fingerprinting lets you collect crucial device telemetry during online actions. This information includes hardware information, browser information, geographic information, and the Internet Protocol (IP) address. This feature is based on artificial intelligence (AI) and can be used as input to the process of fraud assessments. It can be deployed for both browser based and mobile based applications. There is a Java-based web SDK (software development kits) and iOS, Android and React Native SDKs for mobile applications are available.

- **2.Transaction Payload:** Information our customers pass along to Dynamics Fraud Protection related to the transaction. This data is then compared to data already within our fraud protection network where our machine learning will look for linkages. 

- **3.Risk Assessment:** The machine learning model can then return a risk score. The scoring can tell you the probability of fraud risk, or the likelihood of possible fraud that you may want to review or reject. 

- **4.Trust Knowledge (Transaction Acceptance Booster):** This feature helps you benefit from higher acceptance rates by sharing trust knowledge with banks.

At high level this is how Dynamics 365 Fraud Protection works for Purchase Protection. 

On the left-hand side. You can see these are the Dynamics 365 Fraud Protection customers and our merchant’s customers. , the merchant or PSP (payment service provider) is in control of their UX (User experience) and systems and can decide to implement Dynamics Fraud Protection device fingerprinting **(number 1 and 2)** in their UI (user interfaces) for both browser based and mobile based applications.  A Java-based web SDK (software development kits) and iOS, Android and React Native SDKs for mobile applications are available. 

When a purchase takes place, an API from Dynamics 365 Fraud Protection side is called with specific information, to then pass along to Dynamics 365 Fraud Protection **(number 2)**. Then that data is compared to the data already within our fraud protection network. Dynamics Fraud Protection machine learning will then try to find linkages and see past behavior coming from data attributes such as IP address, geo location, and many other device fingerprinting attributes, as well as other data attributes related to the activity of the entities within the transaction such as velocities or the timing of transactions.  

Then on top of the machine learning analysis, there are some simple predefined rules that  Dynamics 365 Fraud Protection customers can set up or you can set up your own custom rules, which would give a response back to you saying the purchase should either be approved or rejected, with this kind of fraud risk or bot score, and along with the reason for the decision that was made.    

As you can see in **(number 3)**, Risk Assessment. These device attributes go into the Dynamics 365 Fraud Protection machine learning model with which we then return a score to you for bot and risk scores. The scoring is important because it tells you the probability the transaction is fraudulent, or the likelihood of fraud that you may want to review or reject. The lower the score, the less likelihood of fraud and the higher the score, the greater probability of fraud.  

On the right-hand side in **(number 4)** you can see we are also partnering with a set of issuing banks via a feature we call Transaction Acceptance Booster. This feature helps you achieve higher bank acceptance rates by sharing some of the intelligence Dynamics 365 Fraud Protection has about the transaction, known as Trust Knowledge, with the issuing banks.  This is data that the issuing bank would not see without Dynamics 365 Fraud Protection and allows them to have higher confidence in their assessment of the transaction and therefore accept many transactions that they would otherwise have rejected.  

 
**API Abstract Diagram -** Below is an abstract diagram of how Microsoft Dynamics 365 Fraud Protection Purchase Protection connects with our customer’s front and back end and provides API descriptions. For Dynamics Fraud Protection to do its best job of adapting to fraud patterns, it is vital for DFP to understand the lifecycle of the transaction and so DFP offers a set of APIs that let the merchant describe that to us.  
 

 

 
