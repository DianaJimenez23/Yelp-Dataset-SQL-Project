Yelp Dataset SQL Project
Prompt taken from SQL for Data Science Course by University of California, Davis
Yelp Dataset SQL Lookup: https://www.coursera.org/learn/sql-for-data-science/supplement/VSJ29/yelp-dataset-sql-lookup

Diana Jimenez

Anaysis indication:

Prediction analysis of which restaurant in Las Vegas has the highest star rating.

Questions asked for answer formation along with queries written to answer each question:

What are the cities provided by the Yelp database?

select cities
from business

+---------------+
| city          |
+---------------+
| Richmond Hill |
| Huntersville  |
| Gilbert       |
| Las Vegas     |
| Tempe         |
| Tempe         |
| Pittsburgh    |
| Pittsburgh    |
| Charlotte     |
| Toronto       |
| Las Vegas     |
| Las Vegas     |
| Charlotte     |
| Henderson     |
| Gilbert       |
| Phoenix       |
| Canonsburg    |
| Bay Village   |
| Streetsboro   |
| Charlotte     |
| Charlotte     |
| Toronto       |
| Scottsdale    |
| Henderson     |
| Edinburgh     |
+---------------+

What are the catagories provided by the Yelp database?

select category
from category

+-----------------------+
| category              |
+-----------------------+
| Shopping              |
| Shopping Centers      |
| Food                  |
| Soul Food             |
| Convenience Stores    |
| Restaurants           |
| Food                  |
| Coffee & Tea          |
| Professional Services |
| Matchmakers           |
| Sandwiches            |
| Restaurants           |
| Shopping              |
| Tobacco Shops         |
| Chiropractors         |
| Health & Medical      |
| Automotive            |
| Oil Change Stations   |
| Car Wash              |
| Auto Detailing        |
| Jewelry Repair        |
| Gold Buyers           |
| Local Services        |
| Shopping              |
| Appraisal Services    |
+-----------------------+

Which city and catagory would you like to analyze?

Las Vegas and Restaurants

How many restaurants are located in Las Vegas (in this dataset), and what are their names?

select
name, city, category
from 
category inner join business on category.business_id = business.id
where
city == 'Las Vegas' AND category == 'Restaurants'

+---------------------+-----------+-------------+
| name                | city      | category    |
+---------------------+-----------+-------------+
| Wingstop            | Las Vegas | Restaurants |
| Big Wong Restaurant | Las Vegas | Restaurants |
| Jacques Cafe        | Las Vegas | Restaurants |
| Hibachi-San         | Las Vegas | Restaurants |
+---------------------+-----------+-------------+

What will be the factor that determines how high a restaurnt's star rating is?

Reviews

select
name, city, category, count(*) as reviews
from 
(category inner join business on category.business_id = business.id)
business inner join review on business.id = review.business_id
where
city == 'Las Vegas' AND category == 'Restaurants'

+---------------------+-----------+-------------+---------+
| name                | city      | category    | reviews |
+---------------------+-----------+-------------+---------+
| Big Wong Restaurant | Las Vegas | Restaurants |       2 |
+---------------------+-----------+-------------+---------+

Are these two reviews good reviews or bad ones? How can we indicate whether they are good or bad?

Look for keywords in the review. I chose to see if the word great was in either two of these reviews.

select
name, city, category, count(*) as good_reviews
from 
(category inner join business on category.business_id = business.id)
business inner join review on business.id = review.business_id
where
city == 'Las Vegas' AND category == 'Restaurants' AND text like "%great%"

+---------------------+-----------+-------------+--------------+
| name                | city      | category    | good_reviews |
+---------------------+-----------+-------------+--------------+
| Big Wong Restaurant | Las Vegas | Restaurants |            2 |
+---------------------+-----------+-------------+--------------+

Both of these reviews have been marked as good reviews.

Conclusion:

From my analysis of the Yelp dataset, I predict that Big Wong Restaurant has the highest star rating out of the four restaurants in Las Vegas.

Results taken from the dataset:

select
name, city, category, stars
from
(category inner join business on category.business_id = business.id)
where
city == 'Las Vegas' AND category == 'Restaurants'

+---------------------+-----------+-------------+-------+
| name                | city      | category    | stars |
+---------------------+-----------+-------------+-------+
| Wingstop            | Las Vegas | Restaurants |   3.0 |
| Big Wong Restaurant | Las Vegas | Restaurants |   4.0 |
| Jacques Cafe        | Las Vegas | Restaurants |   4.0 |
| Hibachi-San         | Las Vegas | Restaurants |   4.5 |
+---------------------+-----------+-------------+-------+

My prediction was wrong. Although Big Wong Restaurant more good reviews than the other restaurants, it did not have the highest star rating. It tied in second place with Jacques Cafe.

