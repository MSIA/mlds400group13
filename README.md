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

**trnsact:** We set the data type of SKU, STORE, REGISTER, TRANNUM, SEQ, QUANTITY, INTERID, and MIC as bigint; SALEDATE as date; STYPE as text, ORGGPRICE, SPRICE, and AMT as numeric; and unknown (last column) as integer type. And we also imported the data into postgresql.

**strinfo:** The data type of STORE, ZIP, and unknown columns are integer, CITY and STATE are character varying. We successfully imported the data into postgresql.

To do list: clean the data, clearly there are some columns that have confusing attributes. Also, remove the last column(unknown) for each dataset because the last column is meaningless. Connect postgresql to python and start to do EDA.

## Oct 27

We have successfully grant access to all tables through Postgresql and we clean data in skuinfo. We dropped the last column for all tables. 

To do list: we want to do EDA in python jupyter notebook as Alice taught in class. We want to decide a research topic and start the project proposal first.
