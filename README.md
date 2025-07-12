# Artist-Album-sales-analysis

ANALYSIS OF ARTISTS, ALBUMS, MUSIC SALES, REVENUE GENERATED AND CUSTOMER BEHAVIOUR USING SQL

##INTRODUCTION

With the growing digitization of music, understanding consumer preferences and sales performance has become crucial for music businesses. This database simulates real-world sales and customer data for Geng Music Label in different countries. By analyzing it through SQL, we can evaluate both customer trends, artist and album performance globally.
### Problem Statement
- Which artists and albums generate the most revenue.
- Where top customers are located.
- Which genres or tracks are most popular.
- How spending varies across selected countries and orders.

### OBJECTIVES
- Analyze customer distribution and purchasing power across countries.
- Identify top-performing tracks, albums, and artists.
- Evaluate the genre spread and track volume.
- Provide business recommendation to optimize marketing, promotions and investments.

### TOOLS USED
- SQLLITE

To find all artist and their album, the subquery below was excuted:
````sql
select *,(select name from artist) Artist from album
````
To merge the First and Last name together and also retrive more information my each customer:
````sql
select firstname || '  ' || lastname Name, email, country, country 
from customer
````

To retrive all information of customers in only USA, LIMIT TO 10:
````SQL
SELECT * FROM CUSTOMER
WHERE COUNTRY IN (select country from customer
where country = 'USA')
ORDER BY FIRSTNAME DESC, LASTNAME ASC
LIMIT 10
````
To find the total number of customer in each country:
````sql
SELECT COUNTRY, COUNT(*)TOTAL
FROM CUSTOMER
GROUP BY COUNTRY 
ORDER BY TOTAL DESC
````
