---
tip: 1
title: transaction gas fee can be paid by third accout
author: Yang LIU <hyangliu@gmail.com>
created: 2019-01-11
status: Draft
type: Standards Track
category: Core
---

# Abstract

This draft TIP describes the mechanism of gas paying agent, when sending a transaction, others can pay the transaction fee instead of sender.

# Motivation

The customers can send transactions without enough TRUE, this is friendly to DApp development.

# Specification

In order for the mechanism to work, the transaction will add some messages.
The original transaction take the following form:
```
- AccountNonce: Number of transactions sent by the sender.
- GasPrice: Number of Wei to be paid per unit of gas for this transaction.
- GasLimit: Maximum amount of gas should be used for this transaction.
- Recipient: Address of the beneficiary for this transaction.
- Value: Amount of token to be transacted.
- Data: Virtual machine code for smart contract deployment or miscellaneous use.
- V,R,S: Cryptographic values corresponding to the signature of the transaction, and used to determine the sender of the transaction.
```
Here is the new form:
```
- AccountNonce: Number of transactions sent by the sender.
- GasPrice: Number of Wei to be paid per unit of gas for this transaction.
- GasLimit: Maximum amount of gas should be used for this transaction.
- Recipient: Address of the beneficiary for this transaction.
- Value: Amount of token to be transacted.
- Data: Virtual machine code for smart contract deployment or miscellaneous use.
- Payer: The payer sender wants the transaction to be paid by.
- V,R,S: Cryptographic values corresponding to the signature of the transaction, and used to determine the sender of the transaction.
- PV,PR,PS: Cryptographic values corresponding to the signature of the payment, used to determine the payer of the transaction.
```

## Create

When a user creates a new transaction, he can set fields `Payer`,`PV`,`PR`,`PS` nil, or set a payer address if he wants others pay the gas.
The sender signs the transaction with these fields:
- AccountNonce
- GasPrice
- GasLimit 
- Recipient 
- Value 
- Code 
- Payer 
  
If the transaction to be paid by himself, send the transaction to a node directly, otherwise, send the transaction to the payer by a offchain message.

The payer signs the transaction with these fields to confirm the payment:
- AccountNonce
- GasPrice
- GasLimit 
- Recipient 
- Value 
- Code 
- Sender  
Then sends the transaction to a node. 


## Validate
When a node receives a transaction, it will checks whether a transaction is valid accrording to the consensus rules:
- validate whether the transaction is signed properly
- if payer is setted, check the payment signature 
- ensure the nonce ordering
- check the sender and payer's funds to cover the costs

## Excute

VM excutes the transaction and deducts the transaction fee from payer accout.

# Implementation

1. https://github.com/truechain/truechain-engineering-code/blob/master/core/types/transaction.go
2. https://github.com/truechain/truechain-engineering-code/blob/master/core/types/transaction_signing.go

