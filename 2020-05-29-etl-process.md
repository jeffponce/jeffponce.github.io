---
title: "ETL Process and Challenge"
date: 2020-05-29
tags: [Data Science]
excerpt: "Data Cleaning & ETL"
mathjax: "true"
---

# Project Overview
The goal of this project is to show my process in preforming ETL on a new dataset and how to find errors we would want to remove before preforming any analysis. The dataset was part of a challenge through SuperDataScience, a platform that teaches data science. In this process we will be using a combination of NotePad++, Excel, SSIS, and SQL to try to find errors in the data that would skew the analysis. Note on Macs the process would be slightly different, NotePad++, SSIS, and SQL are only program that run on Windows. There other solutions like Atom/Brackets as your text editor and PostgreSQL for SQL. I may choose to run this process on Mac in another post since I also do work on my MacBook Pro.

The dataset is just over 1.05M rows and has 5 errors that we need to try to find. Below is the only info we were given in the challenge.
1. The CustomerID field does not contain duplicate records.
2. You know that the total projected revenue for 2016 equals: $419,896,187.87.

Link to GitHub Repo: [GitHub]()

Link to Tableau Visualizations: [Visualization]()

## Part I: NotePad++ & Excel
Now to start, the most important thing is to track as much as possible the changes to the data from the original data and keep a copy of the original data always unchanged. This allows us to have options in case we make any mistakes. In my GitHub Repo there is break down of the way I format the folders. I make a copy of the original data and move it to the prepared data folder to work on. 

Now opening the data in NotePad++..
![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl.PNG)

## Part II: SSIS
I wanted to answer a small question bugging me first. Specifically on why they decided to seperate the files based on the states they used. For example, why only put 8 states in eo1.csv and why 24 states in eo3.csv? Could it be based on some metric? Let's find out.

## Part III: MS SQL
Now we will seperate the Top 10 Non-Profits per State based on Income, merge them, and export the new dataset for further EDA in Tableau.

## Exploratory Data Analysis (EDA)

## Final Thoughts
I really appricate anyone who took the time to read through. I'm mainly building these posts as a way to reteach myself the tools and techniques I have been using and learning the past year and half. Hopefully with the help of the Protégé Effect where by teaching, or even pretending to teach, information to others helps that person learn the information. I'm looking forward to making more complex projects and solving business problems. Thank you again!
