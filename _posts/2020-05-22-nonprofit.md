---
title: "Data Anylsis on US Non-Profit Organizations"
date: 2020-05-22
tags: [Data Science]
excerpt: "Machine Learning"
mathjax: "true"
---

# Project Overview
The goal of this project is to better understand US Non-profit organizations and how they perform when compared to each other on based on income, revenue, and assets. Furthermore, we will look at the Top 10 Non-profits in the regions and the Top 10 per state. The Dataset was obtained from Kaggle, which contains information on US Non-profits broken up into three regions. We will analysis the data, isolate the info needed, and export data to be visualized in Tableau. 

Link to Dataset: [Non-Profit](https://www.kaggle.com/crawford/us-charities-and-nonprofits)

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
With a merge and concatation, we get the resulting list below. 

```python
merged_data = [ne, mw, se]
results = pd.concat(merged_data)
print(results)
```
![Non-profit](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Non-profit/dc4.png)
![Non-profit](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Non-profit/dc5.png)

### EDA Lite
I wanted to answer a small question bugging me. Specfically on why they decided to seperate the files based on the states they used. For example, why only put 8 states in eo1.csv and why 24 states in eo3.csv? Could it be based on some metric? Let's find out.

The code below plots a boxplot with the spread of the Top 30 Non-Profits in the US. 

```python
#Plot Style
sns.set(style="darkgrid", palette="muted", color_codes=True)
#Create BoxPlot and Add Points
a = sns.boxplot(data = results, x = 'Region', y = 'INCOME_AMT')
sns.stripplot(x='Region', y='INCOME_AMT', data=results, jitter=True, size=16, linewidth=0, hue = 'NAME', alpha=0.7)
#Legend and Titles
a.legend(bbox_to_anchor=(1.05, 1.0), loc=2, borderaxespad=0.1)
a.axes.set_title('Top 10 US Non-Profits in 2017',fontsize=35)
a.set_xlabel('Region',fontsize=25)
a.set_ylabel('Income',fontsize=25)
plt.show()
```
![Non-profit](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Non-profit/eda1.png)
**Conclusion:** 
First, we looked at Income since that would give us a true indicator of the "Profitablilty" of the organization. Some non-profits may take in a lot of donations, or revenue, but have to spend it on the goals and running the Non-profit. Based on just looking at Income we see that more than likely the partitioning wasn't based on a financial reasoning. Although, the NorthEast holds the highest organization based on Income, Presidents and Fellows of Harvard College, the MidWest/MidAtlantic on average has a higher income with their orginzations. 

### Data Cleaning Part II
Now we will seperate the Top 10 Non-Profits per State based on Income, merge them, and export the new dataset for further EDA in Tableau.

My first instinct was to take my code from above and start creating new variables for each state, for each file, and merge/concat them into a new set. 
```python
ma = ds1[ds1.STATE == 'MA'].sort_values('INCOME_AMT', ascending=False)[['NAME', 'CITY', 'STATE', 'ASSET_AMT',
                                                     'INCOME_AMT','REVENUE_AMT']].head(10)
ny = ds1[ds1.STATE == 'NY'].sort_values('INCOME_AMT', ascending=False)[['NAME', 'CITY', 'STATE', 'ASSET_AMT',
                                                     'INCOME_AMT','REVENUE_AMT']].head(10)
nj = ds1[ds1.STATE == 'NJ'].sort_values('INCOME_AMT', ascending=False)[['NAME', 'CITY', 'STATE', 'ASSET_AMT',
                                                     'INCOME_AMT','REVENUE_AMT']].head(10)
...
merged_state_list = [ma,ny,nj,me,nh,vt,ct,ri,...]
final_set = pd.concat(merged_state_list)
```
Two problems with this method. 
1. This is very repetative and ineffecient way to run this code. In coding there is a principle called keeping your Code DRY, meaning, Don't Repeat Yourself. 
2. We encounter issues with variables names like id, or, and in which have spefic functions in Python.

Then it hit me like a brick wall...the **Groupby function**! Now below does everything that I did above but just in a better way.
```python
# Use the groupby function to exact the data giving us the top 10 from each state.
new_ds1 = ds1.sort_values("INCOME_AMT", ascending=False).groupby("STATE").head(10)[['NAME', 'CITY', 'STATE', 'ASSET_AMT',
                                                     'INCOME_AMT','REVENUE_AMT']]
new_ds2 = ds2.sort_values("INCOME_AMT", ascending=False).groupby("STATE").head(10)[['NAME', 'CITY', 'STATE', 'ASSET_AMT',
                                                     'INCOME_AMT','REVENUE_AMT']]
new_ds3 = ds3.sort_values("INCOME_AMT", ascending=False).groupby("STATE").head(10)[['NAME', 'CITY', 'STATE', 'ASSET_AMT',
                                                     'INCOME_AMT','REVENUE_AMT']]
#Merge and Concat Data
merged_state_list = [new_ds1, new_ds2, new_ds3]

final_set = pd.concat(merged_state_list)
print(final_set)
```
![Non-profit](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Non-profit/dc6.png)

## Exploratory Data Analysis (EDA)

### Map of Average Income per State
![Non-profit](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Non-profit/eda2.png)
Top 5 States:
1.Massachusetts | $18.4B
2.Oregon | $12.6B
3.Illinois | $11.3B
4.Washington | $10.0B
5.Maryland | $8.6B
### Top 10 Based on Income
![Non-profit](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Non-profit/eda3.png)

### Top 10 Based on Revenue
![Non-profit](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Non-profit/eda4.png)

### Top 10 Based on Assets
![Non-profit](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/Non-profit/eda5.png)



