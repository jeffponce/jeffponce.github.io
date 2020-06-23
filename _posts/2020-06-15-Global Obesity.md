---
title: "Global Obesity 1975-2016"
date: 2020-06-10
tags: []
excerpt: "Data Analysis"
mathjax: "true"
---

# Project Overview
The goal of this project is to better understand global obestiy and how it's changed over the years. This dataset comes from the WHO and looks at the BMI for Males, Females, and an averaged BMI for both genders.  We will clean the data and do some exploratory data analysis on the data to answer some questions. I also want to create a map that will show the change over time. Seeing which countries in 2016 have a BMI higher than 30. I will do this by joining anouther dataset that I like to use, countries of the world.csv, which has additional information such as population, regions, GDP, etc. I will add the dataset to my Github Repo, the Gif will also be added and link to it is below.

Which countries have the highest average BMI?
How has the BMI changed over the decades?

Link to GitHub Repo: [GitHub](https://github.com/jeffponce/non-profit-analysis)

Link to Tableau Visualizations: [Visualization](https://public.tableau.com/profile/jeff.ponce#!/vizhome/Obesity_15923286441470/Dashboard1)
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

Next we will map the genders using the numbers we aquired from the split we did. None will be `both sex`, 1 will be `male`, and 2 will be `female`. 
```python
# Mapping the gender using the numbers we split
df['gender']=df['gender'].map({None:'both sex','1':'male','2':'female'})
df
```
![Obesity](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Obesity/ob2.png)

We will also use the `str.split` function to seperate the lower and higher estimate from the averaged BMI. Using the `-` and `[]` alllows us to isolate the numbers from the data. The last part reorders the columns for this new dataset.

```python
# Seperate BMI Values
df.rename(columns = {'value': 'BMI'}, inplace=True)
df_copy = df.copy()
df['BMI'] = df_copy['BMI'].str.split('[', expand=True)
df['lowest_est_BMI'] = df_copy['BMI'].str.split('[', expand=True)[1].str.split('-', expand=True)[0]
df['highest_est_BMI'] = df_copy['BMI'].str.split('[', expand=True)[1].str.split('-', expand=True)[1].str.split(']', expand=True)[0]

# Reset the column order
df = df[['country', 'year', 'gender', 'BMI', 'lowest_est_BMI', 'highest_est_BMI']]
df
```

![Obesity](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Obesity/ob3.png)

This look pretty good and one might assume to just start doing anaylsis, but I like to do more checks to be sure we dont get scewed data. Lets look at the rows with no data.

```python
print(df[df.BMI=='No data'].country.value_counts())
```

We get four countries that have no data, South Sudan, Sudan, San Marino, and Monaco. The below code will remove these countries from the dataset. 879 rows were removed.

```python
# Remove no data rows
df1=df.dropna(subset=['country'])
df1=df1.drop(df[df.country=='Country'].index)
con=df1[df1.BMI=='No data'].country.value_counts().index
df2=df1[~df1.country.isin(con)]
```
Now let's look at our data types. Below we see that BMI, lowest_est_BMI, and highest_est_BMI were set as objects, we will need to switch them over to floats. The code below is one way to get this accomplished. 

![Obesity](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Obesity/ob4.png)

```python
df2['BMI'] = pd.to_numeric(df2['BMI'], errors = 'coerce')
df2['lowest_est_BMI'] = pd.to_numeric(df2['lowest_est_BMI'], errors = 'coerce')
df2['highest_est_BMI'] = pd.to_numeric(df2['highest_est_BMI'], errors = 'coerce')
```
Now we see these set as floats.

![Obesity](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Obesity/ob5.png)

Only thing left to check is the counts on the year and gender columns. Below we see everything is looking good. Time to do some EDA!

![Obesity](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Obesity/ob6.png)

![Obesity](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Obesity/ob7.png)



## Exploratory Data Analysis (EDA)

### Distribution Change -  10 Year

The below code helps us understand how the BMI has changed over the decades. As we can see the distribution starts to move to right, meaning on average we have a higher BMIs then our 1975 counterparts. Very interesting to see the constant dip in the middle range of BMIs. 

```python
# Distribution Every 10 Years

sns.distplot(df2[df2.year=='1975'].BMI,hist=False,label='1975')
sns.distplot(df2[df2.year=='1985'].BMI,hist=False,label='1985')
sns.distplot(df2[df2.year=='1995'].BMI,hist=False,label='1995') 
sns.distplot(df2[df2.year=='2005'].BMI,hist=False,label='2005') 
sns.distplot(df2[df2.year=='2016'].BMI,hist=False,label='2016')

plt.title('BMI Distribution through the Years',size=20)

plt.legend(bbox_to_anchor=(1.05, 1), loc=2, borderaxespad=0.2, fontsize = 'x-large')

plt.show()
```
![Obesity](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Obesity/eda.png)

We see a similiar distirbution change with the viola charts that we use to seperate between both sexes, males, and females. We do see a larger BMI distirbution with females than males.

```python
data_temp=df2[df2.year.isin(['1975','1985','1995','2005','2016'])]
g = sns.FacetGrid(data_temp, row = 'gender', col = 'year', hue = 'gender')
g = g.map(sns.violinplot, 'year', 'BMI')
plt.show()
```
![Obesity](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Obesity/eda1.png)

### Top 10 Countries based on BMI

```python
data_temp1=df3[df3.year.isin(['1975','1985','1995','2005','2016'])]
g = sns.FacetGrid(data_temp1, col = 'year', sharey=False)
g = g.map(sns.barplot, 'BMI', 'country')
plt.show()
```
![Obesity](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Obesity/eda2.png)

The visual above doesn't change much over the decades. Seems rather misleading as although I can understand per capita these Polynesian/Micronesian islands may have higher BMI, other countries have increased much over the decades. Below I created a Gif from a Tableau graph using this data to visualize some of the other countires we see increases. As we can imagine, USA and Austrilia are high but also some middle eastern countires like Egypt and Saudia Arabia. 

<div style="width:360px;max-width:100%;"><div style="height:0;padding-bottom:76.39%;position:relative;"><iframe width="360" height="275" style="position:absolute;top:0;left:0;width:100%;height:100%;" frameBorder="0" src="https://imgflip.com/embed/460mnm"></iframe></div><p><a href="https://imgflip.com/gif/460mnm">via Imgflip</a></p></div>

## Final Thoughts
This was a good project to practice some data cleaning on Python which was something I was to incorperate in my future projects. I think as an American, sometime we make assumuption about the world and although I've known about our obesity problems. It was helpful to get dirty and visualize to truly see what is going on in the world. I never thought of the Middle East having a higher BMI than some Western European countries. Having family in Chile and Argentina, it's interesting to see their BMis being slightly higher than the rest of south American countries. From experiance I know they have a diet that revolved around white bread and grilled meats. As we can see China and India have lower BMIs, where they eat slightly more vegeterian diets. I believe other factor can be attributing to these numbers, such as lack of food or higher poverty. I think as all things we need moderation and maybe eat some more veggies with that grilled steak!

Note: I did load this data and join it with another dataset, countries of the world, which I use to add regions, population, and other demogaphics to other data. In this case, we really couldn't use much of the information since I decided to keep it simple. I will add the code, dataset, and the uploaded dataset used in Tableau.

