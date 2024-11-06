## Global Electronics Retail

![image](https://github.com/user-attachments/assets/7e06c53a-2341-4f67-9ac4-5437c9c5bdc1)

##

### The following data set consists of various sales-related data for a Global Electronics Retail Company. 

#### The data set is comprised of four tables consisting of Sales, Products, Customers, and Store information.

#### Here is a summary of the tables and their attributes . . . 
![](https://github.com/tanikasuresh/Global-Electronics-Retail-Analysis/blob/main/Miscellaneous/Entity%20Relationship%20Diagram.png)

## Data Cleaning and Preparation

In order to accurately analyze data from four separate tables, it was necessary to combine the data to one table for easier handling. Using the Sales table as the base table, we can build on top of that to include relevant data from other tables. I used VLOOKUP to achieve this by matching Foreign Keys with its Primary Key in another table and adding in the corresponding data.

An example of this is:

```
=VLOOKUP(F2, Customers!A:B, 2)
```
In this example, ```F2``` is the CustomerKey in the Sales table, and it is being matched with the leftmost column in the Customers subset, which is the Primary Key CustomerKey, and obtaining the corresponding value in the second column which is the customers gender.

The ```VLOOKUP``` function will in data from the three other tables into the Sales table including customer Date of Birth, Store Country location, Product Category, and more.

In order to introduce the age demographic into the table, I calculated age by subtracting the year of purchase and date of birth year. To make the analysis a bit more easier, I defined various age groups including the minimum and maximum age within this group.

![image](https://github.com/user-attachments/assets/a07bb1ff-b2ae-4647-9ea7-c3f870cde4b1)

Using this table, I utilized ```VLOOKUP``` to assign the corresponding Age Group depending on the age of the customer at the time of purchase.  

Lastly, in order to analyze profit, it was necessary to calculate the total profit using the following general calculation for every purchase: (`Unit Price` - `Unit Cost`) * `Quantity`

#### With these changes, we can now analyze the sales data using various relevant attributes.

## Profit Analysis

Let's take a look at the profit and the % of Total for various factors . . . 

### Country
![image](https://github.com/user-attachments/assets/7badf0c9-1006-44df-868b-fab61803915a)

### Category
![image](https://github.com/user-attachments/assets/83bb4236-1c9f-49ff-b9ab-1caee42c3f7c)

### Year
![image](https://github.com/user-attachments/assets/c777638e-5cc2-400c-bb35-44437b5404e8)

Here's one example of the ```SUMIF``` function used to calculate the total profit:

```=SUMIF(Sales_Edited!O:O,A19,Sales_Edited!S:S)```

#### Here, we can see that sales in the United States make up the largest portion of sales in all countries. Adding on, the company generates the most revenue from the Computers category. Lastly, profit has increased from 2020 to 2023, with the greatest annual profit during 2023. Most notably, the company experienced the greatest increase in profit in 2022. 

## Customer Analysis

Let's take a look at the number of customers that have shopped at the company.

![image](https://github.com/user-attachments/assets/036c3324-37d0-43d0-b1ea-53eced7cdd62)

To calculate the number of individual shoppers for each year, I used a combination of Excel functions to narrow down the data for the specific year and country, and counting the number of the unique CustomerKey.

For example:

```=ROWS(UNIQUE(CHOOSECOLS(FILTER(Sales_Edited!D$2:K$50647,(Sales_Edited!D$2:D$50647=B33)*(Sales_Edited!K$2:K$50647=A$31)),3)))```

Now let's look at the number of customers that shopped more than once during each year.
	
![image](https://github.com/user-attachments/assets/78320200-3bf0-4d5d-a3a9-9a994a1d99bf)

To calculate the number of returning customers for each year, I first found the number of shoppers that only shopped exactly one time using the ```UNIQUE``` function and subtracted that value from the number of individual shoppers found in the previous table.

For example:

```=C34-ROWS(UNIQUE(CHOOSECOLS(FILTER(Sales_Edited!D$2:K$50647,(Sales_Edited!D$2:D$50647=A41)),3),,TRUE))```

#### Here, we see that the number of unique customers per year has increased from 2020 to 2023. Also, the number of customers that shopped at the company more than once per year has also increased from 2020 to 2023.

#### Moving on to customer demographics . . . 

![image](https://github.com/user-attachments/assets/492b71f6-b1bb-48a7-80a7-318c7ea03e9d)

Here is an example of the functions used to calculate # of Orders for each gender:
```=ROWS(UNIQUE(CHOOSECOLS(FILTER(Sales_Edited!A:H,Sales_Edited!H:H="Male"),1)))```

Here is a sample calculation to find the average profit:
```=AVERAGE(CHOOSECOLS(FILTER(Sales_Edited!H:S,Sales_Edited!H:H="Male"),-1))```

#### Here, we see Male and Female customers make up almost an equal amount of orders. Adding on, and male customers spend slightly more on average.

#### Also, the largest portion of customers are in the 65+ age group, but the 25-34 age group spends the most on average.

## Product Analysis
![image](https://github.com/user-attachments/assets/096d1976-9fbc-4023-a4d7-9c85b0f2c2a5)

#### We can see from the tables that the company sells the most products to customers in the United States, with Online orders being the next. To break it down based on product category, the Computers category sells the most products, with Cell Phones coming in second.

#### However, we can break down those categories further into various subcategories for products to see that the most sold subcategory is Movie DVDs.

## Dashboard

### The dashboard at the top reflects a few of the more interesting and relevant data like the total number of unique and returning customers, profit and products sold for different factors like Country and Category, as well as a visual representation of profit for every month of the four years of operation.

### What is truly exciting about the dashboard is that it is dynamic and fully interactive! There are slicers for each of the three portions to help narrow down the data to relevant features like year, gender, age group, category and country. This makes it much easier to track changes in certain demographics and markets for a better understanding of the Global Electronics Retail Company's performance.


















