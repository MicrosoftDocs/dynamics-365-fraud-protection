---
author: josaw1
description: This topic provides troubleshooting guidance for when a global administrator fails to redeem a Microsoft Dynamics 365 Fraud Protection promotion code because company policy blocks it.
ms.author: josaw
ms.date: 06/09/2022
ms.topic: reference
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Troubleshoot promotion code redemption error
ms.custom:
---

# Troubleshoot promotion code redemption error

This topic provides troubleshooting guidance for when a global administrator encounters an error when attempting to redeem a Microsoft Dynamics 365 Fraud Protection promotion code. because company policy blocks it.

## Trial account blocked by company policy

When trying and failing to redeem a Fraud Protection promotion code, a global administrator may encounter the following error: 

`Trial signup blocked by company policy`

This error is likely generated because company policy blocks trial accounts from redeeming promo codes, which is done by disabling the [AllowAdHocSubscriptions](/powershell/module/msonline/set-msolcompanysettings) PowerShell setting. To successfully redeem the promo code, the **AllowAdHocSubscriptions** PowerShell setting must be temporarily enabled. You can then redeem the promotion code and disable the company setting afterwards.

> [!NOTE] Keep in mind that you or another administrator may have disabled the **AllowAdHocSubscriptions** PowerShell to prevent certain types of signup at your company. It is recommended that you check with your colleagues before following the steps below.

## Temporarily enable ad-hoc subscriptions

You can temporarily enable ad-hoc subscriptions by running the following PowerShell code.

> [!NOTE]
> You'll need to be an Azure global administrator in your tenant to run this code.

1. Start PowerShell and run the following three commands. The second command will prompt you for your credentials.

    ```PowerShell
    Install-Module MSOnline
    Connect-MsolService
    Get-MsolCompanyInformation | fl AllowAdHocSubscriptions
    ```

1. If the third command outputs **False** and you're ready to temporarily allow these signups, run the following command.

    ```PowerShell
    Set-MsolCompanySettings -AllowAdHocSubscriptions $true
    ```

1. Go back to the Fraud Protection site and try to redeem your promo code again.
1. If you were able to redeem your Fraud Protection promotion code and are ready to turn the protection back on, run the following commands. The output of the second command should again be **False**.

    ```PowerShell
    Set-MsolCompanySettings -AllowAdHocSubscriptions $false
    Get-MsolCompanyInformation | fl AllowAdHocSubscriptions
    ```

## References

The same process exists for Dynamics 365 Business Central: [Enable and Disable Dynamics 365 Business Central Self-service Signups](/dynamics365/business-central/dev-itpro/developer/devenv-business-central-manage-selfservice-signups).

## Support

To log a support ticket, go to [Fraud Protection Sign In](https://dfp.microsoft.com), sign in with global administrator permissions, and then select the question mark in the header bar.

[!INCLUDE[footer-include](includes/footer-banner.md)]
