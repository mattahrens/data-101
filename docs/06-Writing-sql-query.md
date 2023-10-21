---
layout: page
title: Lesson 6 - Writing SQL to query data
nav_order: 7
description: Lesson 6 - Writing SQL to query data
---
# Lesson 6 - Writing SQL to query data

## Objective

- Learn what Structured Query Language (SQL) is and what its key parts are
- Understand how to write a SQL query in Python

## Concept

The past couple lessons we learned how to build data queries using functions in Python.  Now we're going to shift to writing queries in a standardized language for queries called SQL.  SQL is a language that is used in many different languages and frameworks where datasets reside.  Learning SQL is important because you can use it in many different ways.

Building a query in SQL involves using specific keywords to represent how you are interacting with the data.  Here is an overview of the main keywords that are present in a query along with a specific example query of art datasets:

![image](images/06-sql_query_overview.jpg)
*Source: learnsql.com*

Let's walk through these keywords one by one.  And as we do so, you can see how the keywords map to functions that we've already seen when working with data in Python.

### SELECT

We'll start with the **SELECT** keyword.  The SELECT keyword allows us to pick which fields in the dataset that we want to see in the output.  Along with picking what fields we want, we also can apply specific operations on the dataset.  In the example above, you can see that the keyword **MIN** is used with the field year so that the output shows the minimum year.  In our previous Python queries where we used functions, we could have picked what columns we wanted by specifying their names directly as part of the code.  In a SQL query, you can do that through the SELECT keyword.
 
### FROM

The **FROM** keyword specifics which dataset that you'll be using.  In our Python code, we created datasets as dataframes and then coded functions against those datasets (e.g. `books_df`, `users_df`).  In a SQL query, you can choose which dataset you want to query by naming it after the FROM keyword.  

### JOIN + ON

In data queries, the way to bring together records from different datasets is through a **join**.  A join involves combining the data through some field that both datasets have in common or that can be related to each other.  In the example above, the **JOIN** keyword is used to join the `artworks` and `artists` datasets together with the common field of artist identifier.  The **ON** keyword specifics the common field to use to join the datasets together.  We'll discuss joins more in a later lesson as they are a more complicated part of data queries.

### WHERE

The **WHERE** keyword allows us to add a filter in a query.  This is similar to how we can specify only certain records to show when we were writing Python functions to query data.  In the previous lesson, we filtered to see only books published in 2002 through this clause: `books_df['Year-Of-Publication'] == '2002'`.  When writing SQL, you can do that same filter using the WHERE keyword.  In the art example above, the filter is used to remove any art titles that are `The Mona Lisa`.

### GROUP BY

### HAVING

### ORDER BY


## Practice: Building SQL queries in Python

## Summary
In this lesson, we learned about SQL and what the main keywords in SQL mean.  We then were able to write our own SQL queries in Python to ask questions of our data.  We saw how writing a SQL query is similar to using functions.
