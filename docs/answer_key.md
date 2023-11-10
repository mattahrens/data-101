---
layout: page
title: Answer Key
nav_order: 13
description: Answer Key
---
# Answer Key
Below are answers to the practice problems from various lessons from the course.

## Lesson 5

1. What is the age of the users who did reviews grouped by each age?  Hint: you will have to use the users dataset for this query.
```
users_df.groupby('Age').count().sort_values(by=['Age'])
```

2. What is the overall average age of users?  Hint: you will have to use the `mean()` function.
```
users_df['Age'].mean()
```

3. What is the number of ratings at each ratings (0 - 10)?  Hint: you will have to the use the ratings dataset.
```
ratings_df.groupby('Book-Rating').count().sort_values(by=['Book-Rating'])
```

4. What is the overall average book rating from all ratings?  Hint: you will have to use the `mean()` function.
```
ratings_df['Book-Rating'].mean()
```

5. How many distinct authors are in the dataset?  Hint: you will have to use the books dataset and the `nunique()` function.
```
books_df['Book-Author'].nunique()
```

## Lesson 6

1. How many users are in the dataset?
```
query = """
   SELECT count(*)
   FROM users_df
   """
sqldf(query)
```
2. How many books are in the dataset?
```
query = """
   SELECT count(*)
   FROM books_df
   """
sqldf(query)
```
3. What are the minimum and maximum ratings that can be given for a book?  (Hint: use `MIN()` and `MAX()` functions in the SELECT part of your query.)
```
query = """
   SELECT MIN(`Book-Rating`), MAX(`Book-Rating`)
   FROM ratings_df
   """
sqldf(query)
```

## Lesson 7

1. What book (ISBN) has the most ratings = 10 and which book (ISBN) has the most ratings = 0?
```
query = """
  SELECT `ISBN`, count(*) as total
  FROM ratings_df
  WHERE `Book-Rating` = 10
  GROUP BY `ISBN`
  ORDER BY total desc
"""
sqldf(query)

query = """
  SELECT `ISBN`, count(*) as total
  FROM ratings_df
  WHERE `Book-Rating` = 0
  GROUP BY `ISBN`
  ORDER BY total desc
"""
sqldf(query)
```

2. What is the average age for the top cities in the United States for users in the dataset? (Hint: use the **AVG** keyword in your SQL query.)
```
query = """
  SELECT AVG(`Age`)
  FROM users_df
  WHERE `Location` LIKE "%usa%"
"""
sqldf(query)
```

3. How many unique publishers did J.K. Rowling use for her Harry Potter books?
```
query = """
  SELECT count(distinct `Publisher`)
  FROM books_df
  WHERE `Book-Title` LIKE "%Harry Potter%" and `Book-Author` LIKE "%Rowling%"
"""
sqldf(query)
```

## Lesson 9

1. What user location has the most number of book ratings?
```
query = """
  SELECT `Location`, count(`Book-Rating`) as rating_cnt
  FROM ratings_df
  INNER JOIN users_df
  ON ratings_df.`User-ID` = users_df.`User-ID`
  GROUP BY users_df.`Location`
  ORDER BY rating_cnt desc
"""
sqldf(query)
```

2. What publication year has the least popular books by average rating that has more than 10 ratings?

```
query = """
  SELECT `Year-Of-Publication`, AVG(`Book-Rating`) as rating_avg
  FROM books_df
  INNER JOIN ratings_df
  ON books_df.`ISBN` = ratings_df.`ISBN`
  GROUP BY `Year-Of-Publication`
  HAVING COUNT(`Book-Rating`) > 10
  ORDER BY rating_avg
"""
sqldf(query)
```

3. What age of users has the highest average rating for books that were published between 2000 and 2003?

```
query = """
  SELECT `Age`, AVG(`Book-Rating`) as rating_avg
  FROM ratings_df
  INNER JOIN users_df
  ON ratings_df.`User-ID` = users_df.`User-ID`
  INNER JOIN books_df
  ON ratings_df.`ISBN` = books_df.`ISBN`
  WHERE `Year-Of-Publication` >= 2000 and `Year-Of-Publication` <= 2003
  GROUP BY users_df.`Age`
  ORDER BY rating_avg desc
"""
sqldf(query)
```

## Lesson 10

1. Create a line chart to show the number of unique users who gave ratings per year of publication from 1992 to 2002.  Hint: you will have to use the `DISTINCT` keyword.
```
query = """
  SELECT `Year-Of-Publication` as year, count(distinct(users_df.`User-ID`)) as users
  FROM ratings_df
  INNER JOIN users_df
  ON ratings_df.`User-ID` = users_df.`User-ID`
  INNER JOIN books_df
  ON ratings_df.`ISBN` = books_df.`ISBN`
  WHERE year >= 1992 and year <= 2002
  GROUP BY year
  ORDER BY year
"""
year_counts = sqldf(query)
year_counts.plot.line(x='year', y='users')
```

2. Create a pie chart for the number of books per year of publication from 1992 to 2002.  

```
query = """
  SELECT `Year-Of-Publication` as year, count(books_df.`ISBN`) as books
  FROM ratings_df
  INNER JOIN books_df
  ON ratings_df.`ISBN` = books_df.`ISBN`
  WHERE year >= 1992 and year <= 2002
  GROUP BY year
  ORDER BY year
"""
year_counts = sqldf(query)
year_counts.plot.pie(x='year', y='books')
```

3. Create a scatter plot to show the relationship between year of publication and average book rating (for 1992 - 2002).  Each book should be a single point in the plot.

```
query = """
  SELECT `Year-Of-Publication` as year, avg(`Book-Rating`) as rating_avg
  FROM ratings_df
  INNER JOIN books_df
  ON ratings_df.`ISBN` = books_df.`ISBN`
  WHERE year >= 1992 and year <= 2002
  GROUP BY year
  ORDER BY year
"""
year_counts = sqldf(query)
year_counts.plot.scatter(x='year', y='rating_avg')
```


