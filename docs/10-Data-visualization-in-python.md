---
layout: page
title: Lesson 10 - Data visualization in Python
nav_order: 11
description: Lesson 10 - Data visualization in Python
---
# Lesson 10 - Data visualization in Python

## Objective

- Learn about different types of data visualizations
- Understand how to use different visualization functions in Python
- Know when to use which type of data visualization

## Concept

We're going to go beyond querying data and now visualizing data.  Data visualization is important because it can help us understand data in different ways than looking at records.  It can show us relationships or trends in the data that we are analyzing.  We're going to look at 4 basic data visualizations and how to use Python to display them.  We'll start by generating data that represents the count of ratings per rating (0 - 10).  Here is the query:

![image](images/10-ratings_data.png)

Now that we have the data, we can plot the data with different `plot` functions.  The plot function is called against the dataframe that we created (`rating_counts`).  We'll start with a line chart, which will display a continuous line across the data.  The `plot.line()` function takes two items -- the x-axis and the y-axis for the chart.  For our data, we will use the rating as the x-axis and the count of ratings as the y-axis.

![image](images/10-line_chart.png)

The line chart is good for showing trends across data on the x-axis.  The bar chart shows a similar view but it has a bar for each item on the x-axis instead of a continuous line.  The `plot.bar()` function also takes the same items as input to the function.

![image](images/10-bar_chart.png)

![image](images/10-pie_chart.png)
![image](images/10-scatter_plot.png)
## Practice: 

## Summary

