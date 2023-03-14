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
### 🧹Data Cleaning 
- There are some missing values in ```customer_orders``` and ```runner_orders``` table that indicates either as ***blank strings ' '*** or as text ***'Null'*** instead of ```Null``` type. 
- The display of unit is not consitent across ```distance``` and ```duration``` column in ```runner_orders``` table.

---> Creare a temporary table that replaces ***blank strings*** and ***Null (as text)*** with ```Null type```  

### A. Pizza Metrics

<details>
  <summary>
    Result
  </summary>
  
  ### Q1. How many pizzas were ordered?
  ### Q2. How many unique customer orders were made?
  ### Q3. How many successful orders were delivered by each runner?

</details>

### B. Runner and Customer Experience 
### C. Ingredient Optimisation
### D. Pricing and Ratings
### E. Bonnus Questions 
 
 
