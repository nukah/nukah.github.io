---
title: "[Interview] Database design case"
date: 2023-03-05T13:14:32+06:00
tags: ['interview', 'engineering', 'case', 'database']
---

# Introduction
This is one of many examples of technical tasks that can be used in interviews with developers and technical managers.
This assignment covers working with databases, large volumes of data, naunces of different data types and the subtleties of working with table structure.

<!--more-->

# Given
We have a table which
- Critical for business operations
- Actively used in application
- Has 3 columns
| Name | Type | Attributes|
| --- | --- | --- |
| id | int | sequential |
| name | text | |
| data | text |
- Current amount of rows is 2 billion
- Each day we add about 10m rows to the table

# Questions
- What potential outcome you see if done nothing?
- What will be the strategy to solve this issue?
- What measures should be taken to minimise system's downtime?

# Links and references
- [Integer at the end of the universe](https://www.crunchydata.com/blog/the-integer-at-the-end-of-the-universe-integer-overflow-in-postgres)
- [SQL Data types](https://www.digitalocean.com/community/tutorials/sql-data-types)