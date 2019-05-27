---
tip: 3
title: the model of handling ErrCodeStoreOutOfGas situation
author: SHU XUN <shuxun@truechain.pro>
created: 2019-05-27
status: Draft
type: Standards Track
category: Core
---

# Abstract

This draft TIP describes the model of handling the situation that contract creation code storage out of gas

# Motivation

when an error of ErrCodeStoreOutOfGas was returned by the EVM,We should punish such behavior.
revert to the snapshot and consume any gas remaining

# Specification

In order to achieve the specs, The current processing mode needs to be modified.
- the current processing mode is when EVM return ErrCodeStoreOutOfGas,we just return the error without any special handling,
But when ErrCodeStoreOutOfGas is a malicious behavior, the client expends some computing resources on it, 
and the gas consume too little about the action.
- so in order to avoid this ,when contract creation code storage out of gas, we should revert to the snapshot and consume any gas remaining.

# Implementation

current processing mode:
```
err != nil && err != ErrCodeStoreOutOfGas{
    evm.StateDB.RevertToSnapshot(snapshot)
    if err != errExecutionReverted {
        contract.UseGas(contract.Gas)
    }
}
```
when err is ErrCodeStoreOutOfGas only return err

modified processing mode:
```
err != nil && (evm.ChainConfig().IsTIP3(evm.BlockNumber) || err != ErrCodeStoreOutOfGas){
    evm.StateDB.RevertToSnapshot(snapshot)
    if err != errExecutionReverted {
        contract.UseGas(contract.Gas)
    }
}
```

1. https://github.com/truechain/truechain-engineering-code/blob/master/core/vm/evm.go


