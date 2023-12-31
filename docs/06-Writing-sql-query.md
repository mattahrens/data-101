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

The past couple lessons we learned how to build data queries using functions in Python.  Now we're going to shift to writing queries in a standardized language for queries called SQL.  SQL is a language that is used in many different databases and frameworks where datasets reside.  Learning SQL is important because you can use it in many different ways.

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

The **GROUP BY** keyword should be familiar as we have used the `groupby()` function already and this does the exact same thing.  It allows us to group records by a specific field.  In the example above, the query is grouping the art data by name so that when the fields are selected, it calculates the minimum year of each name of art through the `MIN(year)` selection.  You can group by multiple fields in a query if needed.

### HAVING

The **HAVING** keyword is a special type of filter that is done after you have completed doing the earlier parts of the query.  In the art example, the HAVING filter is done after you have already selected the name and minimum year for the art; it filters to keep records that have a minimum year less than 1700.  

### ORDER BY

The last keyword that we'll look at is the **ORDER BY** keyword.  This is similar to the `sort_values()` function we used in the previous lesson.  It allows the output records to be sorted by a particular value that is part of the query.  In the art query, it sorts by the minimum year for the artwork.

## Practice: Building SQL queries in Python

Now that we have looked at all the main keywords in a SQL query, it's time to start writing our own SQL queries in Python.  To start, we'll first have to install a package that allows us to write SQL queries using the Pandas library in Python.  Create a new cell in your notebook and add these lines:

```
!pip install pandasql 'sqlalchemy<2.0'
from pandasql import sqldf
```

To start, we'll build a SQL query with the same question we asked in the last lesson: what author published the most books in 2002?  As a reminder, here was the code we used last lesson using functions:
```
books_df[books_df['Year-Of-Publication'] == '2002'].groupby('Book-Author').count().sort_values(by=['ISBN'], ascending=False)
```

Now let's see how that query would look in SQL:
```
query = """
   SELECT `Book-Author`, count(*) as total
   FROM books_df
   WHERE `Year-Of-Publication` = '2002'
   GROUP BY `Book-Author`
   ORDER BY total desc
   """
sqldf(query)
```

Here we can see how a SQL query expresses the question we are asking of the dataset.  In the SELECT keyword, we pick what fields we want in the output and we give the `count(*)` function to say we want to see the total amount of books.  In the FROM part of the query, we choose our dataset to be `books_df`.  We filter only for book that were published in the year 2002 in the WHERE part.  Then we use the GROUP BY keyword to specify that we're grouping by author.  And finally, we order by the total count in descending order to show the author with the most books listed first.

Now let's try another of the questions we answered last lesson: how many books start with each letter of the alphabet?  To do so, we'll reuse the code from last time to create a new field representing the first column of the book title.  Then we can build a query to give us our answer:
```
books_df['Book-First-Letter'] = books_df['Book-Title'].astype(str).str[0]
query = """
   SELECT `Book-First-Letter`, count(*) as total
   FROM books_df
   GROUP BY `Book-First-Letter`
   ORDER BY total desc
   """
sqldf(query)
```

### Build your own queries

Now you can try to build your own SQL queries.  Here are a few to start with:
1. How many users are in the dataset?
2. How many books are in the dataset?
3. What are the minimum and maximum ratings that can be given for a book?  (Hint: use `MIN()` and `MAX()` functions in the SELECT part of your query.)

## Summary
In this lesson, we learned about SQL and what the main keywords in SQL mean.  We then were able to write our own SQL queries in Python to ask questions of our data.  We saw how writing a SQL query is similar to using functions.
