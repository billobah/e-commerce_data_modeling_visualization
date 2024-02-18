# Modeling E-Commerce data using Python and Postgres and Visualizing insights using Power BI

This project shows how to build a data model using Python and stored it in a PostgreSQL database, as our Data Warehouse.

Then, we will answer to some business questions using visualizations from Power BI.

## 1. The Data

Data are downloaded from [Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce/).

## 2. Reading the data

We will use the pandas library to read the data, by importing it first.

```python
customers = pd.read_csv("dataset/customers.csv")
order_items = pd.read_csv("dataset/order_items.csv")
order_payments = pd.read_csv("dataset/order_payments.csv")
orders = pd.read_csv("dataset/orders.csv")
products = pd.read_csv("dataset/products.csv")
sellers = pd.read_csv("dataset/sellers.csv")
```

## 3. Presenting the schema of our tables

Here is the schema of our tables, and the relationship between our tables :

![ecommerce_diagra](images/ecommerce_diagram.png)

## 4. Defining the use case of the data

To know what data to put into the tables of our data model, we need to know what the data is going to be used for. This part is usually done by having a conversation with the users of the data (analysts, managers, scientists, etc). Once we know what will be the most relevant data for our business use case, then we can create a data model for that required data.

Let’s create a data model that supports the following analysis:

* What places contributed the most/least to product sales?
* Which seller sold the most/least products?
* Best and worst performing products.
* Date for everything.

## 5. Creating a star schema

Here is our data model with tables to be loaded in our Data Warehouse:

![ecommerce_star_schema](images/ecommerce_star_schema.png)

## 6. Creating the data model tables from the existing tables

### 6.1 Creating the fact_transactions table

Let’s start with the fact table. From the default schema we can see that the columns that we need are distributed among different tables, so first we need to join those tables. In two steps, we will join **orders**, **order_payments** and **order_items** tables on *order_id* key to produce a unique table.

### 6.2 Creating the dim_customers table

We will extract from the **customers** table the needed columns: *customer_id*, *customer_city*, *customer_state*.

### 6.3 Creating the dim_products table

We will extract from the **products** table the needed columns: *product_id* and *product_category_name*.

### 6.4 Creating the dim_sellers table

We will extract from the **sellers** table the needed columns: *seller_id*, *seller_city*, *seller_state*.

### 6.5 Creating the dim_date table

First, we have to extract the *order_id* and the *order_purchase_timestamp* columns from the **orders** table.

Second, We have to convert *order_purchase_timestamp* column into the datetime format.

Last, We have to extract the month and year from the *order_purchase_timestamp* datetime column.

## 7. Creating a PostgreSQL Database and connecting to it

To connect to our PostgreSQL database from Python, we will use the psycopg2 library.

## 8. Creating our model tables in the database

We will write SQL queries to create our table and execute it.

## 9. Inserting data into database tables

We will write a SQL query to insert rows into the tables. We read each row from the dataframe and insert it into the corresponding table in the ***ecommerce*** database.
