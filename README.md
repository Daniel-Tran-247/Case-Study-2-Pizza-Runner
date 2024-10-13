# 🍕Case Study #2 - Pizza Runners

[Challenge Site](https://8weeksqlchallenge.com/case-study-2/)

## 📖Table of Contents
- 🎯 [Problem Statement](problem-statement)
- 📂 [Dataset](dataset)
- 🚀 [Questions & Solutions](questions-&-solutions)

## 🎯Problem Statement
> Danny just lauchned Pizza Runner and started recruiting "runners" to deliver fresh pizza from the
> his house (aka "Headquater"). He has a specialist design an entity relationship diagram of the
> database related to his business but it requires further assistance to clean data and apply some
> basic calculations so he can better direct his runners and optimise Pizza Runner's operatioon.  

## Dataset
### Entity Relationship Diagram
![image](https://user-images.githubusercontent.com/75436284/225012461-ad086230-84cb-4c2c-9fb3-d387260e7406.png)

### Table 1:  ```runners```
```sql
SELECT * FROM pizza_runner.runners;
```
<details>
<summary>
  Result
</summary>

| runner_id | registration_date        |
| --------- | ------------------------ |
| 1         | 2021-01-01T00:00:00.000Z |
| 2         | 2021-01-03T00:00:00.000Z |
| 3         | 2021-01-08T00:00:00.000Z |
| 4         | 2021-01-15T00:00:00.000Z |

 </details>
 
 
### Table 2: ```customer_orders```
```sql
SELECT * FROM pizza_runner.customer_orders;
```
<details>
<summary>
  Result
</summary>

| order_id | customer_id | pizza_id | exclusions | extras | order_time               |
| -------- | ----------- | -------- | ---------- | ------ | ------------------------ |
| 1        | 101         | 1        |            |        | 2020-01-01T18:05:02.000Z |
| 2        | 101         | 1        |            |        | 2020-01-01T19:00:52.000Z |
| 3        | 102         | 1        |            |        | 2020-01-02T23:51:23.000Z |
| 3        | 102         | 2        |            | NaN    | 2020-01-02T23:51:23.000Z |
| 4        | 103         | 1        | 4          |        | 2020-01-04T13:23:46.000Z |
| 4        | 103         | 1        | 4          |        | 2020-01-04T13:23:46.000Z |
| 4        | 103         | 2        | 4          |        | 2020-01-04T13:23:46.000Z |
| 5        | 104         | 1        | null       | 1      | 2020-01-08T21:00:29.000Z |
| 6        | 101         | 2        | null       | null   | 2020-01-08T21:03:13.000Z |
| 7        | 105         | 2        | null       | 1      | 2020-01-08T21:20:29.000Z |
| 8        | 102         | 1        | null       | null   | 2020-01-09T23:54:33.000Z |
| 9        | 103         | 1        | 4          | 1, 5   | 2020-01-10T11:22:59.000Z |
| 10       | 104         | 1        | null       | null   | 2020-01-11T18:34:49.000Z |
| 10       | 104         | 1        | 2, 6       | 1, 4   | 2020-01-11T18:34:49.000Z |

 </details>
 
 
 ### Table 3:  ```runner_orders```
```sql
SELECT * FROM pizza_runner.runner_orders;
```
<details>
<summary>
  Result
</summary>

| order_id | runner_id | pickup_time         | distance | duration   | cancellation            |
| -------- | --------- | ------------------- | -------- | ---------- | ----------------------- |
| 1        | 1         | 2020-01-01 18:15:34 | 20km     | 32 minutes |                         |
| 2        | 1         | 2020-01-01 19:10:54 | 20km     | 27 minutes |                         |
| 3        | 1         | 2020-01-03 00:12:37 | 13.4km   | 20 mins    | NaN                     |
| 4        | 2         | 2020-01-04 13:53:03 | 23.4     | 40         | NaN                     |
| 5        | 3         | 2020-01-08 21:10:57 | 10       | 15         | NaN                     |
| 6        | 3         | null                | null     | null       | Restaurant Cancellation |
| 7        | 2         | 2020-01-08 21:30:45 | 25km     | 25mins     | null                    |
| 8        | 2         | 2020-01-10 00:15:02 | 23.4 km  | 15 minute  | null                    |
| 9        | 2         | null                | null     | null       | Customer Cancellation   |
| 10       | 1         | 2020-01-11 18:50:20 | 10km     | 10minutes  | null                    |


 </details>
 
 
 ### Table 4:  ```pizza_names```
```sql
SELECT * FROM pizza_runner.pizza_names;
```
<details>
<summary>
  Result
</summary>

| pizza_id | pizza_name |
| -------- | ---------- |
| 1        | Meatlovers |
| 2        | Vegetarian |

 </details>
 
 
  ### Table 5:  ```pizza_recipes```
```sql
SELECT * FROM pizza_runner.pizza_recipes;
```
<details>
<summary>
  Result
</summary>

| pizza_id | toppings                |
| -------- | ----------------------- |
| 1        | 1, 2, 3, 4, 5, 6, 8, 10 |
| 2        | 4, 6, 7, 9, 11, 12      |

</details>


  ### Table 6:  ```pizza_toppings```
```sql
SELECT * FROM pizza_runner.pizza_toppings;
```
<details>
<summary>
  Result
</summary>

| topping_id | topping_name |
| ---------- | ------------ |
| 1          | Bacon        |
| 2          | BBQ Sauce    |
| 3          | Beef         |
| 4          | Cheese       |
| 5          | Chicken      |
| 6          | Mushrooms    |
| 7          | Onions       |
| 8          | Pepperoni    |
| 9          | Peppers      |
| 10         | Salami       |
| 11         | Tomatoes     |
| 12         | Tomato Sauce |

</details>

 
## 🎯Questions & Solutions
### ✔️Data Type Check
- Check data type of each column in ```customer_orders``` and ```runner_orders``` table to compare the changes after cleaning those tables. 

```sql
SELECT 
  table_name,
  column_name,
  data_type
FROM information_schema.columns
WHERE table_name = 'customer_orders';
```

<details>
  <summary>
    Result
  </summary>
  
| table_name      | column_name | data_type                   |
| --------------- | ----------- | --------------------------- |
| customer_orders | order_id    | integer                     |
| customer_orders | customer_id | integer                     |
| customer_orders | pizza_id    | integer                     |
| customer_orders | order_time  | timestamp without time zone |
| customer_orders | exclusions  | character varying           |
| customer_orders | extras      | character varying           |
 
</details>

```sql
SELECT 
  table_name,
  column_name,
  data_type
FROM information_schema.columns
WHERE table_name = 'runner_orders';
```

<details>
  <summary>
    Result
  </summary>
  
| table_name    | column_name  | data_type         |
| ------------- | ------------ | ----------------- |
| runner_orders | order_id     | integer           |
| runner_orders | runner_id    | integer           |
| runner_orders | pickup_time  | character varying |
| runner_orders | distance     | character varying |
| runner_orders | duration     | character varying |
| runner_orders | cancellation | character varying |
 
</details>

---> ```pickup_time``` is supposed to be ```timestamp```

---> ```distance``` and ```duration``` are supposed to be ```numeric```



### 🧹Data Cleaning 
- There are some missing values in ```customer_orders``` and ```runner_orders``` table that indicates either as ***blank strings ' '*** or as text ***'Null'*** instead of ```Null``` type. 
- The display of unit is not consitent across ```distance``` and ```duration``` column in ```runner_orders``` table.
- Incorrect data type in ```distance```, ```duration```, and ```pickup_time``` column in ```runner_orders``` table. 

---> ```customer_orders```: Creare a temporary table that replaces ***blank strings*** and ***Null (as text)*** with ```Null type``` 

```sql
DROP TABLE IF EXISTS customer_orders_cleaned;

CREATE TEMP TABLE customer_orders_cleaned AS (
  SELECT 
  	order_id,
  	customer_id,
  	pizza_id, 
  	CASE 
  		WHEN exclusions = '' THEN NULL
  		WHEN exclusions = 'null' THEN NULL
  		ELSE exclusions
  	END AS exclusions, 
  	CASE 
  		WHEN extras = '' THEN NULL
  		WHEN extras = 'null' THEN NULL
  		ELSE extras
  	END AS extras,
  	order_time
  FROM pizza_runner.customer_orders);

SELECT * FROM customer_orders_cleaned;
```
<details>
   <summary>
     Result
  </summary>
  
| order_id | customer_id | pizza_id | exclusions | extras | order_time               |
| -------- | ----------- | -------- | ---------- | ------ | ------------------------ |
| 1        | 101         | 1        |            |        | 2020-01-01T18:05:02.000Z |
| 2        | 101         | 1        |            |        | 2020-01-01T19:00:52.000Z |
| 3        | 102         | 1        |            |        | 2020-01-02T23:51:23.000Z |
| 3        | 102         | 2        |            |        | 2020-01-02T23:51:23.000Z |
| 4        | 103         | 1        | 4          |        | 2020-01-04T13:23:46.000Z |
| 4        | 103         | 1        | 4          |        | 2020-01-04T13:23:46.000Z |
| 4        | 103         | 2        | 4          |        | 2020-01-04T13:23:46.000Z |
| 5        | 104         | 1        |            | 1      | 2020-01-08T21:00:29.000Z |
| 6        | 101         | 2        |            |        | 2020-01-08T21:03:13.000Z |
| 7        | 105         | 2        |            | 1      | 2020-01-08T21:20:29.000Z |
| 8        | 102         | 1        |            |        | 2020-01-09T23:54:33.000Z |
| 9        | 103         | 1        | 4          | 1, 5   | 2020-01-10T11:22:59.000Z |
| 10       | 104         | 1        |            |        | 2020-01-11T18:34:49.000Z |
| 10       | 104         | 1        | 2, 6       | 1, 4   | 2020-01-11T18:34:49.000Z |
</details>

---> ```runner_orders```: Create a temporary table that replaces the ***blank strings*** and ***null (as text)*** with ```Null``` value. Aditionally, remove the units from ```distance``` and ```duration``` colummn for consistency. Finally, convert data type of ```distance```, ```duration```, and ```pickup_time``` into the correct type.

```sql
DROP TABLE IF EXISTS runner_oders_cleaned;

CREATE TEMP TABLE runner_orders_cleaned AS (
  SELECT 
  	order_id,
  	runner_id,
  	CASE 
  		WHEN pickup_time = 'null' THEN NULL
  		ELSE pickup_time
  	END :: TIMESTAMP AS pickup_time, 
  	CASE 
  		WHEN distance = 'null' THEN NULL
  		WHEN distance LIKE '%km' THEN TRIM('km' FROM distance)
  		ELSE distance
  	END :: FLOAT AS distance,
  	CASE 
  		WHEN duration = 'null' THEN NULL
  		WHEN duration LIKE '%minutes' THEN TRIM('minutes' FROM duration)
  		WHEN duration LIKE '%minute' THEN TRIM('minute' FROM duration)
  		WHEN duration LIKE '%mins' THEN TRIM('mins' FROM duration) 
  		ELSE duration
  	END :: INT AS duration,
  	CASE 
    	WHEN cancellation IN ('', 'null') THEN NULL
  		ELSE cancellation
  	END AS cancellation
  FROM pizza_runner.runner_orders);

SELECT * FROM runner_orders_cleaned;
```
<details>
   <summary>
     Result
  </summary>
  
| order_id | runner_id | pickup_time              | distance | duration | cancellation            |
| -------- | --------- | ------------------------ | -------- | -------- | ----------------------- |
| 1        | 1         | 2020-01-01T18:15:34.000Z | 20       | 32       |                         |
| 2        | 1         | 2020-01-01T19:10:54.000Z | 20       | 27       |                         |
| 3        | 1         | 2020-01-03T00:12:37.000Z | 13.4     | 20       |                         |
| 4        | 2         | 2020-01-04T13:53:03.000Z | 23.4     | 40       |                         |
| 5        | 3         | 2020-01-08T21:10:57.000Z | 10       | 15       |                         |
| 6        | 3         |                          |          |          | Restaurant Cancellation |
| 7        | 2         | 2020-01-08T21:30:45.000Z | 25       | 25       |                         |
| 8        | 2         | 2020-01-10T00:15:02.000Z | 23.4     | 15       |                         |
| 9        | 2         |                          |          |          | Customer Cancellation   |
| 10       | 1         | 2020-01-11T18:50:20.000Z | 10       | 10       |                         |

</details>

**✔️Check Data Type of ```runner_orders_cleaned```**
```sql
SELECT 
  table_name,
  column_name,
  data_type
FROM information_schema.columns
WHERE table_name = 'runner_orders_cleaned';
```

<details>
  <summary>
    Result
  </summary>
  
| table_name            | column_name  | data_type                   |
| --------------------- | ------------ | --------------------------- |
| runner_orders_cleaned | order_id     | integer                     |
| runner_orders_cleaned | runner_id    | integer                     |
| runner_orders_cleaned | pickup_time  | timestamp without time zone |
| runner_orders_cleaned | distance     | double precision            |
| runner_orders_cleaned | duration     | integer                     |
| runner_orders_cleaned | cancellation | character varying           |
  
</details>


### A. Pizza Metrics

<details>
  <summary>
    View Questionss & Solutions
  </summary>
  
  ### Q1. How many pizzas were ordered?
  ```sql
  SELECT 
    COUNT(order_id) AS pizza_count 
  FROM customer_orders_cleaned;
  ```
  <details>
    <summary>
      Result
    </summary>
    
| pizza_count |
| ----------- |
| 14          |
    
  </details>

  
  ### Q2. How many unique customer orders were made?
  ```sql
  SELECT 
    COUNT(DISTINCT order_id) AS order_count 
  FROM customer_orders_cleaned;
  ```
  <details>
    <summary>
      Result
    </summary>
    
| order_count |
| ----------- |
| 10          |
    
  </details>
  
  ### Q3. How many successful orders were delivered by each runner?
  ```sql
  SELECT 
    runner_id,
    COUNT(order_id) AS successful_order_count
  FROM runner_orders_cleaned
  WHERE cancellation IS NULL
  GROUP BY runner_id;
  ```
  <details>
    <summary>
      Result
    </summary>
    
| runner_id | successful_order_count |
| --------- | ---------------------- |
| 1         | 4                      |
| 2         | 3                      |
| 3         | 1                      |
    
  </details>
  
  ### Q4. How many of each type of pizza was delivered?
  ```sql
  SELECT 
    pizza_name,
      COUNT(pizza_id) AS delivered_pizza_count
  FROM runner_orders_cleaned
  JOIN customer_orders_cleaned 
  USING(order_id)
  JOIN pizza_runner.pizza_names
  USING(pizza_id)
  WHERE cancellation IS NULL
  GROUP BY pizza_name;  
  ```
  <details>
    <summary>
      Result
    </summary>
    
| pizza_name | delivered_pizza_count |
| ---------- | ----- |
| Vegetarian | 3     |
| Meatlovers | 9     |
    
  </details>
  
  ### Q5. How many Vegeterian and Meatlovers were ordered by each customer?
  ```sql
  SELECT 
    customer_id,
      pizza_name,
      COUNT(pizza_id) AS ordered_pizza_count
  FROM runner_orders_cleaned
  JOIN customer_orders_cleaned 
  USING(order_id)
  JOIN pizza_runner.pizza_names
  USING(pizza_id)
  GROUP BY customer_id, pizza_name
  ORDER BY customer_id  
  ```
  <details>
    <summary>
      Result
    </summary>
    
| customer_id | pizza_name | ordered_pizza_count |
| ----------- | ---------- | ----- |
| 101         | Meatlovers | 2     |
| 101         | Vegetarian | 1     |
| 102         | Meatlovers | 2     |
| 102         | Vegetarian | 1     |
| 103         | Meatlovers | 3     |
| 103         | Vegetarian | 1     |
| 104         | Meatlovers | 3     |
| 105         | Vegetarian | 1     |
    
  </details>
  
  ### Q6. What was the maximum number of pizzas devilvered in a single order?
  ```sql
  SELECT 
    MAX(delivered_pizza_count)
  FROM (
    SELECT 
        order_id,
        COUNT(pizza_id) AS delivered_pizza_count
    FROM runner_orders_cleaned
    JOIN customer_orders_cleaned 
    USING(order_id)
    WHERE cancellation IS NULL
    GROUP BY order_id
    ORDER BY order_id ) AS delivered_pizza
  ```
  <details>
    <summary>
      Result
    </summary>
    
| max |
| ----|
| 3   |
    
  </details>
  
  ### Q7. For each customer, how many delivered pizzas had at least 1 change and how many had no changes?
  ```sql
  SELECT 
      customer_id, 
      SUM(CASE WHEN (exclusions IS NOT NULL) OR (extras IS NOT NULL) THEN 1 ELSE 0 END) AS at_least_1_change,
      SUM(CASE WHEN (exclusions IS NULL) AND (extras IS NULL) THEN 1 ELSE 0 END) AS no_change
  FROM runner_orders_cleaned
  JOIN customer_orders_cleaned 
  USING(order_id)
  WHERE cancellation IS NULL
  GROUP BY customer_id
  ORDER BY customer_id  
  ```
  <details>
    <summary>
      Result
    </summary>
    
| customer_id | at_least_1_change | no_change |
| ----------- | ----------------- | --------- |
| 101         | 0                 | 2         |
| 102         | 0                 | 3         |
| 103         | 3                 | 0         |
| 104         | 2                 | 1         |
| 105         | 1                 | 0         |
    
  </details>
  
  ### Q8. How many pizzas were delivered that had both exclusions and extras?
  ```sql
  SELECT 
  	COUNT(pizza_id) AS pizza_count
  FROM runner_orders_cleaned
  JOIN customer_orders_cleaned 
  USING(order_id)
  WHERE cancellation IS NULL AND (extras IS NOT NULL) AND (exclusions IS NOT NULL)   
  ```
  
  <details>
    <summary>
      Result
    </summary>
    
| pizza_count |
| ----------- |
| 1           |
    
  </details>
  
  ###  Q9. What was the total volume of pizzas ordered for each hour of the day?
  ```sql
  SELECT 
  	DATE_PART('HOUR', order_time) AS hour_of_day,
  	COUNT(pizza_id) AS order_count
  FROM customer_orders_cleaned
  GROUP BY hour_of_day
  ORDER BY hour_of_day
  ```
  
  <details>
    <summary>
      Result
    </summary>
    
| hour_of_day | order_count |
| ----------- | ----------- |
| 11          | 1           |
| 13          | 3           |
| 18          | 3           |
| 19          | 1           |
| 21          | 3           |
| 23          | 3           |
    
  </details>

  ### Q10. What was the volume of orders for each day of week?
  ```sql
  SELECT
  	TO_CHAR(order_time, 'day') AS day_of_week,
  	COUNT(pizza_id) AS order_count
  FROM customer_orders_cleaned
  GROUP BY day_of_week
  ORDER BY day_of_week
  ```
  
  <details>
    <summary>
      Result
    </summary>
    
| day_of_week | order_count |
| ----------- | ----------- |
| friday      | 1           |
| saturday    | 5           |
| thursday    | 3           |
| wednesday   | 5           |
    
  </details>
</details>
 
