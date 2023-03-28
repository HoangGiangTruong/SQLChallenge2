# SQL Challenge 2
![image](https://user-images.githubusercontent.com/100246099/228257075-80ba2553-76f1-4fa2-95da-2c1ab362afb9.png)

You can find the case study here: https://8weeksqlchallenge.com/case-study-2/

## Introduction

Did you know that over 115 million kilograms of pizza is consumed daily worldwide??? (Well according to Wikipedia anyway…)

Danny was scrolling through his Instagram feed when something really caught his eye - “80s Retro Styling and Pizza Is The Future!”

Danny was sold on the idea, but he knew that pizza alone was not going to help him get seed funding to expand his new Pizza Empire - so he had one more genius idea to combine with it - he was going to Uberize it - and so Pizza Runner was launched!

Danny started by recruiting “runners” to deliver fresh pizza from Pizza Runner Headquarters (otherwise known as Danny’s house) and also maxed out his credit card to pay freelance developers to build a mobile app to accept orders from customers.

## Data Structure
Because Danny had a few years of experience as a data scientist - he was very aware that data collection was going to be critical for his business’ growth.

He has prepared for us an entity relationship diagram of his database design but requires further assistance to clean his data and apply some basic calculations so he can better direct his runners and optimise Pizza Runner’s operations.

All datasets exist within the pizza_runner database schema - be sure to include this reference within your SQL scripts as you start exploring the data and answering the case study questions.

![image](https://user-images.githubusercontent.com/100246099/228262793-731c4d7c-9dd1-4b88-ad01-67c26c2c1cf4.png)


DROP TABLE IF EXISTS runners;
CREATE TABLE runners (
  "runner_id" INTEGER,
  "registration_date" DATE
);
INSERT INTO runners
  ("runner_id", "registration_date")
VALUES
  (1, '2021-01-01'),
  (2, '2021-01-03'),
  (3, '2021-01-08'),
  (4, '2021-01-15');

````sql
DROP TABLE IF EXISTS customer_orders;
CREATE TABLE customer_orders (
  "order_id" INTEGER,
  "customer_id" INTEGER,
  "pizza_id" INTEGER,
  "exclusions" VARCHAR(4),
  "extras" VARCHAR(4),
  "order_time" DATETIME
);
````
````sql
INSERT INTO customer_orders
  ("order_id", "customer_id", "pizza_id", "exclusions", "extras", "order_time")
VALUES
  ('1', '101', '1', '', '', '2020-01-01 18:05:02'),
  ('2', '101', '1', '', '', '2020-01-01 19:00:52'),
  ('3', '102', '1', '', '', '2020-01-02 23:51:23'),
  ('3', '102', '2', '', NULL, '2020-01-02 23:51:23'),
  ('4', '103', '1', '4', '', '2020-01-04 13:23:46'),
  ('4', '103', '1', '4', '', '2020-01-04 13:23:46'),
  ('4', '103', '2', '4', '', '2020-01-04 13:23:46'),
  ('5', '104', '1', 'null', '1', '2020-01-08 21:00:29'),
  ('6', '101', '2', 'null', 'null', '2020-01-08 21:03:13'),
  ('7', '105', '2', 'null', '1', '2020-01-08 21:20:29'),
  ('8', '102', '1', 'null', 'null', '2020-01-09 23:54:33'),
  ('9', '103', '1', '4', '1, 5', '2020-01-10 11:22:59'),
  ('10', '104', '1', 'null', 'null', '2020-01-11 18:34:49'),
  ('10', '104', '1', '2, 6', '1, 4', '2020-01-11 18:34:49');
````
````sql
DROP TABLE IF EXISTS runner_orders;
CREATE TABLE runner_orders (
  "order_id" INTEGER,
  "runner_id" INTEGER,
  "pickup_time" VARCHAR(19),
  "distance" VARCHAR(7),
  "duration" VARCHAR(10),
  "cancellation" VARCHAR(23)
);
````
````sql
INSERT INTO runner_orders
  ("order_id", "runner_id", "pickup_time", "distance", "duration", "cancellation")
VALUES
  ('1', '1', '2020-01-01 18:15:34', '20km', '32 minutes', ''),
  ('2', '1', '2020-01-01 19:10:54', '20km', '27 minutes', ''),
  ('3', '1', '2020-01-03 00:12:37', '13.4km', '20 mins', NULL),
  ('4', '2', '2020-01-04 13:53:03', '23.4', '40', NULL),
  ('5', '3', '2020-01-08 21:10:57', '10', '15', NULL),
  ('6', '3', 'null', 'null', 'null', 'Restaurant Cancellation'),
  ('7', '2', '2020-01-08 21:30:45', '25km', '25mins', 'null'),
  ('8', '2', '2020-01-10 00:15:02', '23.4 km', '15 minute', 'null'),
  ('9', '2', 'null', 'null', 'null', 'Customer Cancellation'),
  ('10', '1', '2020-01-11 18:50:20', '10km', '10minutes', 'null');
````
````sql
DROP TABLE IF EXISTS pizza_names;
CREATE TABLE pizza_names (
  "pizza_id" INTEGER,
  "pizza_name" TEXT
);
INSERT INTO pizza_names
  ("pizza_id", "pizza_name")
VALUES
  (1, 'Meatlovers'),
  (2, 'Vegetarian');
````
````sql
DROP TABLE IF EXISTS pizza_recipes;
CREATE TABLE pizza_recipes (
  "pizza_id" INTEGER,
  "toppings" TEXT
);
INSERT INTO pizza_recipes
  ("pizza_id", "toppings")
VALUES
  (1, '1, 2, 3, 4, 5, 6, 8, 10'),
  (2, '4, 6, 7, 9, 11, 12');
````
````sql
DROP TABLE IF EXISTS pizza_toppings;
CREATE TABLE pizza_toppings (
  "topping_id" INTEGER,
  "topping_name" TEXT
);
INSERT INTO pizza_toppings
  ("topping_id", "topping_name")
VALUES
  (1, 'Bacon'),
  (2, 'BBQ Sauce'),
  (3, 'Beef'),
  (4, 'Cheese'),
  (5, 'Chicken'),
  (6, 'Mushrooms'),
  (7, 'Onions'),
  (8, 'Pepperoni'),
  (9, 'Peppers'),
  (10, 'Salami'),
  (11, 'Tomatoes'),
  (12, 'Tomato Sauce');
  ````
  
 # Case Study Questions
This case study has LOTS of questions - they are broken up by area of focus including:

## Pizza Metrics
Runner and Customer Experience

Ingredient Optimisation

Pricing and Ratings

Bonus DML Challenges (DML = Data Manipulation Language)

Each of the following case study questions can be answered using a single SQL statement.

Again, there are many questions in this case study - please feel free to pick and choose which ones you’d like to try!

Before you start writing your SQL queries however - you might want to investigate the data, you may want to do something with some of those null values and data types in the customer_orders and runner_orders tables!

## A. Pizza Metrics
How many pizzas were ordered?

How many unique customer orders were made?

How many successful orders were delivered by each runner?

How many of each type of pizza was delivered?

How many Vegetarian and Meatlovers were ordered by each customer?

What was the maximum number of pizzas delivered in a single order?

For each customer, how many delivered pizzas had at least 1 change and how many had no changes?

How many pizzas were delivered that had both exclusions and extras?

What was the total volume of pizzas ordered for each hour of the day?

What was the volume of orders for each day of the week?

## B. Runner and Customer Experience
How many runners signed up for each 1 week period? (i.e. week starts 2021-01-01)

What was the average time in minutes it took for each runner to arrive at the Pizza Runner HQ to pickup the order?

Is there any relationship between the number of pizzas and how long the order takes to prepare?

What was the average distance travelled for each customer?

What was the difference between the longest and shortest delivery times for all orders?

What was the average speed for each runner for each delivery and do you notice any trend for these values?

What is the successful delivery percentage for each runner?

## C. Ingredient Optimisation

What are the standard ingredients for each pizza?

What was the most commonly added extra?

What was the most common exclusion?

Generate an order item for each record in the customers_orders table in the format of one of the following:

Meat Lovers

Meat Lovers - Exclude Beef

Meat Lovers - Extra Bacon

Meat Lovers - Exclude Cheese, Bacon - Extra Mushroom, Peppers

Generate an alphabetically ordered comma separated ingredient list for each pizza order from the customer_orders table and add a 2x in front of any relevant ingredients

For example: "Meat Lovers: 2xBacon, Beef, ... , Salami"

What is the total quantity of each ingredient used in all delivered pizzas sorted by most frequent first?

## D. Pricing and Ratings
If a Meat Lovers pizza costs $12 and Vegetarian costs $10 and there were no charges for changes - how much money has Pizza Runner made so far if there are no delivery fees?

What if there was an additional $1 charge for any pizza extras?

Add cheese is $1 extra

The Pizza Runner team now wants to add an additional ratings system that allows customers to rate their runner, how would you design an additional table for this new dataset - generate a schema for this new table and insert your own data for ratings for each successful customer order between 1 to 5.

Using your newly generated table - can you join all of the information together to form a table which has the following information for successful deliveries?

customer_id

order_id

runner_id

rating

order_time

pickup_time

Time between order and pickup

Delivery duration

Average speed

Total number of pizzas

If a Meat Lovers pizza was $12 and Vegetarian $10 fixed prices with no cost for extras and each runner is paid $0.30 per kilometre traveled - how much money does Pizza Runner have left over after these deliveries?

## E. Bonus Questions

If Danny wants to expand his range of pizzas - how would this impact the existing data design? Write an INSERT statement to demonstrate what would happen if a new Supreme pizza with all the toppings was added to the Pizza Runner menu?

## My practical solution 

````sql
SELECT * 
FROM customer_orders; -- table 2
SELECT * 
FROM pizza_names; -- table 4 
SELECT * 
FROM pizza_recipes; -- table 5
SELECT *
FROM runners; -- table 1
SELECT* 
FROM pizza_toppings; -- table 6
SELECT * 
FROM runner_orders; -- table 3
````
--------------------------------------------------------------------------------------------------------------------------------------------------------------
-- Note: 
-- customer_orders — Customers’ pizza orders with 1 row each for individual pizza with topping exclusions and extras, and order time.
-- runner_orders — Orders assigned to runners documenting the pickup time, 
                -- distance and duration from Pizza Runner HQ to customer, and cancellation remark.
-- runners — Runner IDs and registration date
-- pizza_names — Pizza IDs and name
-- pizza_recipes — Pizza IDs and topping names
-- pizza_toppings — Topping IDs and name

------------------------------------ Data cleaning--------------------------------------------
-- Before going into the case study question, quick query all the table above show alot of missing value
-- so that we need to clean the data first

-- Cleaning data: 
-- both tables have some missing values and different types of error. In this case, we transform 
-- all messy data into NULL 
-- the following cases have transformed them into NULL 
-- a. customer_orders 

````sql
SELECT order_id, customer_id, pizza_id, 
CASE 
    WHEN exclusions = '' THEN NULL
    WHEN exclusions = 'null' THEN NULL 
    ELSE exclusions
    END AS exclusions_clean, 
CASE 
    WHEN extras = '' THEN NULL 
    WHEN extras = 'null' THEN NULL 
    ELSE extras
    END AS extras_clean
INTO #cust_order
FROM customer_orders;
select * from #cust_order
````
-- b. runner_orders
````sql
SELECT order_id, runner_id,
CASE 
    WHEN pickup_time = 'null' THEN NULL 
    ELSE pickup_time
    END AS pickup_time,
CASE 
    WHEN distance = 'null' THEN NULL 
    WHEN distance LIKE '%km' THEN TRIM('km' FROM distance)
    ELSE distance
    END AS distance_km,
CASE 
    WHEN duration = 'null' THEN NULL 
    WHEN duration LIKE '%minutes' THEN TRIM('minutes' FROM duration)
    WHEN duration LIKE '%mins' THEN TRIM('mins' FROM duration)
    WHEN duration LIKE '%minute' THEN TRIM('minute' FROM duration) 
    ELSE duration 
    END AS duration_mins,
CASE 
    WHEN cancellation = '' THEN NULL 
    WHEN cancellation = 'null' THEN NULL 
    ELSE cancellation
    END AS cancellation
INTO #runner_orders
FROM runner_orders;
````
````sql
SELECT * 
FROM #runner_orders;
````
````sql
ALTER TABLE #runner_orders
ALTER COLUMN 
    distance_km DECIMAL(3,1);
ALTER TABLE #runner_orders
ALTER COLUMN duration_mins INT;
````
# -----------------------------Case Study Questions---------------------------------------------
--This case study has LOTS of questions - they are broken up by area of focus including:

## A. Pizza Metrics

### 1. How many pizzas were ordered?
````sql
SELECT COUNT(order_id) as pizza_count
FROM #cust_order;
````
-- 14 pizzas were order

### 2. How many unique customer orders were made?
````sql
SELECT COUNT(DISTINCT order_id) as unique_orders
FROM #cust_order;
````
-- 10 different orders 

### 3. How many successful orders were delivered by each runner?
````sql
SELECT 
    runner_id, 
    COUNT(order_id) AS order_count
FROM #runner_orders
WHERE duration_mins IS NOT NULL
GROUP BY runner_id;
````
-- There are 3 runners, runner 1 has 4 successful orders, runner 2 has 3 and runner 3 has 1 only

### 4. How many of each type of pizza was delivered?
````sql
SELECT 
    CAST(p.pizza_name as nvarchar(100)), 
    COUNT(c.pizza_id) as pizza_count
FROM pizza_names as p
JOIN #cust_order as c
    ON p.pizza_id = c.pizza_id
JOIN #runner_orders as r
    ON c.order_id = r.order_id 
WHERE r.duration_mins IS NOT NULL
GROUP BY CAST(p.pizza_name as nvarchar(100));
````
-- Meatlovers 9, Vegetarian 3

### 5. How many Vegetarian and Meatlovers were ordered by each customer?
````sql
SELECT 
    c.customer_id,
    CAST(p.pizza_name as nvarchar(100)) as pizza_name, 
    COUNT(c.pizza_id) as pizza_count
FROM pizza_names as p
JOIN #cust_order as c
    ON p.pizza_id = c.pizza_id
GROUP BY c.customer_id, CAST(p.pizza_name as nvarchar(100))
ORDER BY c.customer_id;
-- customer 101: 2 meatlover 1 vegetarian 
-- customer 102: 2 meatlover 1 vegetarian
-- customer 103: 3 meatlover 1 vegetarian
-- customer 104: 3 meatlover 
-- customer 105: 1 vegetarian 
````
### 6. What was the maximum number of pizzas delivered in a single order?
````sql
WITH temp as
(SELECT
    order_id,
    COUNT(pizza_id) AS pizza_count
FROM #cust_order
GROUP BY order_id)

select max(pizza_count) as max_count
from temp 
;
````
-- the maximum number of pizza order is 3 

### 7. For each customer, how many delivered pizzas had at least 1 change and how many had no changes?
````sql
WITH pizza_changes_counter AS (
SELECT 
    co.customer_id,
    CASE 
        WHEN co.exclusions_clean LIKE '%' OR co.extras_clean LIKE '%' THEN 1
        ELSE 0
    END AS pizza_change_count,
    CASE
        WHEN co.exclusions_clean IS NULL AND co.extras_clean IS NULL THEN 1
        WHEN co.exclusions_clean IS NULL AND co.extras_clean = 'NaN' THEN 1
        ELSE 0
    END AS pizza_no_change_count
FROM #cust_order co
LEFT JOIN #runner_orders ro 
    ON co.order_id = ro.order_id
WHERE ro.duration_mins IS NOT NULL
)
  
SELECT
    customer_id,
    SUM(pizza_change_count) AS having_change,
    SUM(pizza_no_change_count) AS no_change
FROM pizza_changes_counter
GROUP BY customer_id;
````
-- customer 101 and 102 have no change on their recipes
-- customer 103,104,105 prefer their own custom recipe

### 8. How many pizzas were delivered that had both exclusions and extras?
````sql
SELECT 
    c.customer_id,
    SUM(
        CASE 
            WHEN c.exclusions_clean is NOT NULL AND c.extras_clean IS NOT NULL THEN 1
            ELSE 0 
            END) AS pizza_count_w_exclusions_extras    
FROM #cust_order AS c
JOIN #runner_orders AS r 
    ON c.order_id = r.order_id
WHERE r.duration_mins IS NOT NULL 
GROUP BY c.customer_id
ORDER BY pizza_count_w_exclusions_extras DESC 
````
-- only 1 order with full topping

### 9. What was the total volume of pizzas ordered for each hour of the day?
````sql
SELECT
	COUNT(order_id) AS order_count,
	DATEPART(HOUR, [order_time]) AS hour_of_day
FROM customer_orders
GROUP BY DATEPART(HOUR, [order_time]);
````
-- Highest volumne of pizza ordered is at 13, 18, 21 and 23 
-- Lowest volumne of pizza ordered is at 11:00 and 19:00
### 10. What was the volume of orders for each day of the week?
````sql
SELECT FORMAT(DATEADD(DAY, 2, order_time),'dddd') AS day_of_week, 
-- add 2 to adjust 1st day of the week as Monday
 COUNT(order_id) AS total_pizzas_ordered
FROM customer_orders
GROUP BY FORMAT(DATEADD(DAY, 2, order_time),'dddd');
````
-- Monday, Friday: 5 pizzas
-- Saturday: 3 pizzas
-- Sunday: 1 pizzas

## B. Runner and Customer Experience

### 1. How many runners signed up for each 1 week period? (i.e. week starts 2021-01-01)
````sql
SELECT
	COUNT(runner_id) AS runner_count,
    DATEPART(WEEK,registration_date) AS registration_week
FROM runners
GROUP BY DATEPART(WEEK,registration_date);
````
-- Week 1: 1. Week 2: 2. Week 3: 1

-- 2. What was the average time in minutes it took for each runner to arrive at the Pizza Runner HQ to pickup the order?
````sql
SELECT
    r.runner_id,
    AVG(DATEDIFF(MINUTE, c.order_time, r.pickup_time)) AS time_mins
FROM customer_orders c
LEFT JOIN #runner_orders r
	ON c.order_id = r.order_id
GROUP BY r.runner_id;
````
-- time to deliver: runner 1: 15 mins, runner 2: 24 mins, runner 3: 10 mins 

### 3. Is there any relationship between the number of pizzas and how long the order takes to prepare?
````sql
WITH prep_time_cte AS
(
 SELECT c.order_id, COUNT(c.order_id) AS pizza_order, 
  c.order_time, r.pickup_time, 
  DATEDIFF(MINUTE, c.order_time, r.pickup_time) AS prep_time_minutes
 FROM customer_orders AS c
 JOIN #runner_orders AS r
  ON c.order_id = r.order_id
 WHERE r.duration_mins IS NOT NULL
 GROUP BY c.order_id, c.order_time, r.pickup_time
)
SELECT pizza_order, AVG(prep_time_minutes) AS avg_prep_time_minutes
FROM prep_time_cte
WHERE prep_time_minutes > 1
GROUP BY pizza_order;
````
-- On average, a single pizza order takes 12 mins, an order with 2 pizzas would take 18 mins 
-- and an order with 3 pizzas takes 30 mins 

### 4. What was the average distance travelled for each customer?
````sql
SELECT
	c.customer_id,
    AVG(r.distance_km) AS avg_dist_km
FROM #cust_order c 
LEFT JOIN #runner_orders r
	ON c.order_id = r.order_id
GROUP BY c.customer_id;
````
-- customer 101: 20km, customer 102: 16.73km, customer 103: 23.4km, customer 104: 10km, customer 105: 25km

### 5. What was the difference between the longest and shortest delivery times for all orders?
````sql
SELECT
    MAX(duration_mins) - MIN(duration_mins) AS delivery_time_diff
FROM #runner_orders;
````
-- 30 mins 

### 6. What was the average speed for each runner for each delivery and do you notice any trend for these values?
````sql
SELECT r.runner_id,  
 COUNT(c.order_id) AS pizza_count, 
 r.distance_km, r.duration_mins, 
 ROUND((r.distance_km/r.duration_mins * 60), 2) AS avg_speed
FROM #runner_orders AS r
JOIN #cust_order AS c
 ON r.order_id = c.order_id
WHERE distance_km IS NOT NULL 
GROUP BY r.runner_id, r.distance_km, r.duration_mins
ORDER BY r.runner_id;
````
-- runner 1: 37.5km/h to 60km/h
-- runner 2: 35.1km/h to 93.6km/h -> the best runner time 
-- runner 3: 40km/h 
### 7. What is the successful delivery percentage for each runner?
````sql
SELECT runner_id, 
 ROUND(100 * SUM
  (CASE WHEN distance_km IS NULL THEN 0
  ELSE 1
  END) / COUNT(*), 0) AS success_perc
FROM #runner_orders
GROUP BY runner_id;
````
-- runner 1 has 100% success, runner 2 has 75% and runner 3 has 50%
-- but this result says nothing because the cancellation is out of control for the runners
## C. Ingredient Optimisation

1. What are the standard ingredients for each pizza?

2. What was the most commonly added extra?

3. What was the most common exclusion?

4. Generate an order item for each record in the customers_orders table in the format of one of the following:
  Meat Lovers
  Meat Lovers - Exclude Beef
  Meat Lovers - Extra Bacon
  Meat Lovers - Exclude Cheese, Bacon - Extra Mushroom, Peppers

5. Generate an alphabetically ordered comma separated ingredient list for each pizza order from the customer_orders table and add a 2x in front of any relevant ingredients For example: "Meat Lovers: 2xBacon, Beef, ... , Salami
 
6. What is the total quantity of each ingredient used in all delivered pizzas sorted by most frequent first

## D. Pricing and Ratings

### 1. If a Meat Lovers pizza costs $12 and Vegetarian costs $10 and there were no charges for changes - 

How much money has Pizza Runner made so far if there are no delivery fees?
````sql
SELECT
SUM(CASE
	WHEN pizza_id = 1 THEN 12
	WHEN pizza_id = 2 THEN 10
	END) AS pizza_cost
FROM #cust_order;
````
-- pizza cost: 160

 2. What if there was an additional $1 charge for any pizza extras?

Add cheese is $1 extra


 3. The Pizza Runner team now wants to add an additional ratings system that allows customers to rate their runner, 

how would you design an additional table for this new dataset: 

- generate a schema for this new table and insert your own data for ratings for each successful customer order between 1 to 5.

4. Using your newly generated table - 

can you join all of the information together to form a table which has the following information for successful deliveries?

* customer_id

* order_id

* runner_id

* rating

* order_time

* pickup_time

* Time between order and pickup

* Delivery duration

* Average speed

* Total number of pizzas

## 5. If a Meat Lovers pizza was $12 and Vegetarian $10 fixed prices with no cost for extras and each runner is paid $0.30 per kilometre traveled -

how much money does Pizza Runner have left over after these deliveries? 
````sql
WITH base_pizza_cost AS (
SELECT 
    SUM(CASE
        WHEN pizza_id = 1 THEN 12
        WHEN pizza_id = 2 THEN 10
    END) AS pizza_cost
FROM #cust_order
),
````
-- 160 for pizza cost 
````sql
runner_cost_list AS (
SELECT distance_km,
    CASE
        WHEN distance_km IS NOT NULL THEN distance_km*0.30
    END AS runner_cost
FROM #runner_orders
),
runner_cost_total AS (
SELECT SUM(runner_cost) AS total_runner_cost
FROM runner_cost_list
)
SELECT
    pizza_cost - total_runner_cost
FROM base_pizza_cost, runner_cost_total
````
-- 116.440 

-- E. Bonus DML Challenges (DML = Data Manipulation Language)
-- If Danny wants to expand his range of pizzas - how would this impact the existing data design? 
-- Write an INSERT statement to demonstrate what would happen if a new Supreme pizza with all the toppings was added to the Pizza Runner menu?
