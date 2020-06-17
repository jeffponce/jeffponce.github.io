---
title: "Global Obesity 1975-2016"
date: 2020-06-10
tags: []
excerpt: "Data Analysis"
mathjax: "true"
---

# Project Overview
The goal of this project is to better understand global obestiy and how it's changed over the years. This dataset comes from the WHO and looks at the BMI for Males, Females, and an averaged BMI for both genders.  We will clean the data, isolate the info needed, and export data to be visualized in Tableau. 

Link to Dataset: [Non-Profit](https://www.kaggle.com/crawford/us-charities-and-nonprofits)

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

#Import Data using Pandas
ds1 = pd.read_csv('eo1.csv') 
ds2 = pd.read_csv('eo2.csv') 
ds3 = pd.read_csv('eo3.csv')

ds1.head()
```

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

