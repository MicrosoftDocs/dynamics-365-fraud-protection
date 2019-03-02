# Sign up for Dynamics 365 Fraud Protection

To experience the simplicity and power of Dynamics 365 Fraud Protection, complete the Contact form from your promotional source. The form has minimal fields to complete. As Microsoft is committed to preserving your business, customer, and data privacy, we recommend you review the legal, privacy, and General Data Protection Regulation (GDPR) information for reassurance.

![Screenshot of signup promotion form](media/signup-promotion-form.png)

Upon qualifying for Dynamics 365 Fraud Protection, you will recieve an email notification with a promocode embedded in a sign-up link  detailing your next steps.

> [!NOTE]
> Dynamics 365 Fraud Protection Beta is a free service.




Once above complete, to access the API documentation, follow these steps: 
1. Navigate to Partner API Documentation. 
2. Scroll down and select Sign in with the same work account you used to sign into the Azure portal to see more services. 
3. Since you have already been provisioned a tenant, use those account credentials to sign in and view the Dynamics 365 Fraud Protection API documentation.  isn’t this the same work account that they should use from #1-2?   I would restate #3 as: “Navigate to the Dynamics 365 Fraud Protection API documentation and sign in using the the same work account you used to sign into the Azure portal”
4. After signing in, select Dynamics 365 Fraud Protection API.



### To sign up for Dynamics 365 Fraud Protection


# Dynamics 365 Fraud Protection Azure resources and merchant logins

See the following links to access Dynamics 365 Fraud Protection Azure resources and merchant logins

**Admin user logins**

Username: user@merchant.onmicrosoft.com (this must be updated for a new merchant)

Passwords can be set by a Global administrator in the merchant.onmicrosoft.com tenant.

**Azure tenant poral URL**

[Microsoft Azure](https://portal.azure.com/merchant.onmicrosoft.com)

- This site manages user and Azure Active Directory (AAD) application access to Dynamics 365 Fraud Protection and uploading data via the Azure Data Lake.
- We suggest you change your passwords and add two-factor authentication.

**Dynamics 365 Fraud Protection portal URL**

[Sandbox](https://dfp.microsoft-int.com/merchant.onmicrosoft.com)
[Prod](https://dfp.microsoft.com/merchant.onmicrosoft.com)

- Use these URLS to access Dynamics 365 Fraud Protection, including data, metrics, rules, and so on.
- Use the same Admin user credentials to log into the Dynamics 365 Fraud Protection portal URL.

**AAD Application so you can run Dynamics 365 Fraud Protection API**

Sandbox
- Name: DFP-Sandbox Client App
- Application Id: *appid goes here*

Prod
- Name: DFP-Prod Client App
- Application Id: *appid goes here*

**Your CustomerID to use for device fingerprinting**
- **Device fingerprinting customer (environment id) goes here**

**Azure Data Lake for you to upload the historical data**

Sandbox: DFP-Data-Upload-Sandbox

Prod: DFP-Data-Upload-Production


