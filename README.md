# SQL for Data Science
### Course from Coursera
https://www.coursera.org/learn/sql-for-data-science/home/welcome


### Yelp Dataset SQL Lookup   
https://www.coursera.org/learn/sql-for-data-science/supplement/VSJ29/yelp-dataset-sql-lookup

Data Scientist Role Play: Profiling and Analyzing the Yelp Dataset Coursera Worksheet

This is a 2-part assignment. In the first part, you are asked a series of questions that will help you profile and understand the data just like a data scientist would. For this first part of the assignment, you will be assessed both on the correctness of your findings, as well as the code you used to arrive at your answer. You will be graded on how easy your code is to read, so remember to use proper formatting and comments where necessary.

In the second part of the assignment, you are asked to come up with your own inferences and analysis of the data for a particular research question you want to answer. You will be required to prepare the dataset for the analysis you choose to do. As with the first part, you will be graded, in part, on how easy your code is to read, so use proper formatting and comments to illustrate and communicate your intent as required.

For both parts of this assignment, use this "worksheet." It provides all the questions you are being asked, and your job will be to transfer your answers and SQL coding where indicated into this worksheet so that your peers can review your work. You should be able to use any Text Editor (Windows Notepad, Apple TextEdit, Notepad ++, Sublime Text, etc.) to copy and paste your answers. If you are going to use Word or some other page layout application, just be careful to make sure your answers and code are lined appropriately.
In this case, you may want to save as a PDF to ensure your formatting remains intact for you reviewer.

## Part 1: Yelp Dataset Profiling and Understanding

### 1. Profile the data by finding the total number of records for each of the tables below:
	
i. Attribute table = **10000**    
ii. Business table = **10000**    
iii. Category table = **10000**   
iv. Checkin table = **10000**    
v. elite_years table = **10000**    
vi. friend table = **10000**   
vii. hours table = **10000**    
viii. photo table =  **10000**   
ix. review table = **10000**    
x. tip table = **10000**    
xi. user table = **10000**    
	
```SQL    
SELECT 
	COUNT(*)
FROM 
	table   
```

### 2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key.

i. Business = **ID 10000**   
ii. Hours = **business_id 1562**    
iii. Category = **business_id 2643**   
iv. Attribute = **business_id 1115**    
v. Review = **id 10000**    
vi. Checkin = **business_id 493**    
vii. Photo = **id 10000**    
viii. Tip = **business_id 3979, user_id 537**    
ix. User = **id 10000**    
x. Friend = **user_id 11**   
xi. Elite_years = **user_id 2780**    

*Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.   

```SQL 
SELECT 
	COUNT(distinct key_id)
FROM 
	table 
```   

### 3. Are there any columns with null values in the Users table? Indicate "yes," or "no."
Answer: **No**   

SQL code used to arrive at answer:   

```SQL 	
SELECT 
	*
FROM 
	user          
WHERE
	id IS NULL
	OR name IS NULL
	OR review_count IS NULL
	OR yelping_since IS NULL
	OR useful IS NULL
	OR funny IS NULL
	OR cool IS NULL
	OR fans IS NULL
	OR average_stars IS NULL
	OR compliment_hot IS NULL
	OR compliment_more IS NULL
	OR compliment_profile IS NULL
	OR compliment_cute IS NULL
	OR compliment_list IS NULL
	OR compliment_note IS NULL
	OR compliment_plain IS NULL
	OR compliment_cool IS NULL
	OR compliment_funny IS NULL
	OR compliment_writer IS NULL
	OR compliment_photos IS NULL
```	
-*Será tudo isso mesmo?*	

	
### 4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:

i. Table: Review, Column: Stars
	
	min: 1		max: 5		avg: 3.7082
		
	
ii. Table: Business, Column: Stars
	
	min: 1.0	max: 5.0	avg: 3.6549 
		
	
iii. Table: Tip, Column: Likes
	
	min: 0		max: 2		avg: 0.0144
		
	
iv. Table: Checkin, Column: Count
	
	min: 1		max: 53 	avg: 1.9414
		
	
v. Table: User, Column: Review_count
	
	min: 0		max: 2000	avg: 24.2995


```SQL 
 SELECT  
 	MIN(Column), MAX(Column), AVG(Column)
 FROM 
 	table     
```   

### 5. List the cities with the most reviews in descending order:

SQL code used to arrive at answer:
```SQL	 
SELECT
  city,
  SUM(review_count) AS total_reviews
FROM
  Business
GROUP BY
  city
ORDER BY
  total_reviews DESC
```   	

Copy and Paste the Result Below:   

| city            | total_reviews |   
|-----------------|---------------|   
| Las Vegas       |         82854 |   
| Phoenix         |         34503 |   
| Toronto         |         24113 |   
| Scottsdale      |         20614 |   
| Charlotte       |         12523 |   
| Henderson       |         10871 |   
| Tempe           |         10504 |   
| Pittsburgh      |          9798 |   
| Montréal        |          9448 |   
| Chandler        |          8112 |   
| Mesa            |          6875 |   
| Gilbert         |          6380 |   
| Cleveland       |          5593 |   
| Madison         |          5265 |   
| Glendale        |          4406 |   
| Mississauga     |          3814 |   
| Edinburgh       |          2792 |   
| Peoria          |          2624 |     
| North Las Vegas |          2438 |   
| Markham         |          2352 |   
| Champaign       |          2029 |   
| Stuttgart       |          1849 |   
| Surprise        |          1520 |   
| Lakewood        |          1465 |   
| Goodyear        |          1155 |    
(Output limit exceeded, 25 of 362 total rows shown)   

	
### 6. Find the distribution of star ratings to the business in the following cities:

i. Avon

SQL code used to arrive at answer:   

```SQL   
SELECT
  stars,
  SUM(review_count) AS total_reviews
FROM
  Business
WHERE
  city = 'Avon'
GROUP BY
  stars
```  

Copy and Paste the Resulting Table Below  (2 columns – star rating and count):   
| stars | total_reviews |
|-------|---------------|
|   1.5 |            10 |
|   2.5 |             6 |
|   3.5 |            88 |
|   4.0 |            21 |
|   4.5 |            31 |
|   5.0 |             3 |

ii. Beachwood

SQL code used to arrive at answer:

```SQL 
SELECT
  stars,
  SUM(review_count) AS total_reviews
FROM
  Business
WHERE
  city = 'Beachwood'
GROUP BY
  stars
```   

Copy and Paste the Resulting Table Below (2 columns - star rating and count):
		
| stars | total_reviews |
|-------|---------------|
|   2.0 |             8 |
|   2.5 |             3 |
|   3.0 |            11 |
|   3.5 |             6 |
|   4.0 |            69 |
|   4.5 |            17 |
|   5.0 |            23 |


### 7. Find the top 3 users based on their total number of reviews:
		
SQL code used to arrive at answer:

```SQL
SELECT
  id,
  name,
  SUM(review_count) AS total_reviews -- in case of duplicate user
FROM
  user
GROUP BY
  id -- Some didn´t have name
ORDER BY
  total_reviews DESC
LIMIT
  3	
```   

Copy and Paste the Result Below:

| id                     | name   | total_reviews |
|------------------------|--------|---------------|
| -G7Zkl1wIWBBmD0KRy_sCw | Gerald |          2000 |
| -3s52C4zL_DHRK0ULG6qtg | Sara   |          1629 |
| -8lbUNlXVSoXqaRRiHiSNg | Yuri   |          1339 |


### 8. Does posing more reviews correlate with more fans?

Please explain your findings and interpretation of the results:   
**Not really. 
Amy, who has the most amount of fans, has only 609 reviews. That is just 30.45% of reviews comparing to Gerald, who has the highest count of reviews and has about half amount of fans (253 fans).**

```SQL
SELECT
  id,
  name,
  SUM(review_count) AS total_reviews,
  SUM(fans) AS total_fans
  --fans -- it works too as SUM, but let be the SUM just to be sure
FROM
  user
GROUP BY
  id -- Some didn´t have name
ORDER BY
  total_fans DESC
```   


| id                     | name      | total_reviews | total_fans |   
|------------------------|-----------|---------------|------------|   
| -9I98YbNQnLdAmcYfb324Q | Amy       |           609 |        503 |   
| -8EnCioUmDygAbsYZmTeRQ | Mimi      |           968 |        497 |   
| --2vR0DIsmQ6WfcSzKWigw | Harald    |          1153 |        311 |   
| -G7Zkl1wIWBBmD0KRy_sCw | Gerald    |          2000 |        253 |   
| -0IiMAZI2SsQ7VmyzJjokQ | Christine |           930 |        173 |   
| -g3XIcCb2b-BD0QBCcq2Sw | Lisa      |           813 |        159 |   
| -9bbDysuiWeo2VShFJJtcw | Cat       |           377 |        133 |   
| -FZBTkAZEXoP7CYvRV2ZwQ | William   |          1215 |        126 |   
| -9da1xk7zgnnfO1uTVYGkA | Fran      |           862 |        124 |   
| -lh59ko3dxChBSZ9U7LfUw | Lissa     |           834 |        120 |   
| -B-QEUESGWHPE_889WJaeg | Mark      |           861 |        115 |   
| -DmqnhW4Omr3YhmnigaqHg | Tiffany   |           408 |        111 |   
| -cv9PPT7IHux7XUc9dOpkg | bernice   |           255 |        105 |   
| -DFCC64NXgqrxlO8aLU5rg | Roanna    |          1039 |        104 |   
| -IgKkE8JvYNWeGu8ze4P8Q | Angela    |           694 |        101 |   
| -K2Tcgh2EKX6e6HqqIrBIQ | .Hon      |          1246 |        101 |   
| -4viTt9UC44lWCFJwleMNQ | Ben       |           307 |         96 |   
| -3i9bhfvrM3F1wsC9XIB8g | Linda     |           584 |         89 |   
| -kLVfaJytOJY2-QdQoCcNQ | Christina |           842 |         85 |   
| -ePh4Prox7ZXnEBNGKyUEA | Jessica   |           220 |         84 |   
| -4BEUkLvHQntN6qPfKJP2w | Greg      |           408 |         81 |   
| -C-l8EHSLXtZZVfUAUhsPA | Nieves    |           178 |         80 |   
| -dw8f7FLaUmWR7bfJ_Yf0w | Sui       |           754 |         78 |   
| -8lbUNlXVSoXqaRRiHiSNg | Yuri      |          1339 |         76 |   
| -0zEEaDFIjABtPQni0XlHA | Nicole    |           161 |         73 |   
(Output limit exceeded, 25 of 10000 total rows shown)  


### 9. Are there more reviews with the word "love" or with the word "hate" in them?

Answer:   
**1644 reviews with the word 'LOVE' and 115 reviews with the word 'HATE'.**   
**!!ONE IMPORTANTE THING I noticed is that, if I use '%hate%' it counts the word 'WHATEVER'. So, if I use '% hate%', it excludes this mistake.   
Also, if I use '% hate %', it could exclude the cases when the word 'hate' comes followed by comma "," or dot "." and the conjugated verbs ("hated").    
The same I did for the word 'love'.**   
**Just out of curiosity: the results with the '%hate%': 232 and with '%love%': 1780.**

```SQL	
SQL code used to arrive at answer:
SELECT
  COUNT(id) AS total_reviews_LOVE
FROM
  review
WHERE
  text LIKE '% love%' --with space before the LOVE
```

```SQL	  
SELECT
  COUNT(id) AS total_reviews_HATE
FROM
  review
WHERE
  text LIKE '% hate%' --with space before HATE
```	
	
### 10. Find the top 10 users with the most fans:

SQL code used to arrive at answer:   

```SQL	  
SELECT
  id,
  name,
  fans AS total_fans
FROM
  user
ORDER BY
  total_fans DESC
LIMIT
  10	
```   	  

Copy and Paste the Result Below:

| id                     | name      | total_fans |
|------------------------|-----------|------------|
| -9I98YbNQnLdAmcYfb324Q | Amy       |        503 |
| -8EnCioUmDygAbsYZmTeRQ | Mimi      |        497 |
| --2vR0DIsmQ6WfcSzKWigw | Harald    |        311 |
| -G7Zkl1wIWBBmD0KRy_sCw | Gerald    |        253 |
| -0IiMAZI2SsQ7VmyzJjokQ | Christine |        173 |
| -g3XIcCb2b-BD0QBCcq2Sw | Lisa      |        159 |
| -9bbDysuiWeo2VShFJJtcw | Cat       |        133 |
| -FZBTkAZEXoP7CYvRV2ZwQ | William   |        126 |
| -9da1xk7zgnnfO1uTVYGkA | Fran      |        124 |
| -lh59ko3dxChBSZ9U7LfUw | Lissa     |        120 |
	

## Part 2: Inferences and Analysis

### 1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.   

*Checking the Categories:*    

```SQL
SELECT
  category,
  COUNT(category) AS num
FROM
  category
GROUP BY
  category
ORDER BY
  num DESC
```   

| category                  | num |
|---------------------------|-----|
| Restaurants               | 912 |
| Food                      | 425 |
| Shopping                  | 405 |
| Beauty & Spas             | 224 |
| Nightlife                 | 214 |
| Home Services             | 203 |
| Health & Medical          | 196 |
| Bars                      | 185 |
| Local Services            | 166 |
| Automotive                | 163 |
| Active Life               | 122 |
| Event Planning & Services | 119 |
| American (Traditional)    | 105 |
| Fast Food                 | 104 |
| Fashion                   |  98 |
| Coffee & Tea              |  92 |
| Sandwiches                |  90 |
| Pizza                     |  89 |
| Arts & Entertainment      |  87 |
| Hotels & Travel           |  86 |
| Auto Repair               |  84 |
| Burgers                   |  81 |
| Italian                   |  81 |
| Specialty Food            |  79 |
| Hair Salons               |  78 |
(Output limit exceeded, 25 of 712 total rows shown)   


**I chose  Bars**

*Checking the cities:*
```SQL   
SELECT
  city,
  state,
  COUNT(city) AS num
FROM
  business
GROUP BY
  city
ORDER BY
  num DESC
```   

**I Chose Toronto**

**Grouping by stars, it shows only SATURDAY time** 

| name               | city    | category | stars | hours                | Total_reviews |
|--------------------|---------|----------|-------|----------------------|---------------|
| The Fox & Fiddle   | Toronto | Bars     |   2.5 | Saturday 10:00-2:00  |           245 |
| The Charlotte Room | Toronto | Bars     |   3.5 | Saturday 18:00-2:00  |            60 |
| Halo Brewery       | Toronto | Bars     |   4.0 | Saturday 11:00-21:00 |            90 |
| Cabin Fever        | Toronto | Bars     |   4.5 | Saturday 16:00-2:00  |           182 |


**It´s interesting grouping by hours.hours**

| name               | city    | category | stars | hours                 |
|--------------------|---------|----------|-------|-----------------------|
| The Fox & Fiddle   | Toronto | Bars     |   2.5 | Friday 11:00-2:00     |
| Halo Brewery       | Toronto | Bars     |   4.0 | Friday 15:00-21:00    |
| The Charlotte Room | Toronto | Bars     |   3.5 | Friday 15:00-2:00     |
| Cabin Fever        | Toronto | Bars     |   4.5 | Friday 18:00-2:00     |
| The Fox & Fiddle   | Toronto | Bars     |   2.5 | Monday 11:00-2:00     |
| The Charlotte Room | Toronto | Bars     |   3.5 | Monday 15:00-1:00     |
| Cabin Fever        | Toronto | Bars     |   4.5 | Monday 16:00-2:00     |
| The Fox & Fiddle   | Toronto | Bars     |   2.5 | Saturday 10:00-2:00   |
| Halo Brewery       | Toronto | Bars     |   4.0 | Saturday 11:00-21:00  |
| Cabin Fever        | Toronto | Bars     |   4.5 | Saturday 16:00-2:00   |
| The Charlotte Room | Toronto | Bars     |   3.5 | Saturday 18:00-2:00   |
| The Fox & Fiddle   | Toronto | Bars     |   2.5 | Sunday 10:00-2:00     |
| Halo Brewery       | Toronto | Bars     |   4.0 | Sunday 11:00-21:00    |
| Cabin Fever        | Toronto | Bars     |   4.5 | Sunday 16:00-2:00     |
| The Fox & Fiddle   | Toronto | Bars     |   2.5 | Thursday 11:00-2:00   |
| The Charlotte Room | Toronto | Bars     |   3.5 | Thursday 15:00-1:00   |
| Halo Brewery       | Toronto | Bars     |   4.0 | Thursday 15:00-21:00  |
| Cabin Fever        | Toronto | Bars     |   4.5 | Thursday 18:00-2:00   |
| The Fox & Fiddle   | Toronto | Bars     |   2.5 | Tuesday 11:00-2:00    |
| The Charlotte Room | Toronto | Bars     |   3.5 | Tuesday 15:00-1:00    |
| Halo Brewery       | Toronto | Bars     |   4.0 | Tuesday 15:00-21:00   |
| Cabin Fever        | Toronto | Bars     |   4.5 | Tuesday 18:00-2:00    |
| The Fox & Fiddle   | Toronto | Bars     |   2.5 | Wednesday 11:00-2:00  |
| The Charlotte Room | Toronto | Bars     |   3.5 | Wednesday 15:00-1:00  |
| Halo Brewery       | Toronto | Bars     |   4.0 | Wednesday 15:00-21:00 |
(Output limit exceeded, 25 of 26 total rows shown)

i. Do the two groups you chose to analyze have a different distribution of hours?   
**The Bars with highest stars open afernoom, when the Bar with the lowest stars points opens before noom, at 11am.**   

ii. Do the two groups you chose to analyze have a different number of reviews?   
**The Bars with lowest stars have a bit more reviews than the ones with highest stars**       
         
iii. Are you able to infer anything from the location data provided between these two groups? Explain. 

<img src="https://github.com/GePajarinen/SQL-for-Data-Science-Course/blob/main/mapa.jpg?raw=true" alt="map result" style="height: 100px; width:100px;"/>  

**The two bars with the best qualification are located on the west side of the city. As we go to the east, the qualification goes down. The bar with the least amount of stars is located on the east art of the city.
I used google maps and the longitude\latitude informations to pinpoint the locations and get the image**
 
The Fox & Fiddle, 2.5 stars    
The Charlotte Room, 3.5 stars   
Halo Brewery, 4.0 stars   
Cabin Fever, 4.5 stars   

SQL code used for analysis:

```SQL
SELECT
  business.name,
  business.city,
  category.category,
  business.stars,
  hours.hours,
  sum(business.review_count) as Total_reviews
FROM (business
  INNER JOIN
    category
  ON
    business.id = category.business_id)
INNER JOIN
  hours
ON
  hours.business_id = business.id
WHERE
  business.city = 'Toronto'
  AND category.category = "Bars"
GROUP BY
  business.stars

```
		
		
### 2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.
		
i. Difference 1:  

**Comparing on the same category, the ones witch closed have much less total reviews than the ones open.
Well, I could assume that could be a bias:**
**- As we don't know when the closed ones finished their businesses and since the ones open are still getting reviews.**   
**The closed ones, can not get reviews anymore.**

*OPEN by category*
| Quantity |     AvgStrars | totalReviews | category               |
|----------|---------------|--------------|------------------------|
|       53 | 3.45283018868 |         3772 | Restaurants            |
|       25 |           4.0 |          945 | Shopping               |
|       20 |         3.725 |         1588 | Food                   |
|       16 |       4.21875 |          198 | Health & Medical       |
|       15 | 3.93333333333 |           91 | Home Services          |
|       12 | 3.79166666667 |          116 | Beauty & Spas          |
|       12 |         3.625 |          952 | Nightlife              |
|       11 | 3.63636363636 |          945 | Bars                   |
|       10 |          4.15 |          131 | Active Life            |
|       10 |          4.35 |           94 | Local Services         |
|        9 |           4.5 |          198 | Automotive             |
|        8 |        3.8125 |         1114 | American (Traditional) |


*Closed by category*
| Quantity |     AvgStrars | totalReviews | category                  |
|----------|---------------|--------------|---------------------------|
|       18 | 3.47222222222 |          732 | Restaurants               |
|        8 |          3.25 |          399 | Nightlife                 |
|        6 |          3.25 |          377 | Bars                      |
|        5 |           3.9 |           32 | Shopping                  |
|        3 | 3.16666666667 |          190 | American (New)            |
|        3 | 3.83333333333 |           14 | American (Traditional)    |
|        3 | 3.33333333333 |           23 | Event Planning & Services |
|        3 | 4.16666666667 |          193 | Food                      |
|        2 |          4.25 |          102 | Desserts                  |
|        2 |           4.0 |          297 | Gluten-Free               |
|        2 |           3.5 |          148 | Italian                   |
|        2 |          3.25 |            8 | Japanese                  |

SQL code used for analysis:   

```SQL
SELECT
  COUNT(business.is_open) AS Quantity,
  AVG(business.stars) AS AvgStrars,
  SUM(business.review_count) AS totalReviews,
  category.category
FROM
  business
JOIN
  category
ON
  category.business_id = business.id
WHERE
  business.is_open = 1 --0
GROUP BY
  category.category
ORDER BY
  Quantity DESC
LIMIT
  12
``` 
 	 
ii. Difference 2:   
**The closed businesses have got much less reviews classified as useful, cool or funny.**   

| Useful | Funny | Cool | TotalReviews | is_open | Number_businesses |      AvgStars |
|--------|-------|------|--------------|---------|-------------------|---------------|
|     69 |    15 |   30 |         9217 |       0 |                71 | 3.54225352113 |
|    484 |   152 |  219 |       175821 |       1 |               565 |  3.7610619469 |   

SQL code used for analysis:   

```sQL
  SELECT
  SUM(useful) AS Useful,
  SUM(funny) AS Funny,
  SUM(cool) AS Cool,
  SUM(business.review_count) AS TotalReviews,
  business.is_open,
  COUNT(is_open) as Number_businesses, 
  AVG(business.stars) AS AvgStars
FROM
  review
JOIN
  business
ON
  review.business_id = business.id
GROUP BY
  business.is_open   
```         
	
**NOTES:**

| Quantity | is_open |
|----------|---------|
|     1520 |       0 |
|     8480 |       1 |

```SQL
SELECT
  COUNT(is_open) AS Quantity,
  is_open
FROM
  business
WHERE
  is_open = 0 UNION
SELECT
  COUNT(is_open) AS Quantity,
  is_open
FROM
  business
WHERE
  is_open =1
```  
  
### 3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:
	
i. Indicate the type of analysis you chose to do:
         
         
ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:
                           
                  
iii. Output of your finished dataset:
         
         
iv. Provide the SQL code you used to create your final dataset:
