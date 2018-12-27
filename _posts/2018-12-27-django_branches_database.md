---
title: Code across multiple branches while keeping a single database 
dropcaps: true
published: true
description: A pragmatic setup when you code across multiple git branches with each their own migration files.  
tags:
- django
- git
---
Coding an ORM based software having multiple development git branches ain't trivial.  
By definition, your database scheme evolves with your model code and you quickly end up with errors when you apply
a database migration in one branch then checkout another one : database and code get unsynchronized
and ... you're *doomed* :scream:  
You can go back to normal by applying reverse migrations but you don't want that as it's time consuming
and introduces unnecessary complications in your daily workflow.
 
What else then?  
For practical purpose we want to use the same database no matter the branch, so that we always have
same testing data available. Having one database per branch defeats that point and does not scale
well with number of branches (creating a branch in git is *cheap* as opposed to restoring a database).

The trick consists to use [`stellar`](https://github.com/fastmonkeys/stellar), this tool keeps
snapshots of the database in the RDBMS, and works as follow :  
- first, you take a snapshot of your database in its original state, typically just after having 
  restored your database dump :
  
      stellar snapshot <mydb>
        
- when you checkout a new branch, you restore the snapshot and apply migrations created in the 
  meantime :
  
      stellar restore <mydb>
      ./manage.py migrate
  

