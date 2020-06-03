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
3. Give a small explantion to how the error might of occured.

Link to GitHub Repo: [GitHub]()

Link to Tableau Visualizations: [Visualization]()


## Part I: NotePad++ & Excel
Now to start, the most important thing is to track as much as possible the changes to the data from the original data and keep a copy of the original data always unchanged. This allows us to have options in case we make any mistakes. In my GitHub Repo there is break down of the way I format the folders. I make a copy of the original data and move it to the prepared data folder to work on. 

Now opening the data in NotePad++ 

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl.PNG)

We see that this is a dataset from a car sevice company. We have three columns, CustomerID, CustomerSince, and Car, that describes the customer and the car serviced while the other three are what each customer spent that year. Below we see that we have 1.05M rows which due to excels limitation, second image, we will need to spilt the data and combine them after we load it into Excel. Also note that this is a semicolon seperated file which is important when loading into Excel.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl1.PNG)
![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl2.PNG)

In NotePad++ we use `CRTL-G` to go to row 1M and cut everything to the bottom. Save this file as `..copy1` and create a new file with the remaining rows and name it `..copy2`. Now we preform a test to see that the begining of `..copy2` is the end of `..copy1`. As CustomerID is usually a unique number, will verify this later, we can see that we are good and didnt accedentily delete something.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl3.PNG)
![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl4.PNG)

Now we move on to Excel. We open our files in an empty Excel sheet to it goes through the Text Import Wizard.

Here we want to put it as delimited, click next.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl5.PNG)

Here we uncheck Tab and check Semicolon as your delimiter. Why it's important to know get to know the file before loading.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl6.PNG)

Here we highlight all the columns and switch everything to text. Click Finish.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl7.PNG)

Now that we have the data loaded. We will make sure all the columns are formated properly, first with the dates. Although already in YYYY-MM-DD format we want to make sure nothing changes when we export the data in a csv file. Using Text to Column in the Data tab below are what we need to do.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl8.PNG)
![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl9.PNG)

Next we will work on the sales columns. Similiar process Text to Column, convert to number, and fix the first row as text since this is the Year. 

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl13.PNG)

With that the file is ready to be exported as a csv file. We will down the same process above to the `..copy2` file and export that as a csv file. Now we open them both in NotePad++ and merge them together into a new file called `..-Combined`.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl15.PNG)

We will take this file and load it up in SSIS next to start checking for any errors in the data. The reason we format it in Excel first is when we load into SSIS, Excel would have created a new column if there was any issue with a delimiter or a typo in any row. There are other ways to check for this but this has worked for me well. (In the few project ive done with uncleaned data)


## Part II: SSIS
SSIS is a ETL tool that allows us to find and errors in the dataset. SSIS its self is very versitile and can be used for a lot more than what we will be using it for, but it is very powerful.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl16.PNG)

We start by starting a New Project and choosing the Interation Services under the Business Intellegence section. Give it name such as Car Sevice and click `OK`.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl17.PNG)

When it loads up we will be in the Control Flow tab on the top. We will need to drag out a Data Flow Task into the Control Flow window. Give it name similiar to the project name, you can also give it the date. Clikc on the Data Flow tab and now we are on the main page where we will be performing our ETL.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl18.PNG)

We will need to drag out a Flat File Source from Other Sources in the SSIS toolbox on the left. This is how we will be loading the data into SSIS. Next we, in this situation, will drag out the OLE DB Destination which will load the "cleaned" data in MicroSoft SQL. If you wanted to a csv file, you can use the Flat File Destination to create that file. 

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl19.PNG)

Double-click on the Flat File Source and then click on Browse.. to find your `..Combined` file to load up. Change the text delimiter to double quotes("). Next check the columns.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl20.PNG)

Below we see why it was important to take the data and load it into Excel. Although tedious to most, it allows us to identitfy any row shift from errors in the data. Excel helps us ID them by creating this new `Column 6` and when we load into SSIS, SSIS will also ID it as a column. We've found our first error and next we will find the way to exact it from over 1M rows. 

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl21.PNG)

Continuing, in the Advance section we will highlight all the Columns and adjust the OutputColumnWidth to something wont truncate your data and give you errors. 1000 in this situation should be just fine, click OK to finish.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl22.PNG)

Now Flat File Source no longer has a Red X on it so we're clear to move forward.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl23.PNG)

We will take a Conditional Split from SSIS Toolbox and a Flat File Distrination for location to place any error records we find using the conditonal split. We format the split first.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl24.PNG)

Here in the Conditional Split we will need to logically test how to ID row shift. We name the Output Name `Bad Records` and in the condition we will use `LEN([Column 6]) > 0` to check the length of all the rows in Column 6, since we shouldnt anything in this column anything but zero is an error. Using the logical or, `||` we will also check for any row shifts to left or in Column 2016E. Here we will use `LEN([2016E]) == 0` to check if we have any empty cells that column. Remember to name the Default Putput Name to `Good Records`. Click OK and we're done here. Note: If we have any important data that is essential, we would use this same method to make sure it was included in the data.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl25.PNG)

Setting up the Flat File Destination is simliar as before. Click Browse, then here we will create a text File `2020_05_08_BadRecords` in a folder for Removed Rows to account for any changes. This file will be where SSIS puts any error rows we find. 

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl27.PNG)

With these all set up, we will dray the blue arrown from the Flat File Source to the Conditional Split. Next we take the Blue Arrow in Conditional split and drag it tpwards the Flat File Distination, choosing Bad Records as the Output. When we drag the again from Conditonal Split to the OLE DB Distination, it will automatically set it to Good Records.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl28.PNG)

Now we will set up the working table in MS SQL by setting up your Database and then clicking New to open a SQL scripted used to create the table. We add `[RowNumber] int indentity(1,1)` to add a new column to track row numbers and change the table name to `RAW_CarService`.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl29.PNG)

Note: Sometimes we have issues when setting up the SQL database. To fix this we go into the OLE DB Destination and on the right we switch the AlwaysUseDefault parameter to `True`.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl30.PNG)

Once everything is set we press Execution Results button on the top right to start the ETL process. We should see something similiar to the below. This could take some time to run as it is over 1M rows.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl31.PNG)

After it finishes we should see something similier to the below. We've found 1 Bad Record and loaded into the Text file we set up. 

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl32.PNG)

Before we check it in NotePad++ we will go back to the Control Flow tab and right click the Dats Flow Task and disable it.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl33.PNG)

### First Error
Using the Bad Record file we can check which row had the error. Going back to the orginal data we see that the row shift was due to the extra ; in between 118 and 01 making it two seperate numbers. There must have been a error in loading the data that caused it to add the semicolon.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl34.PNG)
![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl35.PNG)


## Part III: MS SQL
Now we will move over to Microsoft SQL Server Management Studio, open up our database, and check if our RAW table was created from SSIS. As we can see, it was completed correctly. 

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl36.PNG)

Below is the Stored Procedure template that we will use to convert a RAW table that we created using SSIS. This also allows us to have a record of how we converted the tables. 

```SQL
USE [DSTRAINING]
GO
/****** Object:  StoredProcedure [dbo].[__tmp1__BLD_WRK_TableName]    Script Date: 5/28/2020 8:22:27 PM ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
ALTER PROC [dbo].[__tmp1__BLD_WRK_TableName]
-- =============================================
-- Author:	
-- Create date: 
-- Description:	RAW to WRK Table
-- Modified Date: 
-- =============================================
AS
BEGIN
-- =============================================
-- Drop Table
-- =============================================
IF OBJECT_ID('WRK_TableName') IS NOT NULL
DROP TABLE [WRK_TableName]

-- =============================================
-- Create Table
-- =============================================
CREATE TABLE [WRK_TableName] 
(
	[RowNumber]		INT IDENTITY(1,1)
	,[AAA]			VARCHAR(100)
	,[BBB]			VARCHAR(1000)
	,[CCC]			DATE
	,[DDD]			INT
	,[EEE]			FLOAT
)

-- =============================================
-- TRUNCATE Table
-- =============================================
TRUNCATE TABLE [WRK_TableName]

-- =============================================
-- INSERT INTO
-- =============================================
INSERT INTO [WRK_TableName]
(
	[AAA]			
	,[BBB]			
	,[CCC]			
	,[DDD]			
	,[EEE]
)
SELECT
	[xAAA]
	,[xBBB]
FROM [RAW_TableName]
--(x row(s) affected)

END
```
Below we replaced the `TableName`, add our author info, and start the process of creating the shell of the WRK table. In the `CREATE TABLE` section we will add the Column names and the column data type. `VARCHAR` for text, `DATE` for the dates, and `float` for the year's sales numbers. Note that in the far right window we are performing a test to check that we have an empty column for `[Column 6]`. Beautiful, moving forward.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl38.PNG)

Here we will use `INSERT INTO` to move the data in the RAW table to the newly made WRK table. Since we set up the data types in the `CREATE TABLE` section through implicit conversion we will not need to add them here. Run the code and we get our second error.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl39.PNG)

### Second Error
Here we got the error message `Error converting data type varchar to float.` This is the benefit of starting with a RAW table and converting into a WRK. Because of the implicit conversion, if we try to add data that doesnt conform to the data type we selected it will give us an error. Since the error was for the Floats we only have to check the 2014, 2015, and 2016E columns. 

Below we start by opening a new query window and trying to find the error at each column. The first part of the SQL code below is checking that all the data in Column 2014 is a number,`isnumeric()`, if it's false we get a 0 meaning there's a string somewhere. The second portion filters the rows that have empty cell since those wouldn't be real errors.  

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl40.PNG)

Checking 2015 column we see the error. Somehow when the original data was created there was an `$` entered instead of a `.` for the sales number. Checking column 2016E we see this is the only error. 

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl41.PNG)

We will fix this issue by excluding this whole row from being inserted into the new WRK table. We do this by added a `WHERE` condition to the end of the `INSERT INTO` section. By flipping the logic from our test code we will exclude this row.

```SQL
...
)
SELECT
	[CustomerID]
	,[CustomerSince]
	,[Vehicle]
	,[2014]
	,[2015]
	,[2016E]
FROM [RAW_CarService_20200529]
---EXCLUSION
WHERE ISNUMERIC([2015])	= 1
OR [2015] = ''
--(1409998 row(s) affected)
```
## Part IV: MS SQL Continued
Next we can check for any date errors. We do this by thinking a little bit about the business. How old do you think this company would hold on to it's records? How old could this company be? Older than 50, 60 years? These are just things we may have to check. I'm making an assumption that this company can't have data older than 1965. Second portion of the code checks that there arent date issues for the future, in this case past 2016. Here we see our 3rd Error

### Third Error
This one seems to be a typo error as well, meaning to enter 1999 instead of 1899. Unless this company was servicing horse and buggy!?!

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl44.PNG)

Next lets check if we truly have unique numbers for CustomerID. We do this by using the `COUNT()` function to create a new column counting the number of CustomerID grouping by CustomerID and only pulling the rows where `COUNT` is greater than 1 so any duplicates. 

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl42.PNG)

### Fourth Error
Here we see that we have 2 duplicate CustomerID. Taking it further, we can use the CustomerID `3490750` to check what happpened at these rows. As we can see, there was an error in creating the CustomerID as the rest of the data seems to indicate two seperate customers.

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/ETL43.PNG)

### Fifth Error
For the last error we did a couple different check. I looked at average, min, and max for the sales columns. We find our final problem by seeing that most of the column averages were around 300 and 2015/2016E maxes were in the similiar 300-400 range. 2014 max however has a max of 2000 which is a major outlier in this dataset. 

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/ETL45.PNG)

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/INFO.PNG)


Finally we will preform the final sum check. Adding up all the 2016E and making sure it match what we recieved in the begining of this challege. In order to do so we will gather the excluded rows and get the current total of the 2016E from SQL. Using Excel to see if everything adds up and does!

![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl46.PNG)
![ETL](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/ETL/etl47.PNG)


## Final Thoughts
I really appricate anyone who took the time to read through. I'm mainly building these posts as a way to reteach myself the tools and techniques I have been using and learning the past year and half. Hopefully with the help of the Protégé Effect where by teaching, or even pretending to teach, information to others helps that person learn the information. I'm looking forward to making more complex projects and solving business problems. Thank you again!
