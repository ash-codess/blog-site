---
author: Ash
pubDatetime: 2025-09-01T1:20:00Z
title: Deltalake
postSlug: Deltalake -
featured: true
draft: false
tags:
  - data-engineering
ogImage: ""
description: Deltalake 101
---

## Intro

### Problems with Data Lake:

#### 1. Lack of ACID transaction support

- Atomic - Nothing or all
- Consistency: Rules must be enforced. A transaction must bring database from one valid state to another.
- Isolation: No interferance. Each transaction will be isolated from another simulations transaction.
- Durability: ONce a transaction is recorded in system it is going to be registered despite of system crash/failures etc.

#### 2. Lack of Update/ Delete / Merge

#### 3. Lack of data reliability/data quality (caused due to lack of schema enforcement)

Delta solves all of the above problems along with other features.

Delta lake soft intro
