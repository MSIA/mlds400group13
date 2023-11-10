# mlds400group13
MLDS400 Group 13

# MLDS400 - Final Project

## Oct 13 

### Deptinfo: 
Has 3 columns: DEPT, DEPTDESC, 0 and 59 rows
This table shows the department where the stock items belong(DEPT) and the corresponding description of the department(DEPTDESC). But there are two rows’ descriptions of the department that only have number values instead of the company. DEPTDESC is character(string) type and DEPT is in numeric type. The third column may have no meaning. 

### Skstinfo:
Has 5 columns and 39,230,146 rows. 
Columns are SKU, STORE, COST, RETAIL, 0.
This dataset shows the unit number of stock items for each store, and their corresponding cost and retail price of the stock item. All columns are in numeric type. The mean cost is $24.16, minimum cost is $0, and the maximum is $2700. The retail price ranges from $0 to $6017 and the mean is $43.33. The last column has no meaning. 

### Skuinfo:
Has 11 columns and 1,564,177 rows. 
Columns: SKU, DEPT, CLASSID, UPC, STYLE, COLOR, SIZE, PACKSIZE, VENDOR, BRAND 
This table describes each stock item’s details, including the department the stock item belongs to, stock item classification, universal product code, color, size, quantity of item per pack, vendor number, and brand name. The SKU, CLASSID, STYLE, COLOR, SIZE, PACKSIZE, VENDOR, and BRAND are in character(string) type. DEPT and UPC are in numeric type. The last column does not have meaning.

### Strinfo:
Has 5 columns and 452 rows
Columns: STORE, CITY, STATE, ZIP, 0
This table describes the detailed information about the store, including store number, city where the store is located, state where the store is located, and zip code. The CITY and STATE variables are in character(string) type while other variables are in numeric type. The last column has no meaning. 

### Trnsact:
Has 14 columns and 120,916,896 rows
This table is about the transaction history of Dillard’s stores. It includes Total amount of the transaction charge to the customer, internal ID, Master Item code, Original price of the time stock, Item quantity of the transaction, Register number of the current transaction, Sale Date, Sequence number, Stock keeping unit number of the stock item, Sale price of the item stock, Store number, Type of the transaction, Transaction code. And there is an unknown column that has no meaning. Will drop it. The minimum store number is 102, and Sale Price and  Total amount of transaction charge to the customer has the same summary result . Sale date has 71025222 rows  that are not in factorized date format.

**To do list:** import data into sql server and order the columns accordingly.


## Oct 20 

All members successfully accessed the sql server and we uploaded all data into tables in postgresql. We specified every string column as "character varying" and every digit as "bigint" to ensure it can store big data. We discovered several extra column and we imported as "unknown"

**skstinfo:** it only has one extra unknown column.

**skuinfo:** the order is confusing, the second column has four digits only which aligns with "classid", however, we couldn't make sure whether the third column is classid or department.

**deptinfo:** We set the data type of DEPT column as integer, DEPTDESC as character varying, and the unknow columns as integer. And we also imported the data into postgresql.

**trnsact:** We set the data type of SKU, STORE, REGISTER, TRANNUM, SEQ, QUANTITY, INTERID, and MIC as bigint; SALEDATE as date; STYPE as text, ORGPRICE, SPRICE, and AMT as numeric; and unknown (last column) as integer type. And we also imported the data into postgresql.

**strinfo:** The data type of STORE, ZIP, and unknown columns are integer, CITY and STATE are character varying. We successfully imported the data into postgresql.

To do list: clean the data, clearly there are some columns that have confusing attributes. Also, remove the last column(unknown) for each dataset because the last column is meaningless. Connect postgresql to python and start to do EDA.

## Oct 27

We have successfully grant access to all tables through Postgresql and we clean data in skuinfo. 

Clean Data: We dropped the last column for all tables. 

**strinfo:** We check the number of appearances of each state and city names, find the percentage breakdowns accordingly to get a sense of the distribution of stores. We also find the state and city with the highest number of stores.

**trnsact:** We selected about 100000 rows of data to do EDA. We checked how the original and sale prices changed over time using a line plot. From the line plot, we discovered that the original prices of the stock were consistently higher than the sale prices. Significantly large differences were in February 2005 and August 2005. The distribution of original prices and sale prices are skewed to the right. From the correlation matrix plot, we also found out that AMT(Total amount of the transaction charge to the customer) and sale price have highly positive correlation with original price.

**deptinfo:** This table needs to combine with other tables to see the department descriptions.

To do list: we want to do more EDA in python jupyter notebook as Alice taught in class. We also want to decide a research topic and start the project proposal first.

## Nov 3
In the current week, we have undertaken an exploratory phase aimed at identifying promising research topics. Our objective is to rigorously evaluate the suitability of these topics through the application of various machine learning methodologies. The primary focus of our efforts is to assess the credibility of these methodologies and their ability to provide comprehensive and explanatory results.

**Topics:** 
1. Predict the future sales volume and price of a specific item in a particular store, or based on its brand (or department), in order to provide stocking and pricing strategies. (retail demand forecasting research question)
2. Seasonality of the store sales in different state saledate, supply chain management, in different type of product (consumer behavior research question)
3. Return and purchase rate of different products-binary (customer satisfaction research question)
4. Inflation trends through years in stores by different products-original price/sales price (economical research question)

**EDA for Topic 1:**
Select the store that has the highest profit in each state, then draw a graph to show the discounts, sales price, or quantity of each item.  

Challenges: trnsact table is too large so it takes a long time to import into python.

To do list: Do more EDA or joining table based on each topic and test them out to see which topics work the best.

### Nov 10
Continue exploreing data from each table, trying to join transaction tables with sampling method.
Examine the relationship between brand and state and trying to predict the sales in the future

***Topic testing in predicting the sale price, discount, and quantity for each brand in the future:*** <br>
**Join table:** We joined the four tables together. 
**Feature Engineering:** Created a profit variable by subtracting COST from SPRICE (Sell price), and discount variable by subtracting SPRICE from ORGPRICE. These two variables can help us have a better understanding how each store is performing in terms of profitability and pricing strategy. We then groupby STATE, STORE, and BRAND, then select the SPRICCE, PROFIT, QUANTITY, and discount variable. Also, we created new variables SPRICE_per_Unit, discount_per_Unit, PROFIT_per_Unit. 
**EDA:** 
1. Summary statistics: SPRICE, PROFIT, QUANTITY, and discount all have very extreme values, such as 166285.50 and -4167.74.
2. Distribution plot: Lots of data point around 0.
3. Bar Plot: Top brands by sale price: CLINIQUE, POLO FAS, LANCOME, LIZ CLAI, and CABERNET are top 5 brands have highest total sale price. AR, NV, LA, AZ, and TX state have highest total sale price. 8402, 9806, 504, 2707 have highest total sale price. Top brands by total profit: CLINIQUE, LANCOME, CABERNET, POLO FAS, and ROUNDTRE. Top states have high total profit are TX, FL, LA, AZ, and OH. Top stores have highest profit are 8402, 9806, 504, 2707, and 1607. Top brands with high total discount are POLO FAS, LIZ CLAI, HART SCH, EMMA JAM, and ROUNDTRE. Top states are TX, FL, AZ, LA, and OH. Top stores are 2203, 8402, 9103, 2109, and 1509. The top brands with most sale quantity are CLINIQUE, CABERNET, LANCOME, LIZ CLAI, and ROUNDTRE. 
4. Scatterplot: As sale price increases, profit increases. As quantity increases, sale price and profit increases.
**Model:** For the modeling, we tried linear regression, gradient boosting regressor, and random forest regressor for SPRICE, discount, and QUANTITY. Among all three models, random forest regressor performs the best. R-squared is 0.9764 in predicting SPRICE, 0.9557 in predicting discount, and 0.9858 in predicting quantity. However, the mean square error are really large for all models since there are many extreme values. We may need to fix this problem by either using sale price per unit and discount per unit or look for other ways. 

To do list: decide on final project and work on data manipulation and modeling.

