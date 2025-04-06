# Share Local Media Data Analyst Interview Project

We would like you to complete this assignment prior to the next round of interviews.

You can answer the questions using tools and methodology of your choice. Past candidates have used Jupyter Notebooks, SQL, Python and/or R.

We would like you to present your results, along with a brief introduction and overview of your skills and experience, to a mixed audience of both technical and non-technical employees. You should prepare a Powerpoint/Keynote presentation to go with the assignment.

For an in-person presentation, you will be able to connect to a screen. Feel free to bring your own computer or send the slides in advance.

## Introduction
You are analyzing the performance of a direct mail marketing campaign that was recently sent on behalf of a client. Please answer the below questions using the example datasets provided.

### Datasets

Four CSV files are provided:

 * Dataset 1A: Transactions file - a list of recent orders, provided by the client.
 * Dataset 1B: Mail file - a list of addresses that were sent this campaign's mailing.
 * Dataset 1C: Holdout file - a list of addresses taken from the same population as those in the mail file, but these addresses were not sent this mailing campaign. Used as a control group when measuring marketing performance.
 * mail_plan: a CSV representation of the Mail Plan used in Section 2.

### Data Dictionary
|Field Name|Definition|
|---|---|
|FullAddress|Primary and secondary address, combined|
|PrimaryAddress||
|SecondaryAddress||
|City||
|State||
|ZipCode||
|OrderRevenue|Dollar value of an order|
|OrderDate|Date order was placed|
|OrderNumber|Unique identifier for an order|
|CustomerID|Unique identifier for a customer|
|FirstTimeOrder|Indicates whether or not this order is the customer's first|
|TestCell|Indicates which test cell the recipient is in|

## Section 1

 1. For this exercise, a valid address is one that begins with a number (0-9). How many rows in the transactions file have a valid address?
 2. Remove those invalid addresses from the transactions data. The transactions file is still not completely clean, however. We need to ensure that every order has a valid date associated with it, and that the `OrderNumber` is a unique integer (if there are duplicates, retain the earliest occurrence of the `OrderNumber`). How many rows are left after cleaning the dataset?

 From here on out, use the "cleaned" transactions file that you produced in question 1.2.

 3. Which state had the most orders placed? How many orders?
 4. How many orders have a secondary address? (i.e. the address is an apartment/suite/etc.)
 5. How many unique customers (based on `CustomerID`) placed an order? What is the average number of orders placed per customer?
 6. The `CustomerID` field has some duplicates. Why do you think this is? Is there a circumstance in which you'd remove duplicates for analysis purposes, and if so, how would you determine which orders to keep?
 7. What other information do you think would be useful to receive from the client in order to analyze the performance of our marketing campaigns? Is there anything that could help for targeting future mailings?

## Section 2

Now that we've cleaned the transactions file, it's time to analyze the mailing campaign!

We can measure the performance of our mailing campaigns by **matching** the addresses between the transactions file and the mail & holdout files (as defined in the "Datasets" section above).

If someone who received a mailing went on to make a purchase for the client, there's a possibility that the marketing influenced that purchasing decision.

Comparing the number of matches between the mailed group and the holdout group allows us to measure a campaign's performance while controlling for any factors outside of that campaign.

Determining which addresses match between two datasets is usually a somewhat complex task, but for this exercise, you just need to see where values of `FullAddress` intersect between the datasets. If the address associated with an order is present in the transactions file, we'd consider that order to be a "match."

### Client Mail Plan

This mail plan describes the campaign. For example, 5,089 addresses received Test Cell 1, a Postcard aimed at New Customer Acquisition, and it cost $5,000 for the client to send this portion of the mailing. The holdout group did not receive the mailing and is used for measuring performance; hence there is no cost associated with it.

|Test Cell|Format|Audience|Quantity Mailed|Total Cost|
|---|---|---|---|---|
|1|Postcard|New Customer Acquisition|5089|5000|
|2|Foldout|New Customer Acquisition|3812|2500|
|3|Foldout|VIP Customers|12|12|
|Holdout|N/A|New Customer Acquisition|2309|N/A|

### Questions
 1. How many "matches" are there between the transactions file and the mail file? Between the transactions file and the holdout file?
 2. The mailing had various different formats and audience targets, as marked by the `TestCell` field. How many matches are there for each `TestCell`?
 3. For each `TestCell`, what percentage of people in the mail and holdout files placed an order?
 4. The mail plan above lists the different Test Cells, the quantity mailed, and the cost to the client. (A CSV version is provided as well, `mail_plan.csv`) Based on this mail plan, create a report or visualization of the campaign's performance that we could share with the client.

Metrics/key performance indicators include, but are not limited to:
 - response rate (number of matched orders divided by quantity)
 - cost per order (CPO) (cost divided by number of matched orders)
 - return on ad spend (ROAS) (revenue from matched orders divided by campaign cost)
 - Breakouts for first time orders, audience target, and so on

 5. For the test cells targeted for New Customer Acquisition, which one do you think is "best" when ignoring the holdout group's performance? Which test cell is "best" when factoring in the holdout? Is the answer still the same? Why or why not?
 6. After reading these results, the client notices the "perfect" performance for Test Cell 3. They determine that since Test Cell 3 used a Foldout format, we should only mail Foldouts going forward. Do you agree?
 7. The client wants to plan a second mailing campaign, using these results as an aid. What are your recommendations to the client on what they should do? Be precise, in one to three sentences.

## Section 3

We are exploring how to build a model that can select the "best" people to target for a client's campaigns, by predicting a person's likelihood to convert, based on the client's transactions data as well as outside data sources.

### Questions

1. Conceptually: What types of additional data might you want to build a model? What types of modeling techniques come to mind as having potential, and what programs and/or software do you think might be applicable or relevant to actually run a model? How would you approach working with datasets containing thousands of records versus datasets containing millions?


