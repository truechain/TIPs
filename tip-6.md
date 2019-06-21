---
tip: 6
title: handling of fee in transaction
author: SHU XUN <shuxun@truechain.pro>
created: 2019-06-21
status: Draft
type: Standards Track
category: Core
---

# Abstract

This draft TIP describes the usage of "fee" field in transaction

# Motivation

Facilitating the flow of asset and values in Truehcian Networks

# Specification

when the "fee" filed in transaction is not null, subtract amount of fee from sender account and add this amount to payment account.

Here is the new form transaction:

```
- AccountNonce: Number of transactions sent by the sender.
- GasPrice: Number of Wei to be paid per unit of gas for this transaction.
- GasLimit: Maximum amount of gas should be used for this transaction.
- Recipient: Address of the beneficiary for this transaction.
- Value: Amount of token to be transacted.
- Fee: Assert service charged.
- Data: Virtual machine code for smart contract deployment or miscellaneous use.
- Payer: The payer sender wants the transaction to be paid by.
- V,R,S: Cryptographic values corresponding to the signature of the transaction, and used to determine the sender of the transaction.
- PV,PR,PS: Cryptographic values corresponding to the signature of the payment, used to determine the payer of the transaction.
```
When EVM executes a transaction and Detected that Fee and Payer address is not empty,
will perform evm.StateDB.SubBalance(Sender, Fee) and evm.StateDB.AddBalance(Payer, Fee).

# Implementation



