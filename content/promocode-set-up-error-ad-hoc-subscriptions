---
author: josaw1
description: This topic provides a workaround for global admins failing to redeem a promo/promotion code because their company policy blocks it, specially the 'AllowAdHocSubscriptions' is set to False in their tenant.
ms.author: josaw
ms.date: 06/07/2022
ms.topic: reference
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Promotion code redemption - Enable ad-hoc subscriptions
ms.custom:
---

# Promotion code redemption - Enable ad-hoc subscriptions

You may encounter an error while redeeming a Dynamics 365 Fraud Protection promotion code stating "Trial signup blocked by company policy".  The company setting known as *[AllowAdHocSubscriptions](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings)* is disabled and needs to be temporarily enabled.  You can then redeem the promotion code and disable the company setting afterwards.

## Temporarily enable the ad-hoc subscriptions
> [!NOTE]
> You'll need to be an Azure global admin in your tenant to run this code.

```powershell
//Start PowerShell and run these first 3 commands.  The 2nd one will prompt you for your credentials:
Install-Module MSOnline
Connect-MsolService
Get-MsolCompanyInformation | fl AllowAdHocSubscriptions

//if it's False and you're ready to temporarily allow these signups, run this:
Set-MsolCompanySettings -AllowAdHocSubscriptions $true

//at this point, go back to the Fraud Protection site and try to redeem your promo code again.

//assuming you want to put the protection back on, run this after you redeem your promo code for Fraud Protection
Set-MsolCompanySettings -AllowAdHocSubscriptions $false

//the setting should be False again
Get-MsolCompanyInformation | fl AllowAdHocSubscriptions
```

## References

- The same process exists for Dynamics 365 Business Central: [Enable and Disable Dynamics 365 Business Central Self-service Signups](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/devenv-business-central-manage-selfservice-signups)

## Support

To log a support ticket, go to <https://dfp.microsoft.com> and click the question mark in the header bar. Global administrator permissions are required.
