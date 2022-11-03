---
author: josaw1
description: This article provides information about the components of case management in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 11/03/2022
ms.topic: reference
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - developer
title: Case management overview
ms.custom:
---

# Case management overview

This article provides information about the components of case management in Microsoft Dynamics 365 Fraud Protection.

Fraud Protection offers a suite of capabilities that you can use to enhance AI-based assessments with the subject matter expertise of human reviewers.

Case management lets you organize and access transactions, and specify the level of ambiguity that will require review by human subject matter experts. It also includes functionality that lets you provide a feedback loop for the AI-based assessments.

Case management has several components that work together to provide an end-to-end transaction management experience. The rest of this article describes the most important of these components:

- [Cases](#cases)
- [Supplementary events](#supplementary-events)
- [Queues](#queues)
- [Routing rules](#routing-rules)
- [Transaction review](#transaction-review)

## Cases

A case represents a purchase transaction that the merchant has decided will require review. The decision of the merchant is based on the outcome of the assessment. For more information about the assessment, see [Manage rules](rules.md#conditions).

## Supplementary events

Supplementary events follow a purchase event and provide additional information about a specific purchase transaction. Supplementary events include calls to the **purchaseStatus** or **bankEvents** application programming interface (API), where the most recent status of the purchase transaction is updated.
 
## Queues

You use queues to organize a set of cases, based on specific criteria. The cases are then reviewed by the appropriate manual review agents.

## Routing rules

You use routing rules to define the criteria for organizing cases into queues.

## Transaction review

From the **Transaction review** page, manual review agents review the contextual information about a case. Based on this review, the agents determine the likelihood of fraud for the transaction and select an appropriate decision for the case. 
