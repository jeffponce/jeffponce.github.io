---
title: "Marketing Dashboards"
date: 2020-07-01
tags: 
excerpt: "Data Anlysis"
mathjax: "true"
---

# Project Overview
The goal of this project to showcase three powerful dashboards that can be used to improve marketing decisions. We will do a buyer persona dashboard to understand the demographics of our customers. Next we will create a email marketing dashboard that can help understand what types of email campaign work best and when to send them to your email lists. Finally we will look at a quick way to see which promotions are making the strongest waves when it comes to sales. These dashboards are a great tool to increase the ROI for marketing campaigns and adds great value to marketing managers and sales to direct their attention to what is going to directly increase sales. 

The datasets are sample dummy data from Google Anaytics provided by SuperDataScience.
 
Link to Tableau Public: [Tableau](https://public.tableau.com/profile/jeff.ponce#!/?newProfile=&activeTab=0)

## Part I: Buyer Persona Dashboard
First we start off with a good way of visualizing demographic data of customer in an easy to read and interactive dashboard. Below we will go over each portion of the dashboard and how we can use it to indetify who are our customers.  

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db.png)

We have created idivdual KPIs, shown below, and place them at the top of our dashboard. I like to include these as numbers instead on the Tooltip of the graph so it give a good visual on what the numbers are when we start to filter in data.

These are important to have for a marketing manager or sales person who want to get the information as quickly as possible. Without getting into too much of the weed, below are breif explaination of the KPIs, or Key Performace Indicators.

* Total Sales: We can use this to see what is selling the highest, where are we getting the highest sales, etc.  
* Average Sale: Good indicator of the type of customers. Do they buy few expensive items, or a lot of inexpensive items?  
* Number of Customers: Good when analysing territories and seeing where we are getting the most traction for our products/service.

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db1.png)

Here we have a standard bar chart showing Total Sales seperated by the Category of items. We will be using this graph as a filter to dig deeper into the data. As we can see in this sample data, sales of handmade items account for a bulk of the sales for this company. 

* How can we use this to isolate what items to sell more of?  
* Can we start pivoting away from other items, such as vintage or furniture?  
* How does this look after we start isolating data?  

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db2.png)

Our second visualization on this dashboard will be a map with the total sales of each state. This company seems to be mainly based in North Carolina and has stores, or sales, in the southeast. We can use this see where our company is making headwinds and where we would need to focus on expanding. 

* How can we use this map to check our Sales by Category graph from before?  
* Are handmade items selling only in North Carolina?  
* Perhaps Florida has higher sales in Furniture?  
* Would pivoting away from Furiniture hurt business in Florida? Should we care?  

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db3.png)

The last visualization is your standard age and gender distribution bar chart. We can use this graph to identify the age group and the gender of our customers. For marketing this is quite useful for marketing campaigns. 

* Using the two graphs from before, who do we target?  
* Who are our customer base? Who should we send promotions to?  
* What age group purchase high cost items?  
* How can we use this information to grow sales?  

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db4.png)

Below we see the interactivity of this dashboard. As we start to click on our Sales by Category graph and/or our Sales by State map, these will filter to breakdown the data further. Is this example, we can see a majority of the customers from North Carolina that bought handmade items were 18-35 year old females. 

* How can we use this for our advantage in advertising our products?  

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db5.png)

I wanted to isolate where the majority of our business is coming from. Here we see that 18-45 year old females make up about a quarter of our total sales through all our regions.

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db6.png)

Here we take it a step further. Close to half of our total sales came from 18-45 year old females and 18-35 year old males. This should be our target demographic for our products. Marketing should focus on creating promotions, emails, etc. focused on what this demographic in mind. Sales people can use this as a guide on who to focus on when customers come into the stores. Very quick to use and easy to make data based business desicions.

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db7.png)

## Part II: Email Marketing Dashboard

This next dashboard is usesul for email marketing data and see what is working and what is not working. You can also use this to test the effectiveness of our email campaigns and increasing ROI. Dashboard has three sections to it. Top portion is our KPIs, next we have visualizations to see our sucesses, and the bottom portion has a calender heat map that shows when our emails are most effective. I will show the heat map later below when I show the visualizations indivdually. 

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db8.png)

Here we see the important KPIs that relate to email marketing. Each helps our marketing manager have a quick view to how their campaign are going.

* Total Sent: Give us the total amount of emails sent out.
* Open Rate: The percentage of emails that were opened by the targets or customers. So we can see that emails are being opened and at least getting to a real person.
* Total Unique Click: Help us see the true amount of clicks we get from our emails. For example, this will not include a customer who clicked on the link twice. 
* Click Through Rate: This is the rate of the actual amount of people who clicked on your link in the email. Strong indicators of the interest of your content.

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db10.png)

Our first visual is a treemap of the breakdown of our email marketing lists. We have our Master list, the Rewards Program list, and a target demographic list. This helps marketers determine what content to send to different targets. Very qucikly we can see that the Master list, which has the most email addresses, but has only a 5% Click Through Rate. Versus out Rewards Program list that has a 17% Click Through Rate. Why, and how can we improve that KPI?

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db11.png)

This next visualization is a breakdown of our emails based on there type and Click Through Rates. We can use this to see which type of emails, Awareness, Promotion, and Discount, have the higher success rate or customers clicking on our links inside our emails. Very powerful when it come to ROI and making sure we are focusing on marketing that is successful.

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db12.png)

Our final visualization is one of my favorite for marketing, a calendar heatmap! This breaksdown the date and time of emails that were sent and compares the Open Rate, which give us the best day and time to send our email campaigns. As we start to use the fist two vizualzation this will change our calendar to show the best open rates for different campaigns or emails lists. 

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db9.png)

Starting off, lets look at the breakdown of the Master list versus the Rewards Program list. As we see in the Master list we have a low Click Through Rate, so very few people are clicking our links. Another key thing is that only 26% of the total emails sent are being open at all in the Master list. Why?

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db13.png)

When we compare to the Reward Program list, we see that they have a much higher Click Through Rate, 17% versus 5% in the Master list. Furthermore, we see that Awareness emails are extremely effective with out loyal customers, average Click Through Rate is 8% so 26% is rather high. Finally, we see that the Open Rate for our loyality customers is 67% much higher than 26% from our Master list. 

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db14.png)

In the below senerio, the marketing manager request to find the best times to send Awareness emails to our Reward Program list customers. As we can see, we highlighted our Reward Program list and the Awareness email type. 

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db15.png)

Here we see that the best time to send would be Tuesday and Wednesday after 3pm. We also see a strong Open Rate on Saturday after 12pm. Now we can target these customer on these days to reduce excess emails and increase ROI.

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db16.png)

Here we will answer the question, what in everything that is good in the world happened to our Master list and why do we have such low KPIs. One thing I want to throw out there first is that as this is a largest list, maybe it a better gauge of the true average. Maybe we go lucky with out Reward customer emails. Below we will work to check if there's anything wrong with the list. 

We start comparing the Bounce Rate and Unsubcribed Rate between each email list. Bounce Rate tells us the amount of emails that get bounced back to us due to the emails being incorrect, as we can see for the Master list has a higher bounce rate. Unsubcribe rate is a good indicator of our quality of content, more people are unsubcribing to our Master list than the others. 

* How can we adjust our content to start improving this metric with our Master list customers?
* How can we convert them over to Reward Program customers?
* Can we start tracking the bouced emails and delete or fix them?

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db17.png)

## Part III: Promotional Impact 

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db18.png)

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db19.png)

![DB](https://raw.githubusercontent.com/jeffponce/jeffponce.github.io/master/images/marketing_dashboards/db20.png)

## Final Thoughts
Many data science websites, bloggers, and teachers say that data processing and cleaning can be take up to 50-80 percent of your time on a project. Meaning these tools and skills can be the most important part and ensures reliability in the conclusions we make in our analysis. As I do more projects, I can attest to the fact that most models can be reused. One can use a template to get most of the model up and running in a relatively short amount of time. Total, without the 30 plus minute SSIS conditional split, it took us about 45 minutes to just find five errors in this challenge. One can only imagine Big Data datasets that can have billions of rows...I think I would need a couple computers, or maybe a GPU on AWS?
