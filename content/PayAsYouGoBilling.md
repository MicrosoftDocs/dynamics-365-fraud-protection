---
description: This topic explains how to enable Pay as you go billing for Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 07/08/2021


ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Pay as you go billing
---

# Pay as you go billing

With Pay as you go billing, you can use Fraud Protection as much or as little as you need, and you pay only for what you use. Service interruptions will be minimized and you won't overpay as a result of forecasted transaction volumes.

This topic describes how to get started with Pay as you go billing. Setup requires Global AAD Tenant admin permissions and contributor permissions to an active Azure Subscription. 

> [!NOTE]
> If you are an existing customer of Dynamics 365 Fraud Protection and wish to take advantage of Pay as you go billing, please contact your Microsoft Partner who can discuss updated pricing and help you make the transition

## Pay as you go Pricing
Every month, your total bill amount would be determined based on how much of each Fraud Protection capability you used. Prices are based on per transaction and become more favorable as the monthly usage grows. Here’s the detailed pricing for each capability of Fraud Protection :

**Fixed Monthly fee:** $12 per month per AAD tenant.

### Pricing tiers for Account Protection capability:
| < 100,000 transactions per month | $0.01  per transaction |
|-----------------------------|--------------------------------------------------|
| 100,000 - 1,300,000 transactions/month | $0.0075 per transaction |
| >= 1,300,000 transactions/month | $0.005 per transaction |

### Pricing tiers for Loss Prevention capability:
| < 20,000 transactions per month | $0.05 per transaction |
|-----------------------------|--------------------------------------------------|
| 20,000 - 160,000 transactions/month | $0.0375 per transaction |
| >= 160,000 transactions/month | $0.025 per transaction |

### Pricing tiers for Purchase Protection capability:
| < 10,000 transactions per month | $0.1  per transaction |
|-----------------------------|--------------------------------------------------|
| 10,000 - 300,000 transactions/month | $0.075 per transaction |
| >= 300,000 transactions/month | $0.05 per transaction |

## Pre-requisites for enabling Pay as you billing
You would need the following to get started with Pay as you go billing for Fraud Protection. We will explain how you can set these up later in the document
* Monthly subscription for the Fraud Protection Pay as you go SKU
* Active Azure Subscription  

> [!NOTE]
> * Global Administrator permission are needed to use Fraud Protection in an existing AAD tenant 
>* Contributor permission to an Azure Subscription is needed to use the subscription for Pay as you go billing

## How to enable Pay as you billing:
Enabling Pay as you go billing requires the following steps. Detailed description of these steps is provided later in the document. 
1.	Set up a monthly subscription for Fraud Protection.
2.	Set up your Fraud Protection environment (could be skipped if you already have a Fraud Protection environment set up).
3.	Configure an Azure Subscription for Pay as you go billing.
4.	Enable Pay as you go billing.

### 1. Set up a monthly subscription for Fraud Protection
* Go to [Fraud Protection website](https://dynamics.microsoft.com/ai/fraud-protection/) and select the Buy Now option 
* Sign-in as the Global Administrator of the same AAD Tenant in which you wish to use Fraud Protection. If you don’t have an AAD tenant you can sign up for a new one by following on-screen instructions
* Complete the purchase flow, and you’ll receive a confirmation that your monthly subscription for Fraud Protection Pay as you go is successfully set up.
* You will be redirected to the Fraud Protection portal, where you would be able to take the next step 

### 2. Set up your Fraud Protection environment
* Once you land on the [Fraud Protection portal](https://dfp.microsoft.com/), sign in as the Global Administrator of the AAD Tenant that you used in Step 1
* If you had already completed the Fraud Protection environment setup (for your Free Trial) before, the Fraud Protection portal would load after you sign-in and you can proceed to the next step. If you have not been through the setup before, you can follow the instructions in [this doc](https://docs.microsoft.com/dynamics365/fraud-protection/promocode-set-up-dfp-purchased-version#complete-the-setup-process) and then move on to the next step

### 3. Configuring an Azure Subscription for Fraud Protection billing
* In a new browser tab, go to the [Azure portal](https://portal.azure.com/) and sign in with the same credentials you used in Step 2. 
* Search for Subscriptions in the Search box and then select Subscriptions option to go the page that lists all the Azure Subscriptions that you have access to. If you do not see any subscriptions, you can create a new one by selecting + Add option. Read more about various subscription options [here](https://docs.microsoft.com/azure/cost-management-billing/manage/create-subscription).
* ![image](https://user-images.githubusercontent.com/51425263/124168346-dd057900-da59-11eb-8636-aa91855a949c.png)
* ![image](https://user-images.githubusercontent.com/51425263/124168399-ee4e8580-da59-11eb-8b44-bdf0de9d4e65.png)
* Now select the Subscription you wish to use for Fraud Protection billing and then select Resource Group option on the next page (it is present in the Settings section of the left-hand menu). Then select the + Create button to start the flow for creating a new Resource Group
* ![image](https://user-images.githubusercontent.com/51425263/124168497-163de900-da5a-11eb-856c-f5ad0f050abc.png)
* In the Create a Resource Group window, you can choose any name and Azure Region that you prefer. Then select the Review + create button in the bottom left corner. Azure validates the information, after which you can select the Create button to create the Resource Group. 
* ![image](https://user-images.githubusercontent.com/51425263/124168712-58ffc100-da5a-11eb-9d11-79af76380724.png)
* You’ll receive a notification in the Azure portal confirming that the Resource Group was successfully created. Remember the name of the Azure Subscription and Resource Group as you'll need them to set up Pay as you go billing in the next step 

### 4.	Enable Pay as you go billing 
* Return to the tab where [Fraud Protection portal](https://dfp.microsoft.com/) is open and select the Enable option on the Dashboard page
* ![image](https://user-images.githubusercontent.com/51425263/124169253-e3e0bb80-da5a-11eb-870d-a9d5de9a6d40.png)
* In the subsequent panel, select the Azure Subscription and Resource Group you configured in Step 3 and Select Enable
* ![image](https://user-images.githubusercontent.com/51425263/124171344-4cc93300-da5d-11eb-96c7-6b5f4c2c75ec.png)
* You’ll receive a confirmation that Pay as you go billing setup was successful. Now you can use Fraud Protection and based on your usage, you will receive your bill each month. 
* ![image](https://user-images.githubusercontent.com/51425263/124171424-6b2f2e80-da5d-11eb-8c85-c2239fa5fb31.png)
* If you wish to learn more about what type of Fraud Protection usage is billable, you can refer [this document](https://docs.microsoft.com/dynamics365/fraud-protection/metering).
