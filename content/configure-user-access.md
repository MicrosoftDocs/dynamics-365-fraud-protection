# Configure user access to Dynamics 365 Fraud Protection

After signing up for Dynamics 365 Fraud Protection, the product’s services are configured within your Azure tenant. When this process completes, you can log in to your tenant with your Azure Active Directory (Azure AD) credentials to access the Dynamics 365 Fraud Protection portal.

The Dynamics 365 Fraud Protection portal provides three experiences:

-	[Diagnose](diagnose-experience.md)
- [Evaluate](evaluate-experience.md)
- [Protect](protect-experience.md)

Set up your company’s user access to Dynamics 365 Fraud Protection portal, using the following roles and permissions.

## To configure user access via the Azure portal

You can configure users by assigning them to specific roles provided within Dynamics 365 Fraud Protection.

To grant users access and add user roles to Dynamics 365 Fraud Protection via the Azure portal, see [Assign a user or group to an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/manage-apps/assign-user-or-group-access-portal).

You must be a tenant admin to administer the Azure Active Directory. If you have that role, follow these instructions to configure user access to Dynamics 365 Fraud Protection. If you do not have the required permissions, ask your tenant admin for assistance.

1.	Open the Azure Active Directory in the [Microsoft Azure portal](https://portal.azure.com/#home).
1.	Click Manage, then Enterprise Applications within the Azure Active Directory Overview page.
1.	Search for the Dynamics 365 Fraud Protection BETA enterprise app in your Azure AD by entering the DFP App GUID ‘bf04bdab-e06f-44f3-9821-d3af64fc93a9’.
1.	Within the Enterprise app, select Getting Started, and then select either Assign a user for testing (required) or Deploy single sign-on to users and groups (recommended).
1.	Add any Users or Groups from your Azure AD, and assign them to appropriate Dynamics 365 Fraud Protection BETA roles. For rights associated with these roles, see the following tables.
