## Scenario

As a Junior Data Analyst, you have been tasked with analyzing a quarter's worth of orders from a fictitious restaurant that serves international cuisine. The dataset includes information on the date and time of each order, the items ordered, and additional details such as the type, name, and price of the items.

## Data Source and Details

The restaurant order dataset was provided by Maven Analytics, along with business questions to address.

The dataset consists of two tables:

- **Menu Items Table** - Contains 4 columns.  

- **Order Details Table** - Contains 5 columns.  

## Objectives

### 1.) Explore the Menu Items Table

- Determine the number of rows in the table
- Identify the least and most expensive items
- Analyze item prices within each category

### 2.) Explore the Order Details Table

- Identify the date range of the orders
- Calculate the number of items within each order
- Find the orders with the highest number of items

### 3.) Analyze Customer Behavior

- Combine the Menu Items and Order Details tables
- Determine the least and most ordered categories
- Examine the details of the highest-spend orders

## Tools Used

- **IDE:** Visual Studio Code
- **Database:** PostgreSQL
- **Extensions and Drivers:** SQLTools

## Data Processing (ETL)

- Downloaded compressed restaurant order file from Maven Analytics
- Used the create_restaurant_db.sql file to create an SQL database and the restaurant order tables that I used for the analysis.

### Creating Database

```
CREATE DATABASE restaurant_order_analysis;
```

### Table Structure for the order_details Table

```
CREATE TABLE order_details (
  order_details_id SMALLINT NOT NULL,
  order_id SMALLINT NOT NULL,
  order_date DATE,
  order_time TIME,
  item_id SMALLINT,
  PRIMARY KEY (order_details_id)
);
```

### Table Structure for the menu_items Table

```
CREATE TABLE menu_items (
  menu_item_id SMALLINT NOT NULL,
  item_name VARCHAR(45),
  category VARCHAR(45),
  price DECIMAL(5,2),
  PRIMARY KEY (menu_item_id)
);
```

### Insert Data into the order_details Table

*Too Big to Post here. Get the dataset.*

### Insert Data into the menu_items Table

```
INSERT INTO menu_items VALUES (101, 'Hamburger', 'American', 12.95),
(102, 'Cheeseburger', 'American', 13.95),
(103, 'Hot Dog', 'American', 9),
(104, 'Veggie Burger', 'American', 10.5),
(105, 'Mac & Cheese', 'American', 7),
(106, 'French Fries', 'American', 7),
(107, 'Orange Chicken', 'Asian', 16.5),
(108, 'Tofu Pad Thai', 'Asian', 14.5),
(109, 'Korean Beef Bowl', 'Asian', 17.95),
(110, 'Pork Ramen', 'Asian', 17.95),
(111, 'California Roll', 'Asian', 11.95),
(112, 'Salmon Roll', 'Asian', 14.95),
(113, 'Edamame', 'Asian', 5),
(114, 'Potstickers', 'Asian', 9),
(115, 'Chicken Tacos', 'Mexican', 11.95),
(116, 'Steak Tacos', 'Mexican', 13.95),
(117, 'Chicken Burrito', 'Mexican', 12.95),
(118, 'Steak Burrito', 'Mexican', 14.95),
(119, 'Chicken Torta', 'Mexican', 11.95),
(120, 'Steak Torta', 'Mexican', 13.95),
(121, 'Cheese Quesadillas', 'Mexican', 10.5),
(122, 'Chips & Salsa', 'Mexican', 7),
(123, 'Chips & Guacamole', 'Mexican', 9),
(124, 'Spaghetti', 'Italian', 14.5),
(125, 'Spaghetti & Meatballs', 'Italian', 17.95),
(126, 'Fettuccine Alfredo', 'Italian', 14.5),
(127, 'Meat Lasagna', 'Italian', 17.95),
(128, 'Cheese Lasagna', 'Italian', 15.5),
(129, 'Mushroom Ravioli', 'Italian', 15.5),
(130, 'Shrimp Scampi', 'Italian', 19.95),
(131, 'Chicken Parmesan', 'Italian', 17.95),
(132, 'Eggplant Parmesan', 'Italian', 16.95);
```

## Restaurant Order Analysis and Answering Business Questions

Analyze order data to identify the most and least popular menu items and types of cuisine.

### 1.) View the menu_items table and write a query to find the number of items on the menu

**a.) View the menu_items table**

```
SELECT
    *
FROM
    menu_items;
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/42508782-3a07-433f-afd8-3b06fad59775.jpg)

This table has 4 columns;

- menu_item_id: Unique ID of a menu item
- item_name: Name of a menu item
- category: Category or type of cuisine of the menu item
- price: Price of the menu item (US Dollars $)

**b.) Find the number of items on the menu**

```
SELECT
    COUNT(menu_item_id) AS num_of_items_on_menu
FROM
    menu_items;
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/4ed283f1-1ff6-45d2-8520-41452dbda8f9.jpg)

There are 32 items on the menu.

### 2.) What are the least and most expensive items on the menu?

**a.) Least Expensive Item on the Menu**

```
SELECT
    item_name,
    price
FROM
    menu_items
ORDER BY
    price;
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/d7b5aff7-82ec-4694-a110-7cf84530dc71.jpg)

Least Expensive Item: Edamame with a price of $5.00

**b.) Most Expensive Item on the menu**

```
SELECT
    item_name,
    price
FROM
    menu_items
ORDER BY
    price DESC;
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/b4f0f6f5-d567-421e-b9d2-ea2a362ff6b7.jpg)

Most Expensive Item: Shrimp Scampi with a price of $19.95

### 3.) How many Italian dishes are on the menu? What are the least and most expensive Italian dishes on the menu?

**a.) How many Italian dishes are on the menu?**

```
SELECT
    COUNT(menu_item_id)
FROM
    menu_items
WHERE
    category = 'Italian';
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/a8eb1ca1-e013-44d5-9800-60059dce6d8a.jpg)

There are 9 Italian dishes on the menu.

**b.) What is the least expensive Italian dishes on the menu?**

```
SELECT
	item_name,
	price
FROM
	menu_items
WHERE
	category = 'Italian'
ORDER BY
	price;
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/36b5605f-e4b4-4170-b949-a25d6e10c53a.jpg)

The least expensive Italian dish on the menu is Fettuccine Alfredo with a price of $14.50

**c.) What is the most expensive Italian dishes on the menu?**

```
SELECT
	item_name,
	price
FROM
	menu_items
WHERE
	category = 'Italian'
ORDER BY
	price DESC;
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/afef240f-820f-40a7-a07a-f7cc5f245cb1.jpg)

The most expensive Italian dish on the menu is Shrimp Scampi with a price of $19.95

### 4.) How many dishes are in each category? What is the average dish price within each category?

**a.) How many dishes are in each category?**

```
SELECT
	category,
	COUNT(menu_item_id) AS num_of_dishes_per_category
FROM
	menu_items
GROUP BY
	category
ORDER BY
	num_of_dishes_per_category DESC;
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/9679c42c-465e-4cf4-9106-002cf88c4b2c.jpg)

There are 4 categories;

- Mexican: 9 dishes
- Italian: 9 dishes
- Asian: 8 dishes
- American: 6 dishes.

**b.) What is the average dish price within each category?**

```
SELECT
	category,
	ROUND(AVG(price), 2) AS average_dish_price
FROM
	menu_items
GROUP BY
	category
ORDER BY
	average_dish_price DESC;
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/7afeb789-261d-48d8-8ee7-028cc26b7c2e.jpg)

The average dish prices within each category are as follows;

- Italian: $16.75
- Asian: $13.48
- Mexican: $11.80
- American: $10.07

### 5.) View the order_details table. What is the date range of the table?

**a.) View the order_details table**

```
SELECT
	*
FROM
	order_details;
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/ef190114-6145-4c9f-ac25-c10c783f847a.jpg)

This table has 4 columns;

- order_details_id: Unique ID of an item in an order
- order_id: ID of an order
- order_date: Date an order was put in (MM/DD/YY)
- order_time: Time an order was put in (HH:MM:SS AM/PM)
- item_id: Matches the menu_item_id in the menu_items table

**b.) What is the date range of the table?**

```
SELECT
	MIN(order_date) AS start_date,
	MAX(order_date) AS end_date
FROM
	order_details;
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/cf6b6739-e724-4cfd-9609-aa73c410f09b.jpg)

The Date range of the table is January 1st, 2023 to March 31st, 2023.

### 6.) How many orders were made within this date range? How many items were ordered within this date range?

**a.) How many orders were made within this date range?**

```
SELECT
	COUNT(DISTINCT(order_id)) AS total_orders
FROM
	order_details;
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/e4e35c73-b14f-4848-9a67-b10dbf1955b1.jpg)

5,370 orders were made within the table's date range.

**b.) How many items were ordered within this date range?**

```
SELECT
	COUNT(order_details_id) AS total_ordered_items
FROM
	order_details;
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/c0fc0530-d8a2-4961-8fb8-3fb7098afaf1.jpg)

12,234 items were ordered within this date range.

### 7.) Which orders had the most number of items?

```
SELECT
	order_id,
	COUNT(order_details_id) AS total_ordered_items
FROM
	order_details
GROUP BY
	order_id
ORDER BY
	total_ordered_items DESC;
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/7aefdcd7-7723-4b24-b53d-b1f5175be72d.jpg)

The highest number of items ordered is 14 and 8 orders have this number of items ordered.

Their Order ID is;

- 4305
- 4482
- 2675
- 443
- 1957
- 330
- 3473
- 440

### 8.) How many orders had more than 12 items?

```
SELECT
	order_id,
	COUNT(order_details_id) AS total_ordered_items
FROM
	order_details
GROUP BY
	order_id
HAVING
	COUNT(order_details_id) > 12
ORDER BY
	total_ordered_items DESC;
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/a8782dd5-702f-4b25-87dc-ac96576f28ba.jpg)

There are 23 orders with more than 12 ordered items.

### 9.) Combine the menu_items and order_details tables into a single table

```
SELECT
	*
FROM
	order_details
LEFT JOIN
	menu_items
ON
	item_id = menu_item_id;
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/3b5f432c-8a65-4138-8af7-ff923473c155.jpg)

### 10.) What were the least and most ordered items? What categories were they in?

**a.) What is the most ordered item and its category?**

```
SELECT
	item_name,
	category,
	COUNT(order_details_id) AS number_of_items_ordered
FROM
	order_details
LEFT JOIN
	menu_items
ON
	item_id = menu_item_id
GROUP BY
	item_name,
	category
ORDER BY
	number_of_items_ordered DESC;
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/b2ded061-bc42-4354-91dd-c379b3cb245e.jpg)

The most ordered item is Hamburger, ordered 622 times and its category is American

**b.) What is the least ordered item and its category?**

```
SELECT
	item_name,
	category,
	COUNT(order_details_id) AS number_of_items_ordered
FROM
	order_details
	LEFT JOIN
	menu_items
ON
	item_id = menu_item_id
GROUP BY
	item_name,
	category
ORDER BY
	number_of_items_ordered;
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/e52b5ee7-58c0-40c9-a06d-9f741f2a7362.jpg)

The least ordered item is Chicken Tacos, ordered 123 times and its category is Mexican

### 11.) What were the top 5 orders that spent the most money?

```
SELECT
	order_details.order_id,
	COALESCE(SUM(menu_items.price),0) AS total_price
FROM
	order_details
LEFT JOIN
	menu_items
ON
	item_id = menu_item_id
GROUP BY
	order_details.order_id
ORDER BY
	total_price DESC
LIMIT
	5;
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/1e77e6d0-2e4f-4f3c-83e2-b2f22effc104.jpg)

The top 5 orders (Order ID) with the most amount spent are;

- 440: $192.15
- 2075: $191.15
- 1957: $190.10
- 330: $189.70
- 2675: $185.10

### 12.) View the details of the highest spend order. Which specific items were purchased?

```
SELECT
	order_details.order_id,
	menu_items.category,
	menu_items.item_name
FROM
	order_details
LEFT JOIN
	menu_items
ON
	order_details.item_id = menu_items.menu_item_id
WHERE
	order_details.order_id = 440
GROUP BY
	order_details.order_id,
	menu_items.category,
	menu_items.item_name;
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/53669763-9bc2-4422-b6a7-870bc4a4d177.jpg)

- The highest spend order is Order ID 440 and 12 items were ordered. The items ordered and their category are in the image above.
- 6 of the items are from the Italian category while the American, Mexican, and Asian categories have 2 items each.

### 13.) BONUS: View the details of the top 5 highest spend orders

```
SELECT
	order_details.order_id,
	menu_items.category,
	COUNT(item_id) AS number_of_orders
FROM
	order_details
LEFT JOIN
	menu_items
ON
	order_details.item_id = menu_items.menu_item_id
WHERE
	order_details.order_id IN (440, 2075, 1957, 330, 2675)
GROUP BY
	order_details.order_id,
	menu_items.category
ORDER BY
	number_of_orders DESC;
```

![undefined](https://mavenanalyticsio-upload-bucket-prod.s3.us-west-2.amazonaws.com/209678157/projects/2d39189c-e4cb-4e88-a6cf-911ebc12b99d.jpg)

The most ordered dish category is Italian. Followed by Asian and Mexican.

## Insight Gained

- The most ordered item is Hamburger which is an American dish
- The least ordered item is Chicken Tacos, a Mexican dish
- 6 of the most ordered items from the most expensive orders are Italian Dishes
- At $16.75, Italian has the highest average dish price

## Recommendation

1.) Add more Italian dishes to the menu items. Not just because they are the most ordered but also because they have the highest average dish price which means they bring in more money to the restaurant than other item categories.

2.) American dishes have the lowest average dish price at $10.07 but an item in this category (Hamburger) is the most ordered item. So, this category should be kept.

3.) At $11.80, Mexican dishes have slightly higher average dish price than American but they also have some of the least ordered items by the top spenders. Further analysis should be done to determine the Gross profit of this category and if negative, the category should be retired.
