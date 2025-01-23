## Project Overview
A certain firm in the United States is focused on distributing 15 candy products to customers across the country and Canada. The company has 5 factories and its products are classified under 3 divisions namely; chocolate, sugar, and others. In this analysis, the goal is to examine the business sales, profits, and trends across the 4-year period starting from 2021 to 2024. In the end, I will make some recommendations based on the insights derived from querying the data.

<img width="546" alt="Wonka 2" src="https://github.com/user-attachments/assets/a77891be-3e01-4f71-afe4-30be6a38039f" />
<img width="544" alt="Wonka 3" src="https://github.com/user-attachments/assets/e13e6cff-a0fd-4a9e-bc47-faa15a7d18e4" />
<img width="548" alt="Wonka 4" src="https://github.com/user-attachments/assets/d627bdbe-468d-4789-beee-ba47d70c2318" />

Link to interact with the dashboard: http://bit.ly/4hjCtFX

## Data Source
The source of this data is Maven Analytics. The dataset can be accessed in this [link](https://mavenanalytics.io/data-playground?order=date_added%2Cdesc&search=us%20candy).

## Tools
The primary tools used for cleaning, analyzing and visualizing the insights from this dataset are Excel and Power BI.

## Data Cleaning
Cleaning this dataset required;
 + a. Checking for and removing null values.
 + b. Using the Power Query ETL platform to format values correctly and insert the right column names.
 + c. Modelling relationships to relate tables using the appropriate primary and foreign keys.

## Product Analysis
The following questions were analyzed from the dataset:
+ How are products classified by factory, division, and ship mode?
+ How many units of each product were sold per year and month?
+ How much was made in sales for unique candy products by year and month?

## Deep Insights
+ How much did each factory make?
+ How much sales were made by region?
+ How many transactions did each region and state make?
+ What was the profit by year?
+ How did the highest grossing product compare to the lowest grossing product?
+ How did the highest grossing state compare to the lowest?

## Trends Analysis
+ Classify states by total sales and year on year percentage.
+ Show the relationship between sales and profit percentage change across months.
+ What is the month on month percent change for sales and units sold?
  
## Observations
+ 2024 made the highest profit and Lots O'Nuts factory made the most sales while Sugar Shack made the lowest.
+ The pacific region ordered most candy products with California topping the list.
+ Overall, the months of November and December recorded the highest profits and sales.
+ The peak positive change in profit and sales occurred in the month of March while January experienced the lowest negative change.
+ Of the 39000 units of candy sold within this period, $140,000 was generated in sales, and the company realized $93,000 in profits.

## DAX Calculations
```dax

1. PreviousYearSales = 
CALCULATE(
    SUM('Candy_sales (2)'[Sales]),
    DATEADD('Calendar'[Date], -1, YEAR)
)

2. YOY % = 
DIVIDE(
    SUM('Candy_sales (2)'[Sales]) - [PreviousYearSales],
    [PreviousYearSales],
    0
) * 100

3. Total profit = SUM('Candy_sales (2)'[Gross Profit])

4. Total sales = SUM('Candy_sales (2)'[Sales])

5. PreviousMonthSales = 
CALCULATE(
    SUM('Candy_sales (2)'[Sales]),
    DATEADD('Calendar'[Date], -1, MONTH)
)

6. MoM Sales % Change = 
DIVIDE(
    [MoMSalesChange], 
    [PreviousMonthSales], 
    0
) * 100

7. PreviousMonthUnitsSold = 
CALCULATE(
    SUM('Candy_sales (2)'[Units]),
    DATEADD('Calendar'[Date], -1, MONTH)
)

8. MoM Units Sold % Change = 
DIVIDE(
    [MoMUnitsSoldChange], 
    [PreviousMonthUnitsSold], 
    0
) * 100

9. Total profit = SUM('Candy_sales (2)'[Gross Profit])

10. MoMProfitPercentageChange = 
DIVIDE(
    [MoMProfitChange], 
    [PreviousMonthProfit], 
    0
) * 100
