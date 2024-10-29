## Use custom lists

[Rules](../rules.md) define custom logic that automates business decisions. To help define this logic, you can take advantage of any list in a rule. For example, you can create one list of email addresses that you consider risky and another list of email addresses that you consider safe. You can then configure a rule so that all sign-in attempts that use an email address in the **Risky Emails** list are rejected, whereas sign-in attempts that use an email address in the **Safe Emails** list are approved.

## Single-column and multicolumn lists

The following example shows two separate lists, **Risky Emails** and **Safe Emails**. In both lists, a single column of values represents a key (in this case, the email address).

| Risky Emails |
|--------------|
| `Kayla@contoso.com` |
| `Jamie@bellowscollege.com` |
| `Marie@atatum.com` |

| Safe Emails |
|-------------|
| `Camille@fabrikam.com` |
| `Miguel@proseware.com` |
| `Tyler@contoso.com` |

However, you can use additional columns to hold values that are relevant to the key. For example, instead of using two separate lists, you can combine the same information into one multicolumn list, as shown here.

| Email address | Status |
|---------------|--------|
| `Kayla@contoso.com` | Risky |
| `Jamie@bellowscollege.com` | Risky |
| `Marie@atatum.com` | Risky |
| `Camille@fabrikam.com` | Safe |
| `Miguel@proseware.com` | Safe |
| `Tyler@contoso.com` | Safe |

You can then configure your rule so that all sign-in attempts that use an email address that appears in this list and has a status of *Risky* are rejected, whereas attempts that use an email address that has a status of *Safe* are approved.

In addition to using multicolumn lists to combine safe and block lists, you can use them to specify the unique levels of risk that are associated with a set of products, email addresses, or countries/regions. For example, if specific product types present different levels of risk to your business, you can make decisions for those products differently. Specifically, you can evaluate each product against its own score threshold. To use this approach, you must first create a list that represents this information, as shown in the following example.

| Product type | Score threshold |
|--------------|-----------------|
| Digital | 500 |
| Consumable | 600 |
| Physical | 750 |

You can then configure a rule that enforces the rejection of transactions where the [risk score](../ap-scorecard.md#risk-model-score) exceeds the specified threshold for the product type. For information about how to create effective rules to customize your business logic, see [Rules](../rules.md).

> [!NOTE]
>
> Lists can also be referenced within Functions. For more information, see [Functions](../functions.md).