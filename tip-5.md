---
tip: 5
title: The model of generate FruitsHash
author: WenTao WU <wuwentao@truechain.pro>
created: 2019-06-11
status: Draft
type: Standards Track
category: Core
---

# Abstract

This draft TIP describes the model of generate fruitsHash

# Motivation

make this change is in order to verify fruits more lightweight in lightchain and snapshot.

# Specification

In order to achieve the specs, The current processing mode needs to be modified.
- the current processing mode is when create fruitsHash it uses allfruits include bodies and headers.
- in this change we just need all headers.

# Implementation

current processing mode:
```
if len(fruits) == 0 {
		b.header.FruitsHash = EmptyRootHash
	} else {
		b.header.FruitsHash = DeriveSha(Fruits(fruits))
		b.fruits = make([]*SnailBlock, len(fruits))
		for i := range fruits {
			b.fruits[i] = CopyFruit(fruits[i])
		}
	}
```

modified processing mode:
```
if len(fruits) == 0 {
		b.header.FruitsHash = EmptyRootHash
	} else {
		b.fruits = make([]*SnailBlock, len(fruits))
		var headers []*SnailHeader
		for i := range fruits {
			b.fruits[i] = CopyFruit(fruits[i])
			headers = append(headers, fruits[i].header)
		}
		if config.IsTIP5(header.Number) {
			b.header.FruitsHash = DeriveSha(FruitsHeaders(headers))
		} else {
			b.header.FruitsHash = DeriveSha(Fruits(fruits))
		}
	}
```

1. https://github.com/truechain/truechain-engineering-code/blob/master/core/types/block.go


