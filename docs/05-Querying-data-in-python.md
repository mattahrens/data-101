---
layout: page
title: Lesson 5 - Querying data in Python
nav_order: 6
description: Lesson 5 - Querying data in Python
---
# Lesson 5 - Querying data in Python

## Objective

- Learn how to use functions with dataframes to query data
- Understand how to map a question about a dataset to Python code

## Concept

We'll pick up where we left off with our book ratings dataset to understand more about how to query a dataset.  Remember that we loaded in a dataset and created 3 dataframes: `ratings_df`, `books_df`, and `users_df`.  We can see the names of the fields inside a dataset by calling the `columns` attribute for the dataframe:

![image](images/05-books_df_columns.png)

Now that we know the fields that are in the books dataframe, we can query the dataset.  To query data using Python, we will call functions for our dataframe objects.  Last lesson, you did an example of a function with the `info()` function.  When building a query using functions, you can build functions together in a single line of code to make the query simpler.  

Let's start by querying the books dataset to figure out which year of publication had the most books in the dataset.  Here is a single line of code for that query:

![image](images/05-books_group_year.png)

```
books_df.groupby(['Year-Of-Publication']).count().sort_values(by=['ISBN'], ascending=False).head(25)
```

This single line of code looks complicated, so let's break it apart to see the various functions that are being called.

## Practice: 

## Summary

