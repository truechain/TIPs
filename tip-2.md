---
tip: 1
title: Incentive model to support asset-backed token transactions
author: Eric Zhang <eric@truechain.pro>, Yang Liu <hyangliu@gmail.com>
created: 2019-01-11
status: Draft
type: Standards Track
category: Core
---

# Abstract

This proposal addresses the concern over the status-quo public chain incentive mechanism. It raises a different idea of incentivization mechanism to support asset-backed token transactions in the future.

# Motivation

As on-chain assets are growing rapidly in volume, we propose an incentive mechanism on TrueChain to support large-volume asset-backed token transactions.

Asset-backed tokens are different from utility tokens. An incentive mechanism supporting asset-backed tokens is largely different from ETH's current approach. We have to consider the following issues:
- gas payment in tokens to stablize transaction fees
- linkage between TRUE token and distribution of gas
- larger on-chain asset value incentivizes more hash power

# Specification

In order to achieve the specs, we 
- When user transfers an asset-backed token, a certain percentage of the transfered token are deducted as gas fee.
- The deducted token gas fees are distributed among miners based on their stake of TRUE tokens (token*days) and mining results (blocks and fruits successfully mined in history).
- Miners still get instant TRUE token rewards.

# Implementation

# Notes of Motivations

The Ethereum block incentive model and gas model have been widely adopted for a long time in many public chains' designs. Over the year 2018, utility tokens have been largely failing because most of these tokens are not backed by valuable digital or real assets. In other words, the value of utility tokens are unsure and their economic models are generally not successful. For example, a utility token with only economic model but no revenue would fail miserably. In turn, the fall of utility tokens largely lowered the value of public chains and blockchain infrastructure projects.

Whatever it will be called, tokens can survive have to be valuable. It could be a game asset people love to buy, or a real estate project that generates investment return, or a growing business with future cash flow prospects.

Therefore, public chains have to support such asset backed tokens. The key to this problem is incentive model. The economic model of ETH has to be re-thought and a new incentive model has to be proposed to fulfill the needs of valuable transactions. 