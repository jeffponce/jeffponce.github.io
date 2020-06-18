---
title: "Global Obesity 1975-2016"
date: 2020-06-10
tags: []
excerpt: "Data Analysis"
mathjax: "true"
---

# Project Overview
The goal of this project is to better understand global obestiy and how it's changed over the years. This dataset comes from the WHO and looks at the BMI for Males, Females, and an averaged BMI for both genders.  We will clean the data and do some exploratory data analysis on the data to answer some questions. I also want to create a map that will show the change over time. Seeing which countries in 2016 have a BMI higher than 30. I will do this by joining anouther dataset that I like to use, countries of the world.csv, which has additional information such as population, regions, GDP, etc.

Which countries have the highest average BMI?
How has the BMI changed over the decades?

Link to Dataset: [Global Obesity]()

Link to GitHub Repo: [GitHub](https://github.com/jeffponce/non-profit-analysis)

Link to Tableau Visualizations: [Visualization](https://public.tableau.com/profile/jeff.ponce#!/vizhome/2017Non-ProfitAnalysis/Non-ProfitAnalysis)
## Data Cleaning
First we import our libraries, like Pandas, NumPy, and Seaborn, with some other parameters. Next we import the data into Jupyter Notebooks and display the data to see what they provide.
```python
# Import Libaries and Parameters for Seaborn.
import pandas as pd
import os
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline 
plt.rcParams['figure.figsize'] = 20,20
import warnings
warnings.filterwarnings('ignore')

# Import Data
data = pd.read_csv('data.csv')
data.head(10)
```
![Obesity](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Obesity/ob.png)

Some thing we can see off the bat is that this data is in what they called wide form, we will need to fix that. The first column is `Unnamed: 0` which we will rename or drop depending on how the pivot turns out. We have 2016, 2016.1, and 2016.2 as an indicator for Male, Female, and Both Genders. The BMI has a lower estimate and a higher estimate which we will need to seperate from the actual BMI.

Looking at it, I think we will rename the column before the pivot to be sure we dont lose information. The Melt() function is a very useful way to pivot the data from wide form into long form which is more how computers read data than how humans read it.

```python
# Rename Column & Preform Pivot
df = data.copy()
df.rename(columns={'Unnamed: 0':'country'}, inplace=True)
df=df.melt(id_vars=['country'],var_name='year')
```

Next we will drop the top three rows as they are just extra information, this will also reset the index to account for the removed rows. Our thrid line of code will split the year column using the `'.'` portion to use the numbers to assign the genders.

```python
# Drop the first three rows and Split the year to get gender
df = df.drop([0,1,2]).reset_index()
df = df.drop(columns = ['index'])
df[['year','gender']] = df['year'].str.split('.',expand=True)
df
```
![Obesity](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Obesity/ob1.png)

## Exploratory Data Analysis (EDA)

### Map of Average Income per State
![Non-profit](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Non-profit/eda2.png)

Top 5 States:
1. Massachusetts  $18.4B
2. Oregon  $12.6B
3. Illinois  $11.3B
4. Washington  $10.0B
5. Maryland  $8.6B

### Top 10 Based on Income
![Non-profit](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Non-profit/eda3.png)

### Top 10 Based on Revenue
![Non-profit](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Non-profit/eda4.png)

### Top 10 Based on Assets
![Non-profit](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Non-profit/eda5.png)

## Final Thoughts
I really appreciate anyone who took the time to read through. I'm mainly building these posts as a way to reteach myself the tools and techniques I have been using and learning the past year and half. Hopefully with the help of the Protégé Effect where by teaching, or even pretending to teach, information to others helps that person learn the information. I'm looking forward to making more complex projects and solving business problems. Thank you again!

