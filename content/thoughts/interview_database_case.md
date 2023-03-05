---
title: "Database column type overflow case"
date: 2023-03-05T13:14:32+06:00
draft: true
tags: ['interview', 'engineering', 'case']
---

## Interview questions and cases #1
This is one of many examples of technical tasks that can be used in interviews with developers and technical managers.

This assignment covers working with databases, large volumes of data, naunces of different data types and the subtleties of working with table structure.

<!--more-->

### Given
A table in a relational database with a small number of columns but a large number of rows (more than 1 billion).
This table is critical to business operations and is very actively used in the application.
One of the columns is a sequential key of type int32 and in the near future (week, month), the number of rows will lead to a capacity overflow of type int32.

### The task
What will be the strategy to solve this problem and what measures should be taken to minimise system downtime?