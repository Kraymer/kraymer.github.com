---
title: Code across multiple branches while keeping a single database 
dropcaps: false
published: true
description: A pragmatic setup when you code across multiple git branches with each their own migration files.  
draft: true
tags:
- django
- git
---

A pragmatic setup when you code across multiple git branches with each their own migration files.  
For practical purpose we want to use the same database no matter the branch, so that we always have same testing data 
available. Having one database per branch defeats that point and does not scale well with number of branches (creating a branch in 
git is *cheap* as opposed to restoring a database).

The trick consists to use `stellar`.
