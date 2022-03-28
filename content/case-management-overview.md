---
author: josaw1
description: This topic provides information about the componente of Case management in Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 03/28/2022
ms.topic: reference
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - developer
title: Case management overview
ms.custom:
---

# Case management overview

Dynamics 365 Fraud Protection offers a suite of capabilities that you can use to enhance AI-based assessments with the subject matter expertise of human reviewers.
With case management, you can organize and access transactions, and determine the level of ambiguity required for a review by human subject matter experts. You can also use the functionality of case management to provide a feedback loop for the AI-based assessments. Case management has several components that work together to provide an end-to-end transaction management experience. The most important components of case management include: 

  - [Case](#case)
  - [Supplementary events](#events)
  - [Queues](#queues)
  - [Routing rules](#rules)
  - [Transaction review](#review)

## <a name="case"></a> Case

A case represents a purchase transaction that the merchant has decided will need a review. The decision of the merchant is based on the outcome of the assessment. For more information about the assessment, see [Manage rules](rules.md#conditions). 

## <a name="events"></a> Supplementary events

Supplementary events follow a pruchase event and provide additional iformation about a specific purchase transaction. Supplementary events include calls to the **purchaseStatus** API or **bankEvents** API where the most recent status of the purchase transaction is updated. 
 
## <a name="queues"></a> Queues

Use queues organize a set of cases based on certain criteria. The cases are then reviewed by the appropriate manual review agents.

## <a name="rules"></a> Routing rules

Use routing rules to define the criteria for organizing cases into queues.

## <a name="review"></a> Transaction review

Manual review agents use transaction reviews to review the contextual information about a particular case. Based on this review, the agents determine the likelihood of fraud for the transaction. 
