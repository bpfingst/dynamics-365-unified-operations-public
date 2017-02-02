---
# required metadata

title: Automatic settlement and prioritization | Microsoft Docs
description: This article describes how transactions are settled if you select Automatic settlement on the Accounts receivable parameters page. It also explains how automatic settlement can be used in combination with the payment priority.
author: twheeloc
manager: AnnBe
ms.date: 2015-12-02 23:32:21
ms.topic: article
ms.prod: 
ms.service: Dynamics365Operations
ms.technology: 

# optional metadata

keywords: CustOpenTrans, CustParameters, LedgerJournalTransCustPaym
# ROBOTS: 
audience: Application User
# ms.devlang: 
ms.reviewer: twheeloc
ms.suite: Released- Dynamics AX 7.0.0
# ms.tgt_pltfrm: 
ms.custom: 14531
ms.assetid: 1af2529e-7a08-4e9c-9673-4fab30169ca5
ms.region: Global
# ms.industry: 
ms.author: kweekley

---

# Automatic settlement and prioritization

This article describes how transactions are settled if you select Automatic settlement on the Accounts receivable parameters page. It also explains how automatic settlement can be used in combination with the payment priority.

You have two options when you settle payments with invoices and other transactions. You can manually select the transactions to settle, or Microsoft Dynamics 365 for Operations can select the transactions automatically by using the automatic settlement functionality. You can also customize how automatic settlements are processed by using the **Prioritize settlement** option. All these options are part of the [settlement parameters](http://ax.help.dynamics.com/en/?p=246884) that are defined on the **Accounts receivable parameters** page. The way that transactions are automatically settled can differ, depending on the method that you use for automatic settlement. The following methods are available:

-   User-defined settlement priority
-   Default automatic settlement

The following sections describe how transactions are settled for each method.

## Example transactions
The examples of settlements later in this article are based on the following transactions. All transactions are for customer 2050.

| Transaction   | Date        | Amount | Cash discount terms | Cash discount date | Comments                                                                                                                                                                                      |
|---------------|-------------|--------|---------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Invoice 1     | August 15   | 100.00 | 2%14, Net 30        | August 29          |                                                                                                                                                                                               |
| Invoice 2     | September 1 | 250.00 | 2%14, Net 30        | September 15       |                                                                                                                                                                                               |
| Invoice 3     | October 15  | 500.00 | 2% 14/Net 30        | October 29         |                                                                                                                                                                                               |
| Interest note | October 15  | 7.00   |                     |                    | This interest note is for invoice 1 and invoice 2. The amount is calculated as 2-percent interest on amounts that are 30 or more days past due. For example, 0.02 × (100.00 + 250.00) = 7.00. |

## Userdefined settlement priority
If you set **Use priority for automatic settlements** to **Yes** on the **Accounts receivable parameters** page, the settlement priority that you define on the **Settlement priority** page is used when transactions are selected for automatic settlement. For this example, the following settlement priority is defined:

1.  Transaction type
    -   Payment fees
    -   Collection letters
    -   Interest notes
    -   Invoices

2.  Transaction date, Ascending
3.  Voucher

If you post a payment for 700.00 on October 25, the payment is settled to the transactions in the following order.

| Voucher       | Date       | Invoice | Amount in transaction currency | Amount to settle | Balance | Currency |
|---------------|------------|---------|--------------------------------|------------------|---------|----------|
| Interest note | 10/15/2015 |         | 7.00                           | 7.00             | 0.00    | USD      |
| Invoice 1     | 8/15/2015  | 10001   | 100.00                         | 100.00           | 0.00    | USD      |
| Invoice 2     | 9/1/2015   | 10002   | 250.00                         | 250.00           | 0.00    | USD      |
| Invoice 3     | 10/15/2015 |         | 500.00                         | 343.00           | 157.00  | USD      |

## Default automatic settlement
If there is no user-defined settlement priority, transactions are automatically selected for settlement based on the due date. The transactions that are settled must have the same currency as the transaction that they are settled with. If you post a payment for 700.00 on October 25, the following transactions are selected for settlement.

| Voucher       | Date       | Invoice | Amount in transaction currency | Amount to settle | Balance | Currency |
|---------------|------------|---------|--------------------------------|------------------|---------|----------|
| Invoice 1     | 8/15/2015  | 10001   | 100.00                         | 100.00           | 0.00    | USD      |
| Invoice 2     | 9/1/2015   | 10002   | 250.00                         | 250.00           | 0.00    | USD      |
| Invoice 3     | 10/15/2015 |         | 500.00                         | 350.00           | 150.00  | USD      |
| Interest note | 10/15/2015 |         | 7.00                           | 0.00             | 0.00    | USD      |


