---
tip: 13
title: make more validators in committee after it not work
author: TianMing <tianming@truechain.pro>
created: 2019-07-19
status: Draft
type: Standards Track
category: Consensus
---

# Abstract

This draft TIP describes the commitee will be join new validators automatically and dynamically when it was not work, that make the committee work again smoothness until next election.

# Motivation

the committee can revent to work again when it break on some errors.

# Implementation

the committee has more than ten rounds on a proposal,it will never have a true-consensus with High probability.
For the stability of the truechain main network :

the validators set:
```
- workValidatorSet: working in Current committee. 
- backValidatorSet: backup validator in Current committee.
- seedValidatorSet: seed validator in every committee.
```
the committee work broken with no one evil validator,just have difference fast-block with a reward in every validator,that make a partition on the committee,than they have nerver make consensus with a proposal block.

so we provide a solution that resize the committee count dynamically on next proposal in new round,
the current committee will be approve this proposal and update the count of the committee,all seed validators will enter the committee.

```
the committee = workValidatorSet + seedValidatorSet
// exclude the validator who was removed
```
setp:

```
- leader make new proposal(add seed member into committee) and send to all members.
- validators will check and vote on this proposal.
- the committee commit this block with the proposal and boradcast it.
- nodes update the validator and restart the committee.
```








