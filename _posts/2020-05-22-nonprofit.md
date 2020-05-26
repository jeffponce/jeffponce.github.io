---
title: "Data Anylsis on US Non-Profit Organizations"
date: 2020-05-22
tags: [Data Science]
excerpt: "Machine Learning"
mathjax: "true"
---

# Project Overview
The goal of this project is to better understand US Non-profit organizations and how they perform when compared to each other on based on income, revenue, and assets. Furthermore, we will look at the Top 10 Non-profits in the regions and the Top 10 per state. The Dataset was obtained from Kaggle, which contains information on US Non-profits broken up into three regions. We will analysis the data, isolate the info needed, and export data to be visualized in Tableau. 

Link to Dataset: [Non-Profit]<https://www.kaggle.com/crawford/us-charities-and-nonprofits>

## Data Cleaning
First we import the data into Junpyer Notebooks and display the data to see what they provide.
```python
ds1 = pd.read_csv('eo1.csv') 
ds2 = pd.read_csv('eo2.csv') 
ds3 = pd.read_csv('eo3.csv')

ds1.head()
```
![Non-profit](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Non-profit/dc1.png)
![Non-profit2](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Non-profit/dc2.png)
Lookng at the data we can see most of the information is internal coding to other points of data. For example, Subsection, Affliation, etc. What we need is the basic information on each organization and the financials, *Income/Revenue/Assets*.

First, we take a look at how they broke up the indivdual states.
![Non-profit3](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Non-profit/dc3.png)
We could seperate the data to make them more like the US standard regions, but since we will seperate at the state level this will be fine for the time being.

Below we are seperating the data into a new region variable for vizualiztion. Sorting thr data based on Income and only taking the Name, City, State, Asset, Income, and Revenue columns. Second line adds a new column for the Region. Giving us the Top 10 US Non-Profits based on Income per Region.

```python
#NorthEast Region
ne = ds1.sort_values('INCOME_AMT', ascending=False)[['NAME', 'CITY', 'STATE', 'ASSET_AMT',
                                                     'INCOME_AMT','REVENUE_AMT']].head(10)
ne['Region'] = 'NorthEast'

#MidWest Region
mw = ds2.sort_values('INCOME_AMT', ascending=False)[['NAME', 'CITY', 'STATE', 'ASSET_AMT',
                                                     'INCOME_AMT','REVENUE_AMT']].head(10)
mw['Region'] = 'MidWest/MidAtlantic'

#SouthEast and Western Regions
se = ds3.sort_values('INCOME_AMT', ascending=False)[['NAME', 'CITY', 'STATE', 'ASSET_AMT',
                                                     'INCOME_AMT','REVENUE_AMT']].head(10)
se['Region'] = 'SouthEast/West'
```


### H3 Heading

Here's some text

and here's some *itlaics*

Here's **bold** text



Here's a list:
* First thing
+ Second thing
- Third thing

Here's numbers:
1. First
2. Second
3. Third

Python Code Block:
```Python
    import numPY as np

    def test_function(x,y):
      z = np.sum(x,y)
      return z
```

R Code Block:
```r
library(tidyverse)
df <- read_csv("some_file.csv")
head(df)
```

Here's some in line code `x+y`



Here's another images KRAMDown

Here's some math:

$$z=x+y$$

You can also put in it in line $$z=x+y$$
